# ES6
ECMAScript 6, also known as ES6 or ECMAScript 2015, is the sixth edition of the ECMAScript standard. It was released in 2015 and brought significant enhancements to the 
JavaScript language. ES6 aimed to make JavaScript more readable, maintainable, and scalable for larger applications. Some key features introduced in ES6 include:

## 1. Class:
ES6 introduced a more convenient and syntactically cleaner way to work with object-oriented programming in JavaScript through the introduction of classes. 
The class syntax in ES6 provides a more familiar and readable syntax for creating objects and dealing with inheritance. Here's an overview of ES6 classes:

### 1. Class Declaration:

To declare a class, you use the `class` keyword, followed by the class name. The body of the class contains methods and properties.

```javascript
class Animal {
  // Constructor method
  constructor(name, sound) {
    this.name = name;
    this.sound = sound;
  }

  // Method
  makeSound() {
    console.log(`${this.name} says ${this.sound}`);
  }
}
```

### 2. Constructor Method:

The `constructor` method is a special method used for initializing instances of the class. It is called automatically when a new object is created from the class. 
It is used to set up the initial state of the object.

### 3. Creating Instances:

To create an instance of a class, you use the `new` keyword followed by the class name. The constructor is called with the provided arguments.

```javascript
const cat = new Animal('Whiskers', 'Meow');
const dog = new Animal('Buddy', 'Woof');
```

### 4. Methods:

Methods in a class are functions defined within the class body. They can be called on instances of the class.

```javascript
cat.makeSound();  // Outputs: Whiskers says Meow
dog.makeSound();  // Outputs: Buddy says Woof
```

### 5. Inheritance:

ES6 classes support inheritance through the `extends` keyword. This allows a class to inherit the properties and methods of another class.

```javascript
class Dog extends Animal {
  // Additional method
  bark() {
    console.log(`${this.name} barks loudly!`);
  }
}

const puppy = new Dog('Rover', 'Woof');
puppy.makeSound();  // Outputs: Rover says Woof
puppy.bark();       // Outputs: Rover barks loudly!
```

In the example above, the `Dog` class extends the `Animal` class, inheriting its `makeSound` method. The `bark` method is specific to the `Dog` class.

### 6. Getters and Setters:

ES6 classes also support getter and setter methods, allowing you to control access to properties of an object.

```javascript
class Circle {
  constructor(radius) {
    this._radius = radius;
  }

  get radius() {
    return this._radius;
  }

  set radius(newRadius) {
    if (newRadius > 0) {
      this._radius = newRadius;
    } else {
      console.error('Radius must be greater than 0');
    }
  }
}

const myCircle = new Circle(5);
console.log(myCircle.radius);    // Outputs: 5
myCircle.radius = 8;              // Sets a new radius
console.log(myCircle.radius);    // Outputs: 8
myCircle.radius = -3;             // Outputs: Radius must be greater than 0 (Error message)
```

### 7. Static Methods:

Static methods are methods that are called on the class itself, rather than on an instance of the class.

```javascript
class MathOperations {
  static add(x, y) {
    return x + y;
  }

  static multiply(x, y) {
    return x * y;
  }
}

console.log(MathOperations.add(2, 3));       // Outputs: 5
console.log(MathOperations.multiply(4, 5));  // Outputs: 20
```

Static methods are useful for utility functions that are related to the class but don't depend on specific instance data.

## 2. Arrow Function
ES6 arrow functions provide a more concise syntax for writing function expressions in JavaScript. They are particularly useful for short and anonymous functions. 
Here are some key features of arrow functions:

### 1. Syntax:

The basic syntax of an arrow function is shorter than the traditional function expression:

```javascript
// ES5 function expression
var add = function(a, b) {
  return a + b;
};

// ES6 arrow function
const add = (a, b) => a + b;
```

### 2. Shorter Function Declaration:

Arrow functions eliminate the need for the `function` keyword and, in some cases, the need for curly braces `{}` and the `return` keyword. 
If the function body consists of a single expression, that expression is implicitly returned.

### 3. Lexical `this` Binding:

Arrow functions do not have their own `this` context; instead, they inherit the `this` value from the enclosing scope. This behavior can be beneficial in 
avoiding common pitfalls related to the `this` keyword.

