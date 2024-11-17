### ng-container Directive in Angular

#### What is ng-container?
`ng-container` is an Angular directive that acts as a logical container for grouping elements without adding any additional DOM elements. It is useful for applying structural directives like `*ngIf`, `*ngFor`, or `*ngSwitch` without introducing extra wrapping elements in the HTML.

#### How to use ng-container?
You can use `ng-container` to conditionally render elements or iterate over a collection without affecting the DOM structure.

**Example: Using ng-container with ngIf**
```html
<ng-container *ngIf="isLoggedIn">
  <p>Welcome back!</p>
</ng-container>
```

**Example: Using ng-container with ngFor**
```html
<ng-container *ngFor="let item of items">
  <li>{{ item }}</li>
</ng-container>
```

#### How to use ng-template & ng-container together?
You can combine `ng-template` and `ng-container` to create reusable templates and manage conditional rendering effectively.

**Example: Using ng-template with ng-container**
```html
<ng-template #loginTemplate>
  <p>Please log in.</p>
</ng-template>

<ng-container *ngIf="!isLoggedIn; else loginTemplate">
  <p>Welcome back!</p>
</ng-container>
```

### Summary
- **ng-container**: A logical container that does not add extra elements to the DOM.
- **ng-template**: Defines a template that can be reused and rendered conditionally.
- **Combining**: Use `ng-container` to manage structural directives and `ng-template` for reusable templates.

If you need more examples or further explanation, feel free to ask!