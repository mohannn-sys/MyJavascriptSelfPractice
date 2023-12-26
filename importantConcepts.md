# Scope
In JavaScript, the concept of scope refers to the region of the code where a particular variable can be accessed or modified. It defines the visibility and 
lifetime of variables and parameters during the execution of a program. Understanding scope is crucial for writing maintainable and bug-free code. There are two 
main types of scope in JavaScript:

### 1. **Global Scope:**
   - Variables declared outside of any function or block have global scope.
   - They can be accessed and modified from any part of the code, including within functions.
   - Global variables persist throughout the entire lifetime of the application.

   **Example:**
   ```javascript
   var globalVar = 'I am global';

   function exampleFunction() {
     console.log(globalVar); // Accessible within the function
   }

   exampleFunction();
   console.log(globalVar); // Accessible outside the function
   ```

### 2. **Local Scope:**
   - Variables declared inside a function, block, or any other code structure have local scope.
   - They are only accessible within the function or block in which they are declared.
   - Local variables have a shorter lifetime, existing only during the execution of the function or block.

   **Example:**
   ```javascript
   function exampleFunction() {
     var localVar = 'I am local';
     console.log(localVar); // Accessible within the function
   }

   exampleFunction();
   // console.log(localVar); // Uncommenting this line would result in an error
   ```

### Scope Chain:
- JavaScript follows a hierarchical structure for scope known as the "scope chain."
- When a variable is accessed, JavaScript looks for it in the current scope. If not found, it looks in the outer (enclosing) scope,
  continuing up the chain until the global scope.
- This behavior is fundamental to understanding how variables are resolved in nested functions.

   **Example:**
   ```javascript
   var globalVar = 'I am global';

   function outerFunction() {
     var outerVar = 'I am outer';

     function innerFunction() {
       var innerVar = 'I am inner';
       console.log(innerVar);   // Accessible directly
       console.log(outerVar);   // Accessible via the outer scope
       console.log(globalVar);  // Accessible via the global scope
     }

     innerFunction();
     // console.log(innerVar); // Uncommenting this line would result in an error
   }

   outerFunction();
   ```

### Block Scope (Introduced in ES6):

- Prior to ECMAScript 6 (ES6), JavaScript only had function scope.
- With the introduction of `let` and `const` in ES6, block scope was introduced.
- Variables declared with `let` and `const` are block-scoped, meaning they are confined to the nearest pair of curly braces `{}`.

   **Example:**
   ```javascript
   if (true) {
     var functionScopedVar = 'I am function-scoped';
     let blockScopedVar = 'I am block-scoped';
     const alsoBlockScoped = 'I am also block-scoped';
   }

   // console.log(functionScopedVar); // Accessible (function scope)
   // console.log(blockScopedVar);    // Uncommenting this line would result in an error
   // console.log(alsoBlockScoped);   // Uncommenting this line would result in an error
   ```

### `var`, `let`, and `const` in Relation to Scope:

- Variables declared with `var` are function-scoped or globally-scoped.
- Variables declared with `let` and `const` are block-scoped.

   **Example:**
   ```javascript
   function example() {
     if (true) {
       var functionScopedVar = 'I am function-scoped';
       let blockScopedVar = 'I am block-scoped';
     }

     console.log(functionScopedVar);  // Accessible (function scope)
     // console.log(blockScopedVar);  // Uncommenting this line would result in an error
   }
   ```

# Hoisting
Hoisting is a behavior in JavaScript where variable and function declarations are moved to the top of their containing scope during the compilation phase. 
This means that you can use variables and functions before they are declared in the code. However, it's important to note that only the declarations are hoisted, 
not the initializations.

There are two main types of hoisting in JavaScript: hoisting of variable declarations (`var`) and hoisting of function declarations.

### Hoisting of Variable Declarations (`var`):

When a variable is declared using `var`, the declaration is hoisted to the top of its containing scope, but the initialization remains in place. 
If the variable is accessed before its declaration, it will have the value `undefined`.

**Example:**
```javascript
console.log(x); // Outputs: undefined (hoisted)
var x = 5;
console.log(x); // Outputs: 5
```

In this example, the variable `x` is hoisted to the top, but its initialization (`x = 5`) remains in the original position.

### Hoisting of Function Declarations:

Function declarations are also hoisted, meaning you can use a function before it's declared in the code.

**Example:**
```javascript
sayHello(); // Outputs: Hello, World!
function sayHello() {
  console.log('Hello, World!');
}
```

In this example, the `sayHello` function is hoisted to the top, allowing it to be called before the actual declaration.

### Hoisting with `let` and `const`:

Unlike `var`, variables declared with `let` and `const` are hoisted to the top of their block or scope but are not initialized until the actual declaration. 
Accessing them before the declaration results in a `ReferenceError`.

**Example:**
```javascript
// console.log(y); // Uncommenting this line would result in a ReferenceError
let y = 10;
```

In this example, attempting to access `y` before its declaration would result in an error.

### Hoisting of Function Expressions:

Function expressions are not hoisted in the same way as function declarations. If a function is assigned to a variable using a function expression, 
the variable declaration is hoisted, but the assignment remains in place.

**Example:**
```javascript
// console.log(square); // Uncommenting this line would result in undefined
var square = function(x) {
  return x * x;
};
console.log(square(5)); // Outputs: 25
```

In this example, the variable `square` is hoisted to the top, but its assignment (`square = function(x) { ... }`) remains in the original position.

### Recommendations:

- It's generally considered good practice to declare variables at the top of their scope to avoid unexpected behavior due to hoisting.
- While hoisting can be useful, relying on it for clarity in code is not recommended. Code readability is improved by declaring and initializing variables and
  functions in a logical order.