```javascript
function Counter() {
  this.count = 0;

  // Without arrow function
  // this will refer to the object that calls the function, not the Counter instance
  // causing an error
  // setInterval(function() {
  //   this.count++;
  //   console.log(this.count);
  // }, 1000);

  // With arrow function
  // this refers to the Counter instance
  setInterval(() => {
    this.count++;
    console.log(this.count);
  }, 1000);
}

const counter = new Counter();
```

### 4. No Arguments Object:

Arrow functions do not have their own `arguments` object. If you need to access arguments, you can use the rest parameter syntax (`...args`).

```javascript
// ES5 function expression
var printArguments = function() {
  console.log(arguments);
};

// ES6 arrow function
const printArguments = (...args) => console.log(args);
```

### 5. Compact Syntax for Single-Parameter Functions:

For functions with a single parameter, you can omit the parentheses around the parameter.

```javascript
// ES6 arrow function with a single parameter
const square = x => x * x;
```

### 6. Concise Object Methods:

When defining methods within objects, arrow functions provide a more concise syntax.

```javascript
const person = {
  name: 'John',
  sayHello: () => {
    console.log(`Hello, ${this.name}`); // 'this' is lexically scoped to the outer context
  }
};

person.sayHello(); // Outputs: Hello, undefined
```

### 7. Use Cases:

Arrow functions are well-suited for short, non-method functions. However, they may not be suitable for all scenarios, such as when dealing with the `arguments` 
object or when defining object methods that require access to the instance via `this`.

## 3. let, const, and var
In ECMAScript 6 (ES6), three keywords are used for variable declaration: `var`, `let`, and `const`. These keywords have different behaviors regarding scoping rules, 
reassignment, and hoisting.

### 1. `var`:

- **Function-Scoped:** Variables declared with `var` are function-scoped, meaning their scope is limited to the function in which they are declared.
- **Hoisting:** Variables declared with `var` are hoisted to the top of their scope. This means you can use the variable before it's declared,
  but its value will be `undefined`.
- **Reassignment:** `var` allows reassignment and redeclaration within the same scope.

Example:

```javascript
function example() {
  if (true) {
    var x = 10;
    console.log(x); // Outputs: 10
  }
  console.log(x); // Outputs: 10
}

console.log(x); // Outputs: ReferenceError: x is not defined
```

### 2. `let`:

- **Block-Scoped:** Variables declared with `let` are block-scoped, meaning their scope is limited to the block (enclosed by curly braces) in which they are defined.
- **Hoisting:** Like `var`, variables declared with `let` are hoisted, but they are not initialized. Trying to access them before the
  declaration results in a `ReferenceError`.
- **Reassignment:** Variables declared with `let` can be reassigned but not redeclared within the same block.

Example:

```javascript
function example() {
  if (true) {
    let y = 20;
    console.log(y); // Outputs: 20
  }
  console.log(y); // Outputs: ReferenceError: y is not defined
}

console.log(y); // Outputs: ReferenceError: y is not defined
```

### 3. `const`:

- **Block-Scoped:** Like `let`, variables declared with `const` are block-scoped.
- **Hoisting:** `const` variables are also hoisted, but like `let`, they are not initialized.
- **Reassignment:** Variables declared with `const` cannot be reassigned after initialization. They must be assigned a value when declared,
  and this value cannot be changed.

Example:

```javascript
function example() {
  if (true) {
    const z = 30;
    console.log(z); // Outputs: 30
  }
  console.log(z); // Outputs: ReferenceError: z is not defined
}

console.log(z); // Outputs: ReferenceError: z is not defined
```

```javascript
const PI = 3.14;
PI = 3.1415; // Error: Assignment to a constant variable
```

### Key Takeaways:

- Use `var` when you need function-scoping or want to take advantage of hoisting.
- Prefer `let` when you need block-scoping and the ability to reassign variables.
- Use `const` when you need block-scoping and want to ensure that a variable is not reassigned after initialization.

## 4. Array Methods
ES6 introduced several new array methods that provide more concise and expressive ways to work with arrays in JavaScript. These methods make it easier to perform common 
operations such as iteration, filtering, mapping, and reducing. Here are some of the most commonly used array methods introduced in ES6:

### 1. `forEach`:

