

### Function arguments

- Use of maximum 3 arguments
- Never use optionals as arguments, always use those in an options object.

### Single Argument

❌ Bad
```ts
function (options:{ name: string }){
  // 
}
```

✅ Good
```ts
function (name:string) {
  //
}
```

### Two arguments with optional


❌ Bad
```ts
function (firstName:string, lastName?: string = '') {
  //
}
```

✅ Good
```ts
function (options: { firstName: string, lastName?: string }){
  //
}
```

### Many arguments


❌ Bad
```ts
function (firstName:string, lastName: string, age: number, place: string) {
  //
}
```

✅ Good
```ts
function (options: { firstName: string, lastName: string, age: number, place: string }){
  //
}
```
