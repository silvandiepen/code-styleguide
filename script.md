# Function Argument Best Practices

When designing functions, it's crucial to maintain clarity and flexibility in how arguments are handled. Adhering to best practices for function arguments can significantly improve code readability and maintainability. Below are some guidelines and examples illustrating the preferred approach to using function arguments in TypeScript.

### Single Argument

❌ Bad

```ts
function greet(name: string) {
  console.log(`Hello, ${name}`);
}
```

✅ Good

For single arguments where only one parameter is needed, using a direct parameter is straightforward:

```ts
function greet(name: string) {
  console.log(`Hello, ${name}`);
}
```

### Two Arguments with Optional

❌ Bad

When dealing with optional arguments, mixing them directly in the parameter list can lead to confusion:

```ts
function formatName(firstName: string, lastName?: string = '') {
  console.log(`${firstName} ${lastName}`);
}
```

✅ Good

Encapsulating parameters in an options object improves clarity and flexibility:

```ts
interface NameOptions {
  firstName: string;
  lastName?: string;
}

function formatName({ firstName, lastName = '' }: NameOptions) {
  console.log(`${firstName} ${lastName}`);
}
```

### Many Arguments

❌ Bad

Functions with multiple parameters directly listed can be cumbersome and harder to manage:

```ts
function registerUser(firstName: string, lastName: string, age: number, place: string) {
  console.log(`${firstName} ${lastName}, Age: ${age}, Place: ${place}`);
}
```

✅ Good

Using an options object to handle multiple parameters simplifies function signatures and enhances readability:

```ts
interface UserOptions {
  firstName: string;
  lastName: string;
  age: number;
  place: string;
}

function registerUser({ firstName, lastName, age, place }: UserOptions) {
  console.log(`${firstName} ${lastName}, Age: ${age}, Place: ${place}`);
}
```

### Summary

Using options objects for managing function arguments can make your code more readable and maintainable. For simple cases with only one parameter, direct arguments are sufficient. For functions with multiple parameters or optional values, encapsulating parameters within an object offers greater flexibility and clarity, making your functions easier to understand and extend in the future.