The `forEach` method iterates over the elements of an array and executes a provided function once for each element.

```javascript
const numbers = [1, 2, 3, 4];

numbers.forEach((number) => {
  console.log(number);
});
```

### 2. `map`:

The `map` method creates a new array by applying a function to each element in the existing array.

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map((number) => {
  return number * 2;
});

// doubled is now [2, 4, 6, 8]
```

### 3. `filter`:

The `filter` method creates a new array with elements that satisfy a provided condition.

```javascript
const numbers = [1, 2, 3, 4];

const evens = numbers.filter((number) => {
  return number % 2 === 0;
});

// evens is now [2, 4]
```

### 4. `find`:

The `find` method returns the first element in the array that satisfies a provided testing function.

```javascript
const numbers = [1, 2, 3, 4];

const found = numbers.find((number) => {
  return number > 2;
});

// found is now 3
```

### 5. `reduce`:

The `reduce` method applies a function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

```javascript
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce((accumulator, current) => {
  return accumulator + current;
}, 0);

// sum is now 10
```

### 6. `some` and `every`:

The `some` method tests whether at least one element in the array passes the provided function, while `every` tests whether all elements pass the provided function.

```javascript
const numbers = [1, 2, 3, 4];

const hasEven = numbers.some((number) => {
  return number % 2 === 0;
});

// hasEven is true

const allEven = numbers.every((number) => {
  return number % 2 === 0;
});

// allEven is false
```

### 7. `includes`:

The `includes` method checks if an array includes a specific element.

```javascript
const numbers = [1, 2, 3, 4];

const includesThree = numbers.includes(3);

// includesThree is true
```

### 8. `Array.from`:

The `Array.from` method creates a new, shallow-copied array instance from an array-like or iterable object.

```javascript
const iterable = 'hello';
const chars = Array.from(iterable);

// chars is now ['h', 'e', 'l', 'l', 'o']
```

## 5. Destructuring Assignment
Destructuring assignment is a feature introduced in ECMAScript 6 (ES6) that allows you to extract values from arrays or properties from objects and assign them to variables 
in a more concise and readable way. It simplifies the process of working with complex data structures. Destructuring assignment is commonly used with arrays and objects.

### 1. Array Destructuring:

#### Basic Example:

```javascript
// Before ES6
const numbers = [1, 2, 3];
const a = numbers[0];
const b = numbers[1];
const c = numbers[2];

// With ES6
const [a, b, c] = numbers;
```

#### Skipping Elements:

You can skip elements in the array by leaving empty slots in the destructuring pattern.

```javascript
const numbers = [1, 2, 3, 4, 5];
const [a, , c] = numbers; // a = 1, c = 3
```

#### Rest Operator:

The rest operator (`...`) gathers the remaining elements into a new array.

```javascript
const numbers = [1, 2, 3, 4, 5];
const [a, b, ...rest] = numbers; // a = 1, b = 2, rest = [3, 4, 5]
```

### 2. Object Destructuring:

#### Basic Example:

```javascript
// Before ES6
const person = { firstName: 'John', lastName: 'Doe' };
const firstName = person.firstName;
const lastName = person.lastName;

// With ES6
const { firstName, lastName } = person;
```

#### Changing Variable Names:

You can assign values to variables with different names.

```javascript
const person = { firstName: 'John', lastName: 'Doe' };
const { firstName: first, lastName: last } = person;
// first = 'John', last = 'Doe'
```

#### Default Values:

You can provide default values for properties that might be undefined.

```javascript
const person = { firstName: 'John' };
const { firstName, lastName = 'Doe' } = person;
// firstName = 'John', lastName = 'Doe'
```

#### Nested Destructuring:

You can destructure nested objects.

```javascript
const person = { name: { first: 'John', last: 'Doe' }, age: 30 };
const { name: { first, last }, age } = person;
// first = 'John', last = 'Doe', age = 30
```

### 3. Destructuring in Function Parameters:

Destructuring can also be used in function parameters.

```javascript
// Without destructuring
function printFullName(person) {
  console.log(`${person.firstName} ${person.lastName}`);
}

// With destructuring
function printFullName({ firstName, lastName }) {
  console.log(`${firstName} ${lastName}`);
}

