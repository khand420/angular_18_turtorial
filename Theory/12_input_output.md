

1. **What is a reusable component?**
2. **What is the use of Input?**
3. **What is the use of Output?**
4. **When do we have to create reusable components?**

### Answers:

1. **What is a reusable component?**
   - A reusable component in Angular is a component designed to be used multiple times throughout an application. It encapsulates functionality and UI, allowing it to be easily integrated into different parts of the app without duplicating code.

2. **What is the use of Input?**
   - The `@Input()` decorator is used to pass data from a parent component to a child component. It allows the parent to bind values to properties of the child component, enabling dynamic data sharing.

   **Example:**
   ```typescript
   @Input() title: string;
   ```

3. **What is the use of Output?**
   - The `@Output()` decorator is used to emit events from a child component to a parent component. It allows the child to communicate back to the parent, often used for handling user interactions or notifying the parent of changes.

   **Example:**
   ```typescript
   @Output() notify: EventEmitter<string> = new EventEmitter<string>();
   ```

4. **When do we have to create reusable components?**
   - Reusable components should be created when:
     - A piece of functionality or UI is needed in multiple places within an application.
     - You want to follow the DRY (Don't Repeat Yourself) principle, reducing code duplication.
     - You aim to make the application more maintainable and organized.

These concepts are fundamental in Angular development, especially when building scalable and maintainable applications. If you need further details or examples, feel free to ask!