To perform CRUD operations using Angular with API integration, you'll typically use the `HttpClient` service. Below is a step-by-step guide on how to implement this, including examples for each operation.

### Step 1: Set Up Angular Project

If you haven't already, create a new Angular project:

```bash
ng new crud-app
cd crud-app
ng serve
```

### Step 2: Install HttpClient Module

Make sure to import `HttpClientModule` in your `app.module.ts`:

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

### Step 3: Create a Service for API Calls

Create a service to handle HTTP requests:

```bash
ng generate service api
```

In `api.service.ts`, implement CRUD operations:

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ApiService {
  private apiUrl = 'https://jsonplaceholder.typicode.com/users'; // Example API

  constructor(private http: HttpClient) {}

  // Create
  createUser(user: any): Observable<any> {
    return this.http.post(this.apiUrl, user);
  }

  // Read
  getUsers(): Observable<any[]> {
    return this.http.get<any[]>(this.apiUrl);
  }

  // Update
  updateUser(id: number, user: any): Observable<any> {
    return this.http.put(`${this.apiUrl}/${id}`, user);
  }

  // Delete
  deleteUser(id: number): Observable<any> {
    return this.http.delete(`${this.apiUrl}/${id}`);
  }
}
```

### Step 4: Implement CRUD in Component

In your component (e.g., `app.component.ts`), use the service to perform CRUD operations:

```typescript
import { Component, OnInit } from '@angular/core';
import { ApiService } from './api.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html'
})
export class AppComponent implements OnInit {
  users: any[] = [];
  newUser = { name: '', email: '' }; // Example user structure

  constructor(private apiService: ApiService) {}

  ngOnInit() {
    this.loadUsers();
  }

  loadUsers() {
    this.apiService.getUsers().subscribe(data => {
      this.users = data;
    });
  }

  addUser() {
    this.apiService.createUser(this.newUser).subscribe(user => {
      this.users.push(user);
      this.newUser = { name: '', email: '' }; // Reset form
    });
  }

  updateUser(user: any) {
    this.apiService.updateUser(user.id, user).subscribe(() => {
      console.log('User updated!');
    });
  }

  deleteUser(id: number) {
    this.apiService.deleteUser(id).subscribe(() => {
      this.users = this.users.filter(user => user.id !== id);
      console.log('User deleted!');
    });
  }
}
```

### Step 5: Create the Template

In `app.component.html`, create a simple form and display the users:

```html
<h1>CRUD Operations</h1>

<form (ngSubmit)="addUser()">
  <input type="text" [(ngModel)]="newUser.name" name="name" placeholder="Name" required>
  <input type="email" [(ngModel)]="newUser.email" name="email" placeholder="Email" required>
  <button type="submit">Add User</button>
</form>

<ul>
  <li *ngFor="let user of users">
    {{ user.name }} ({{ user.email }})
    <button (click)="updateUser(user)">Update</button>
    <button (click)="deleteUser(user.id)">Delete</button>
  </li>
</ul>
```

### Summary

1. **Service**: Handles API calls for CRUD operations.
2. **Component**: Manages user interactions and displays data.
3. **Template**: Provides a UI for users to interact with.

### Running the Application

After implementing the above steps, run your Angular application:

```bash
ng serve
```

You can now perform CRUD operations using the example API provided. Adjust the API URLs and data structures as needed for your specific application.