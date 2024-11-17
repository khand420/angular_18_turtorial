Here’s an explanation of the data binding concepts mentioned in the image, along with examples for each use case:

### 1. One Way Data Binding

This type of data binding allows data to flow in one direction, either from the component to the view or from the view to the component.

#### a. From `.ts` to `.html` (Interpolation and Property Binding)

**Example:**

- **Interpolation**: This is used to display component properties in the template.

```typescript
// TypeScript Component (app.component.ts)
export class AppComponent {
  title: string = 'Angular Data Binding Example';
}
```

```html
<!-- HTML Template (app.component.html) -->
<h1>{{ title }}</h1>
```

- **Property Binding**: This is used to bind data to an HTML element's property.

```typescript
// TypeScript Component
export class AppComponent {
  imageUrl: string = 'https://example.com/image.png';
}
```

```html
<!-- HTML Template -->
<img [src]="imageUrl" alt="Example Image">
```

#### b. From `.html` to `.ts` (Event Binding)

Event binding allows the view to send data back to the component when an event occurs.

**Example:**

```typescript
// TypeScript Component
export class AppComponent {
  onButtonClick() {
    console.log('Button clicked!');
  }
}
```

```html
<!-- HTML Template -->
<button (click)="onButtonClick()">Click Me</button>
```

### 2. Two Way Data Binding

Two-way data binding allows for synchronization between the model and the view. Any changes in the model are reflected in the view and vice versa.

**Example: Using `ngModel`**

To use two-way data binding, you typically use the `ngModel` directive.

```typescript
// TypeScript Component
export class AppComponent {
  name: string = '';
}
```

```html
<!-- HTML Template -->
<input [(ngModel)]="name" placeholder="Enter your name">
<p>Your name is: {{ name }}</p>
```

In this example, when the user types in the input field, the `name` property in the component is updated in real-time, and vice versa.

### 3. Using Signal (Angular 17 Onwards)

Signals in Angular are a new way to manage state and reactivity. They provide a more efficient way to handle changes in data.

**Example:**

```typescript
import { component$, useSignal } from '@builder.io/qwik';

export const MyComponent = component$(() => {
  const count = useSignal(0);

  return (
    <div>
      <button onClick$={() => count.value++}>Increment</button>
      <p>Count: {count.value}</p>
    </div>
  );
});
```

In this example, clicking the button increments the `count` signal, and the displayed count updates automatically.

### Summary

- **One Way Data Binding**: Data flows in one direction (from component to view or view to component).
- **Two Way Data Binding**: Data flows in both directions, allowing for real-time synchronization between the model and the view using `ngModel`.
- **Using Signal**: An efficient way to manage state and reactivity introduced in Angular 17, allowing for better performance and easier state management.

If you have any specific questions or need further examples, feel free to ask!