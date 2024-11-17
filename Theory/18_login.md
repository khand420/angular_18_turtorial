To implement a login feature in Angular that uses different tokens for authentication (like JWT), you can follow these steps:

### Step 1: Set Up Angular Project

If you haven't already set up an Angular project, run:

```bash
ng new my-app
cd my-app
ng serve
```

### Step 2: Install HttpClient Module

Make sure to install the `HttpClientModule` for making HTTP requests:

```bash
ng generate module app-routing --flat --module=app
```

Then, import `HttpClientModule` in your `app.module.ts`:

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http'; // Import HttpClientModule
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { LoginComponent } from './login/login.component';

@NgModule({
  declarations: [
    AppComponent,
    LoginComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule, // Add HttpClientModule here
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Step 3: Create Auth Service

Generate a new service for authentication:

```bash
ng generate service auth
```

Update `auth.service.ts` to handle login and token storage:

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private apiUrl = 'https://your-api-url.com/login'; // Replace with your API URL

  constructor(private http: HttpClient) { }

  login(username: string, password: string): Observable<any> {
    return this.http.post(this.apiUrl, { username, password });
  }

  saveToken(token: string) {
    localStorage.setItem('authToken', token);
  }

  getToken() {
    return localStorage.getItem('authToken');
  }

  isLoggedIn() {
    return !!this.getToken();
  }

  logout() {
    localStorage.removeItem('authToken');
  }
}
```

### Step 4: Update Login Component

Edit `login.component.ts` to use the `AuthService`:

```typescript
import { Component } from '@angular/core';
import { AuthService } from '../auth.service';

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
  styleUrls: ['./login.component.css']
})
export class LoginComponent {
  username: string = '';
  password: string = '';
  errorMessage: string = '';

  constructor(private authService: AuthService) {}

  onLogin() {
    this.authService.login(this.username, this.password).subscribe({
      next: (response) => {
        const token = response.token; // Adjust based on your API response structure
        this.authService.saveToken(token);
        console.log('Login successful, token:', token);
        // Redirect or perform additional actions
      },
      error: (err) => {
        this.errorMessage = 'Login failed. Please check your credentials.';
        console.error(err);
      }
    });
  }
}
```

### Step 5: Update Login Template

Update `login.component.html` to display error messages:

```html
<div class="login-container">
  <h2>Login</h2>
  <form (ngSubmit)="onLogin()">
    <div>
      <label for="username">Username:</label>
      <input type="text" id="username" [(ngModel)]="username" name="username" required>
    </div>
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" [(ngModel)]="password" name="password" required>
    </div>
    <button type="submit">Login</button>
    <div *ngIf="errorMessage" class="error">{{ errorMessage }}</div>
  </form>
</div>
```

### Step 6: Use Login Component

Ensure you're using the login component in your `app.component.html`:

```html
<app-login></app-login>
```

### Step 7: Run Your Application

Run your Angular application:

```bash
ng serve
```

### Step 8: Additional Considerations

- **Backend API**: Ensure your backend API is set up to handle login requests and respond with a token.
- **Token Expiration**: Handle token expiration and refresh logic if needed.
- **Routing**: Implement routing to navigate to different parts of your application after successful login.
- **Guarding Routes**: Consider using route guards to protect routes that require authentication.

This setup provides a basic structure for handling login with token-based authentication in Angular. If you have any further questions or need additional features, feel free to ask!