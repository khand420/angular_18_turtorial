In Angular, **pipes** are a powerful feature that allows you to transform data in templates. They can be used to format data, filter lists, and manipulate strings, among other things. Pipes take in data as input and return a transformed value.

### Types of Pipes in Angular

1. **Built-in Pipes**:
   - **DatePipe**: Formats dates.
     - **Example**: `{{ today | date:'fullDate' }}` formats the current date.
   - **CurrencyPipe**: Formats numbers as currency.
     - **Example**: `{{ price | currency:'USD':'symbol':'1.2-2' }}` displays a price in USD.
   - **DecimalPipe**: Formats numbers with decimal points.
     - **Example**: `{{ number | number:'1.0-2' }}` formats a number to two decimal places.
   - **PercentPipe**: Converts a number to a percentage.
     - **Example**: `{{ fraction | percent }}` converts 0.25 to 25%.
   - **SlicePipe**: Creates a new array or string containing a subset of the original.
     - **Example**: `{{ items | slice:1:3 }}` returns items from index 1 to 2.
   - **AsyncPipe**: Unwraps observable or promise values.
     - **Example**: `{{ data$ | async }}` displays the latest value from an observable.

2. **Custom Pipes**:
   - You can create your own pipes to encapsulate specific transformation logic.
   - **Example**:
     ```typescript
     import { Pipe, PipeTransform } from '@angular/core';

     @Pipe({ name: 'exponentialStrength' })
     export class ExponentialStrengthPipe implements PipeTransform {
       transform(value: number, exponent: string): number {
         const exp = parseFloat(exponent);
         return Math.pow(value, isNaN(exp) ? 1 : exp);
       }
     }
     ```
   - **Usage**: `{{ 2 | exponentialStrength:10 }}` returns 1024.

### Use Cases

1. **Formatting Dates**:
   - Use `DatePipe` to display dates in a user-friendly format in a dashboard.

2. **Displaying Prices**:
   - Use `CurrencyPipe` to show prices in different currencies based on user preferences.

3. **Showing Percentages**:
   - Use `PercentPipe` to display completion rates in a progress bar.

4. **Filtering Lists**:
   - Use custom pipes to filter lists of items, such as searching through a list of products.

5. **Transforming Data for Charts**:
   - Use pipes to format data before displaying it in charts or graphs.

### Example in an Angular Component

Here’s a simple example of using pipes in an Angular component:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `
    <h1>Angular Pipes Example</h1>
    <p>Today's date: {{ today | date:'fullDate' }}</p>
    <p>Price: {{ price | currency:'USD' }}</p>
    <p>Completion: {{ fraction | percent }}</p>
  `
})
export class ExampleComponent {
  today: number = Date.now();
  price: number = 123.45;
  fraction: number = 0.75;
}
```

### Summary

Pipes in Angular are a great way to transform data in templates. They can simplify the presentation of data without cluttering your component logic, making your code cleaner and more maintainable.