const person = { firstName: 'John', lastName: 'Doe' };
printFullName(person); // Outputs: John Doe
```

## 7. Spread and Rest Operators
The spread (`...`) and rest (`...`) operators are both introduced in ECMAScript 6 (ES6) and provide powerful and flexible ways to work with arrays and function parameters.

### Spread Operator (`...`):

#### 1. Array Spread:

The spread operator allows you to expand an array into individual elements. It is often used to create a shallow copy of an array or to concatenate arrays.

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

const combined = [...arr1, ...arr2]; // Shallow copy and concatenation
// combined is now [1, 2, 3, 4, 5, 6]
```

#### 2. Object Spread:

Similarly, you can use the spread operator to shallow copy and merge objects.

```javascript
const obj1 = { a: 1, b: 2 };
const obj2 = { b: 3, c: 4 };

const merged = { ...obj1, ...obj2 }; // Shallow copy and merging
// merged is now { a: 1, b: 3, c: 4 }
```

### Rest Parameter (`...`):

The rest parameter is used in function parameters to collect the remaining arguments into a single array. It is the counterpart to the spread operator.

#### 1. Rest Parameter in Function Parameters:

```javascript
function sum(...numbers) {
  return numbers.reduce((acc, num) => acc + num, 0);
}

console.log(sum(1, 2, 3, 4)); // Outputs: 10
```

In this example, the `...numbers` syntax collects all the arguments passed to the `sum` function into an array called `numbers`.

#### 2. Destructuring with Rest:

The rest operator can also be used in destructuring to capture the remaining elements into a new array.

```javascript
const [first, second, ...rest] = [1, 2, 3, 4, 5];
// first = 1, second = 2, rest = [3, 4, 5]
```

### Combining Spread and Rest:

You can use both the spread and rest operators in a single operation.

```javascript
const [first, ...rest] = [1, 2, 3, 4, 5];
// first = 1, rest = [2, 3, 4, 5]
```

### Use Cases:

- **Spread Operator:**
  - Copying arrays or objects.
  - Concatenating arrays.
  - Passing elements of an array as individual arguments to a function.

- **Rest Parameter:**
  - Collecting function arguments into an array.
  - Capturing remaining elements during array destructuring.

### Important Note:

While the spread operator creates shallow copies, it does not perform deep cloning. This means that nested objects or arrays inside the spread may still reference 
the original objects. If deep cloning is required, additional steps or libraries like Lodash's `_.cloneDeep` may be necessary.

## 8. Modules
In ECMAScript (ES), modules are a way to organize and structure code by encapsulating it into smaller, reusable units. ES6 (ES2015) introduced a standardized module 
system, allowing developers to create modular code that can be easily shared and maintained. The module system provides a clean and efficient way to manage dependencies 
and promote code organization.

Here are some key aspects of modules in ES6:

### 1. **File-Based Modules:**
   - Each module typically corresponds to a single file. The contents of the file are considered the module's scope, and only the variables and functions
     explicitly exported are accessible from outside the module.

### 2. **Exporting and Importing:**
   - **Exporting:** In a module, you can use the `export` keyword to expose variables, functions, or classes to other modules.
     ```javascript
     // exampleModule.js
     export const PI = 3.14;
     export function square(x) {
       return x * x;
     }
     ```

   - **Importing:** In another module, you use the `import` statement to bring in the exported items.
     ```javascript
     // mainModule.js
     import { PI, square } from './exampleModule';
     console.log(PI);         // Outputs: 3.14
     console.log(square(2));  // Outputs: 4
     ```

### 3. **Default Export:**
   - A module can have a default export, which is the primary exported value or functionality. It is imported without using braces `{}`.
     ```javascript
     // exampleModule.js
     const defaultExport = 42;
     export default defaultExport;
     ```

     ```javascript
     // mainModule.js
     import myDefaultExport from './exampleModule';
     console.log(myDefaultExport);  // Outputs: 42
     ```

### 4. **Exporting All:**
   - You can use the `export *` syntax to export all items from one module into another.
     ```javascript
     // exampleModule.js
     const A = 10;
     const B = 20;
     export { A, B };
     ```

     ```javascript
     // mainModule.js
     import * as exampleModule from './exampleModule';
     console.log(exampleModule.A);  // Outputs: 10
     console.log(exampleModule.B);  // Outputs: 20
     ```

