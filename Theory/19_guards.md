In Angular, route guards are used to control access to certain routes in your application based on specific conditions, such as whether a user is authenticated. Here’s how to create an authentication guard using Angular's built-in routing features.

### Step 1: Generate an Auth Guard

You can generate an auth guard using the Angular CLI:

```bash
ng generate guard auth
```

This will create an `auth.guard.ts` file in your project.

### Step 2: Implement the Auth Guard

Edit the `auth.guard.ts` file to implement the logic for checking if a user is authenticated:

```typescript
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, RouterStateSnapshot, Router } from '@angular/router';
import { AuthService } from './auth.service'; // Adjust the path as necessary

@Injectable({
  providedIn: 'root'
})
export class AuthGuard implements CanActivate {

  constructor(private authService: AuthService, private router: Router) {}

  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): boolean {
    if (this.authService.isLoggedIn()) {
      return true; // User is authenticated, allow access
    } else {
      this.router.navigate(['/login']); // Redirect to login if not authenticated
      return false; // Deny access
    }
  }
}
```

### Step 3: Update Your Routes

Next, you need to apply the guard to your routes. Open your routing module (usually `app-routing.module.ts`) and update your routes to use the `AuthGuard`:

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { LoginComponent } from './login/login.component';
import { ProtectedComponent } from './protected/protected.component'; // Example protected component
import { AuthGuard } from './auth.guard'; // Import your AuthGuard

const routes: Routes = [
  { path: 'login', component: LoginComponent },
  { path: 'protected', component: ProtectedComponent, canActivate: [AuthGuard] }, // Protect this route
  { path: '', redirectTo: '/login', pathMatch: 'full' },
  { path: '**', redirectTo: '/login' } // Redirect unknown paths to login
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### Step 4: Create a Protected Component (Optional)

If you don’t have a protected component, you can create one for testing:

```bash
ng generate component protected
```

Add some content to `protected.component.html`:

```html
<h2>Protected Route</h2>
<p>You can only see this if you are logged in!</p>
```

### Step 5: Test the Guard

1. **Run your application**:

   ```bash
   ng serve
   ```

2. **Navigate to the protected route** (`/protected`) without logging in. You should be redirected to the login page.

3. **Log in** using the login form. If the authentication is successful, you should be able to access the protected route.

### Step 6: Additional Considerations

- **Role-Based Access**: If you want to implement role-based access, you can modify the guard to check the user's role before granting access.
- **Guarding Child Routes**: You can also apply guards to child routes by specifying `canActivate` in the child route configuration.
- **Multiple Guards**: You can combine multiple guards by providing them in an array.

This setup provides a simple yet effective way to control access to routes in your Angular application using route guards. If you have any further questions or need additional features, feel free to ask!