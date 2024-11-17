In Angular, **template-driven forms** are a way to create forms using Angular directives in your HTML templates. They are easy to use and suitable for simple forms. Validation can be applied to ensure that user input meets specified criteria.

### Template-Driven Forms

1. **Setting Up a Template-Driven Form**:
   - Import `FormsModule` in your `app.module.ts`.
   - Use the `ngForm` directive in your template.

2. **Basic Example**:

```typescript
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [AppComponent],
  imports: [BrowserModule, FormsModule],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
})
export class AppComponent {
  user = {
    name: '',
    email: ''
  };

  onSubmit(form: any) {
    console.log('Form Submitted!', form);
  }
}
```

```html
<!-- app.component.html -->
<form #userForm="ngForm" (ngSubmit)="onSubmit(userForm)">
  <div>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" ngModel required>
    <div *ngIf="userForm.controls.name?.invalid && userForm.controls.name?.touched">
      Name is required.
    </div>
  </div>
  
  <div>
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" ngModel required email>
    <div *ngIf="userForm.controls.email?.invalid && userForm.controls.email?.touched">
      <div *ngIf="userForm.controls.email?.errors?.required">Email is required.</div>
      <div *ngIf="userForm.controls.email?.errors?.email">Invalid email format.</div>
    </div>
  </div>

  <button type="submit" [disabled]="userForm.invalid">Submit</button>
</form>
```

### Validation

- **Built-in Validators**: Angular provides several built-in validators such as `required`, `minlength`, `maxlength`, and `email`.
- **Custom Validators**: You can create custom validators for more complex validation logic.

### Example of Custom Validator

```typescript
// custom-validators.ts
import { AbstractControl, ValidatorFn } from '@angular/forms';

export function forbiddenNameValidator(nameRe: RegExp): ValidatorFn {
  return (control: AbstractControl): { [key: string]: any } | null => {
    const forbidden = nameRe.test(control.value);
    return forbidden ? { 'forbiddenName': { value: control.value } } : null;
  };
}
```

### Interview Questions (Tricky)

1. **What is the difference between reactive forms and template-driven forms?**
   - **Answer**: Reactive forms are more scalable and provide more control over form validation and state management. Template-driven forms are simpler and more suitable for basic forms.

2. **How would you implement custom validation in a template-driven form?**
   - **Answer**: You can create a custom validator function and apply it using the `ngModel` directive. You can also use the `ngModel` directive's `ngModelOptions` to specify additional options like `updateOn`.

3. **How do you handle form submission in Angular?**
   - **Answer**: You can handle form submission by binding the `(ngSubmit)` event to a method in your component and passing the form object as an argument.

4. **What happens if you don't provide a `name` attribute in an input field in a template-driven form?**
   - **Answer**: Without a `name` attribute, the control will not be registered in the form, and you won't be able to access its value or validation status.

5. **How can you reset a form in Angular?**
   - **Answer**: You can reset a form by calling the `reset()` method on the form object, which can be accessed through the template reference variable.

### Summary

Template-driven forms in Angular are straightforward to implement and provide a simple way to handle user input and validation. Understanding how to work with these forms, including built-in and custom validators, is essential for building robust applications. Being prepared for tricky interview questions will help demonstrate your knowledge and problem-solving skills.