### 5. **Module Interoperability:**
   - ES6 modules work well with other module systems, but there are different syntaxes for CommonJS (`require`, `module.exports`) and AMD
     (Asynchronous Module Definition). Tools like Babel can be used to transpile code between different module formats.

### 6. **Static Structure:**
   - Module imports and exports are static, meaning they are resolved at compile-time rather than runtime. This allows tools to analyze and optimize the module structure.

### 7. **Top-Level Scope:**
   - Variables declared in a module are local to that module unless explicitly exported. They don't pollute the global scope.

### 8. **Circular Dependencies:**
   - ES6 modules handle circular dependencies more predictably compared to CommonJS modules.

### 9. **Browser and Node.js Support:**
   - ES6 modules are supported in modern browsers natively using `<script type="module">`. In Node.js, support for ES6 modules has been evolving, and you can
     use the `.mjs` extension or the `"type": "module"` field in `package.json` to enable ES6 modules.

## 9. Promises
Promises in ECMAScript 6 (ES6) are a powerful abstraction for handling asynchronous operations. They provide a clean and more readable way to work with 
asynchronous code compared to traditional callback-based approaches. A Promise represents the eventual completion or failure of an asynchronous operation and its 
resulting value.

### Basic Structure:

A Promise is an object that represents the eventual completion or failure of an asynchronous operation. It has three states:

1. **Pending:** The initial state; the promise is neither fulfilled nor rejected.
2. **Fulfilled:** The operation completed successfully, and the promise has a resulting value.
3. **Rejected:** The operation failed, and the promise has a reason for the failure.

### Creating a Promise:

A Promise is created using the `Promise` constructor, which takes a function (executor) with two parameters: `resolve` and `reject`. Inside this function, 
you perform your asynchronous operation, and when it's done, you call `resolve` with the result or `reject` with an error.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  const success = true;

  if (success) {
    resolve("Operation succeeded");
  } else {
    reject("Operation failed");
  }
});
```

### Consuming a Promise:

Once a Promise is created, you can use methods like `.then()` and `.catch()` to handle the fulfilled and rejected states.

```javascript
myPromise
  .then((result) => {
    console.log(result); // Outputs: Operation succeeded
  })
  .catch((error) => {
    console.error(error); // Outputs: Operation failed
  });
```

### Chaining Promises:

Promises can be chained using multiple `.then()` calls. Each `.then()` can return a new Promise, allowing for a sequence of asynchronous operations.

```javascript
const startOperation = new Promise((resolve) => {
  resolve("Initial data");
});

startOperation
  .then((data) => {
    console.log(data); // Outputs: Initial data
    return "Additional data";
  })
  .then((data) => {
    console.log(data); // Outputs: Additional data
  })
  .catch((error) => {
    console.error(error);
  });
```

### Promise.all and Promise.race:

- **Promise.all:** Combines multiple promises into a single promise that is fulfilled with an array of the results when all the input promises are fulfilled.

  ```javascript
  const promise1 = Promise.resolve(1);
  const promise2 = Promise.resolve(2);
  const promise3 = Promise.resolve(3);

  Promise.all([promise1, promise2, promise3])
    .then((values) => {
      console.log(values); // Outputs: [1, 2, 3]
    })
    .catch((error) => {
      console.error(error);
    });
  ```

- **Promise.race:** Returns a promise that fulfills or rejects as soon as one of the input promises fulfills or rejects.

  ```javascript
  const promise1 = new Promise((resolve) => setTimeout(() => resolve('Promise 1'), 1000));
  const promise2 = new Promise((resolve) => setTimeout(() => resolve('Promise 2'), 500));

  Promise.race([promise1, promise2])
    .then((value) => {
      console.log(value); // Outputs: Promise 2
    })
    .catch((error) => {
      console.error(error);
    });
  ```

### Async/Await:

ES2017 introduced `async` and `await`, which provide syntactic sugar for working with Promises. The `async` keyword is used to define an asynchronous function, 
and `await` is used to pause the execution of the function until the Promise is fulfilled.

```javascript
async function fetchData() {
  try {
    const result = await myPromise;
    console.log(result);
  } catch (error) {
    console.error(error);
  }
}

fetchData();
```

