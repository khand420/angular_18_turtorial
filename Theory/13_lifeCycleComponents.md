
1. **What are Component Life Cycle Events?**
2. **How to Write Life Cycle Events?**
3. **Sequence of Life Cycle Events?**
4. **Which Life Cycle Event do we mostly use?**

### Answers:

1. **What are Component Life Cycle Events?**
   - Component lifecycle events are specific points in time during a component's existence in Angular. These events allow developers to hook into the lifecycle of a component to perform actions at specific stages (like initialization, change detection, destruction, etc.). Key lifecycle events include:
     - `ngOnInit()`
     - `ngOnChanges()`
     - `ngOnDestroy()`
     - `ngDoCheck()`
     - `ngAfterViewInit()`, among others.

2. **How to Write Life Cycle Events?**
   - To implement lifecycle events, you need to import the necessary lifecycle interfaces from Angular and then define methods in your component class. For example:
   ```typescript
   import { Component, OnInit } from '@angular/core';

   @Component({
     selector: 'app-example',
     templateUrl: './example.component.html',
   })
   export class ExampleComponent implements OnInit {
     ngOnInit() {
       // Code to run on component initialization
     }
   }
   ```

3. **Sequence of Life Cycle Events?**
   - The sequence of lifecycle events in Angular typically follows this order:
     1. `ngOnChanges()`
     2. `ngOnInit()`
     3. `ngDoCheck()`
     4. `ngAfterContentInit()`
     5. `ngAfterContentChecked()`
     6. `ngAfterViewInit()`
     7. `ngAfterViewChecked()`
     8. `ngOnDestroy()`

4. **Which Life Cycle Event do we mostly use?**
   - The most commonly used lifecycle events are:
     - `ngOnInit()`: for initialization logic.
     - `ngOnDestroy()`: for cleanup logic before the component is destroyed.
   - These methods are essential for managing resources, subscriptions, and component states effectively.





Sure! Here are detailed examples for each of the lifecycle events mentioned, along with explanations:

### 1. **ngOnInit()**
This lifecycle hook is called once after the component is initialized. It's a good place to perform initialization logic.

**Example:**
```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user',
  template: `<h1>{{ user.name }}</h1>`,
})
export class UserComponent implements OnInit {
  user: { name: string };

  ngOnInit() {
    // Simulate fetching user data from a service
    this.user = { name: 'John Doe' };
    console.log('User data initialized:', this.user);
  }
}
```

### 2. **ngOnChanges()**
This hook is called whenever any data-bound input properties change. It receives a `SimpleChanges` object that contains the current and previous values.

**Example:**
```typescript
import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';

@Component({
  selector: 'app-greeting',
  template: `<p>Hello, {{ name }}!</p>`,
})
export class GreetingComponent implements OnChanges {
  @Input() name: string;

  ngOnChanges(changes: SimpleChanges) {
    console.log('Changes detected:', changes);
  }
}
```

### 3. **ngOnDestroy()**
This lifecycle hook is called just before the component is destroyed. It's used for cleanup, such as unsubscribing from observables.

**Example:**
```typescript
import { Component, OnDestroy } from '@angular/core';
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-data',
  template: `<p>Data Component</p>`,
})
export class DataComponent implements OnDestroy {
  private subscription: Subscription;

  constructor() {
    // Simulate an observable subscription
    this.subscription = new Subscription();
  }

  ngOnDestroy() {
    // Cleanup logic
    this.subscription.unsubscribe();
    console.log('DataComponent destroyed and subscription cleaned up.');
  }
}
```

### 4. **ngDoCheck()**
This hook is called during every change detection run. It allows you to implement your custom change detection logic.

**Example:**
```typescript
import { Component, DoCheck } from '@angular/core';

@Component({
  selector: 'app-checker',
  template: `<p>Check my changes!</p>`,
})
export class CheckerComponent implements DoCheck {
  data: number = 0;

  ngDoCheck() {
    // Custom change detection logic
    console.log('Change detection running, current data:', this.data);
  }
}
```

### 5. **ngAfterViewInit()**
This lifecycle hook is called after the component's view has been fully initialized. It’s useful for DOM manipulation.

**Example:**
```typescript
import { Component, AfterViewInit, ElementRef, ViewChild } from '@angular/core';

@Component({
  selector: 'app-view',
  template: `<div #myDiv>Hello World!</div>`,
})
export class ViewComponent implements AfterViewInit {
  @ViewChild('myDiv') myDiv: ElementRef;

  ngAfterViewInit() {
    // Accessing the DOM element
    this.myDiv.nativeElement.style.color = 'blue';
    console.log('View initialized:', this.myDiv.nativeElement.innerText);
  }
}







```

Sure! Here’s a single Angular component that demonstrates the use of multiple lifecycle hooks: `ngOnInit`, `ngOnChanges`, `ngOnDestroy`, `ngDoCheck`, and `ngAfterViewInit`. This will give you a comprehensive understanding of how these hooks work together in a component.

### Combined Example Component

```typescript
import { Component, Input, OnInit, OnChanges, OnDestroy, DoCheck, AfterViewInit, SimpleChanges, ElementRef, ViewChild } from '@angular/core';
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-combined',
  template: `
    <h1>{{ user.name }}</h1>
    <p>Hello, {{ name }}!</p>
    <div #myDiv>Hello World!</div>
  `,
})
export class CombinedComponent implements OnInit, OnChanges, OnDestroy, DoCheck, AfterViewInit {
  @Input() name: string;
  user: { name: string };
  private subscription: Subscription;

  @ViewChild('myDiv') myDiv: ElementRef;

  ngOnInit() {
    // Simulate fetching user data
    this.user = { name: 'John Doe' };
    console.log('User data initialized:', this.user);
  }

  ngOnChanges(changes: SimpleChanges) {
    console.log('Changes detected:', changes);
  }

  ngDoCheck() {
    // Custom change detection logic
    console.log('Change detection running, current name:', this.name);
  }

  ngAfterViewInit() {
    // Accessing the DOM element
    this.myDiv.nativeElement.style.color = 'blue';
    console.log('View initialized:', this.myDiv.nativeElement.innerText);
  }

  ngOnDestroy() {
    // Cleanup logic
    if (this.subscription) {
      this.subscription.unsubscribe();
      console.log('CombinedComponent destroyed and subscription cleaned up.');
    }
  }
}
```

### Explanation of the Code:

1. **Imports**: The necessary Angular modules and decorators are imported.
2. **Component Decorator**: The `@Component` decorator defines the selector and template for the component.
3. **Inputs**: The `name` property is marked with `@Input()`, allowing it to receive data from a parent component.
4. **Lifecycle Hooks**:
   - **ngOnInit**: Initializes the user data.
   - **ngOnChanges**: Logs changes to the `name` input property when it changes.
   - **ngDoCheck**: Custom logic to check for changes in the component.
   - **ngAfterViewInit**: Changes the color of a DOM element after the view is initialized.
   - **ngOnDestroy**: Cleans up any subscriptions when the component is destroyed (even though no actual subscription is created in this example, it's set up for demonstration).

### Usage
You can use this component in your Angular application by including it in a parent component and passing a `name` input to it. This will trigger the lifecycle hooks as the component is created, updated, and destroyed. 

If you have any further questions or need additional modifications, feel free to ask!