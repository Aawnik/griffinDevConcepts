## Variables
- variables, containers to store the data values.
  - Declaration Keywords
    - `var`, Function-scoped, can be redeclared and updated. Hoisted with undefined.
    - `let`, Block-scoped, can be updated but not redeclared in the same scope.
    - `const`, Block-scoped, cannot be updated or redeclared. Must be initialized.
  - ### ArchitecturalBestPractice
    > - Use `const` by default, unless if needs reassignment use `let`
    > - Avoid `var` usless we are working with the legacy code.
    > - Using of meaningful variable names. Avoiding the use of any singleLetterNames.
## DataTypes
- js is dynamically typed, which means the variable types are determined at runtime.
  - Primitive(Immutable)
    - String, text data (e.g., "Hello")
    - Number, integers and floating points (e.g., 10, 3.14)
    - Boolean, true or false
    - Null, absence of value
    - Undefined, variable declared but not assigned a value
    - Symbol, unique identifiers
    - BigInt, integers beyond the `Number.MAX_SAFE_INTEGER`
  - NonPrimitive(Refrence)
    - Object, collections of key-value pairs
    - Array, ordered list of values
    - Function, callable objects
  - TypeChecking
    - `typeof` operator.
  - ### ArchitecturalBestPractice
    > - Using of strict equality `===` and `!==` to avoid any unexpected typeCoercion
    > - validate & sanitize data to avoid `undefined` or `null`.
    > - use of destructuring for cleaner access to object/array values.
    > - ```js
        > const [first, second] = arr;
        > const { name, age } = person;
    <!-- > - ``` -->
## Operators, Precedence\_&_Associativity
- operators,
  - Type Of Operators
    - Arthimetic\_\_ `+, -, *, /, %, **`
    - Assignment\_\_ `=, +=, -=`
    - Comparision\_\_ `==, !=, ===, !==, >, <`
    - Logical\_\_ `&&, ||, !`
    - Bitwise\_\_ `&, |, ^, ~, <<, >>, >>>`
    - Unary\_\_ `typeof, !, ++, --`
    - Ternary\_\_ `condition ? true : false`
  - Operator Precedence
    - Determines the order of operations
  - Associativity
    - Determines the order in which the operators of same precedence are evaluated.
      - Left-to-Right : a-b-c -> (a-b)-c
      - Right-to-Left : a=b=c -> a=(b=c)
  - ### ArchitecturalBestPractice
    > - Group expressions with parentheses when readability is low. Avoid overly complex ternary operations
    > - Be explicit with booleans in conditionals: if (value !== null && value !== undefined).

## conditional\_&_Loops
- conditional_&_loops, 
  - Conditional Loop
    - `if`, basic conditional logic
    - `if...else`, Executes only `if` the condition is true,
    - `else if`, Adds multiple conditions.
    - `switch`, Efficient alternative for `if-else`
        ```js
            if (score > 90) {
              console.log("Excellent");
            } else if (score > 70) {
              console.log("Good");
            } else {
              console.log("Try again");
            }
            
  - Loop
    - `for`, Traditional loop with the initializer, condition, increment
    - `while`, executes only if the 'while' condition is `true`
    - `do...while`, executes only once, then checks the condition.
    - `for...in`, iterates over the 'properties' of an Object
    - `for...of`, iterates over the iterable 'values' (arrays, strings)
  - ### ArchitecturalBestPractice
    > - ✅ Prefer array methods (map, filter, reduce) over for loops for declarative code.
    > - ✅ Avoid deeply nested if/else. Consider early returns or switch-case.
    > - ✅ Use for...of with arrays and for...in with objects appropriately.

## Functions
- functions are the resuable blocks of code.
  - Function Declaration
    ```js
        function greet(name) {
          return "Hello " + name;
        }
    ```
  - function Expression
    ```js
        const greet = function (name) {
          return "Hello " + name;
        };
    ```
  - Arrow Function
    ```js
        const greet = (name) => "Hello " + name;
    ```
  - ### ArchitecturalBestPractice
    - ✅ Use arrow functions for small callbacks or methods without this.
    - ✅ have small, single-purpose functions (SRP – Single Responsibility Principle).
    - ✅ Use default parameters:
        > ```js
        > function greet(name = "Guest") {
        >   return `Hello, ${name}`;
        >   }
        > ```
## Callback_&_Anonymous Function
- CallbackFunction, The func passed as an argument to another function, or to be executed later.
  - Syntax
    ```js
        function greet(name,callback){
            console.log(`Hello`,${name})
            callback()
        }
        function sayGoodBye(){
            console.log(`GoodBye..!`)
        }
        greet(`Aawni`, sayGoodBye)
    ```
- AnonymousFunction, 
  - The function without a name, which is often used as the callback or in IIFE.
  - useful, when the function's logic is short, selfContained and doesn't need to be referenced anywhere in the code.
  - IIFE, creates the private scope for var's preventing them from polluting the global scope.
  - Syntax
    ```js
        // As a callback
        setTimeout(function(){
            console.log(`This gets executed after every 2 seconds`)
        },1000)
        // IIFE, Immediately invoked function Expression.
        (function(){
            console.log(`IIFE...!`)
        })();
  - ### ArchitecturalBestPractice
    - ✅ Use descriptive names for callback functions where possible to improve code readability, especially for complex operations.
    - ✅ Avoid deeply nested callbacks (callback hell) by using Promises, async/await, or event emitters for asynchronous operations.
## Scope
- Scope, 
  - GlobalScope
    - Variables declared outside of any function, can be accessed from anywhere in the code.
    - Working
      - When JS engine starts, it creates the GlobalExecutionContext. 
      - `windows` in browser, `global` in NodeJS
  - Function/LocalScope
    - Varibales declared inside the function, accessed only within the function
    - Working
      - Each time is called, the new functional ExecutionContext is created.
      - Variables declared with `var`,`let`,`const` inside the function are part of the same "variableEnviornment" and can be accessed only within the function's boundaries. 
  - BlockScope
    - Variables declared with `let` or `const` within the `{}`. can accessed within that block.
    - Working
      - introduced in ES_6, `blockScope` means the variables are limited to the nearest enclosing curly braces.
      - Which prevents the variable leakage and 
      - makes the code more predictable.
      - **var**, doesn't works with the blockScope.
  - LexicalScope
    - the function's ability to remember and access the variables from its outer scope even after it finished its execution.
    ```js
        function outerFunc(outerVar){
        return function innerFunc(innerVar){
        console.log(`Outer ${outerVar}, ${innerVar}`)
            }
        }
        const closure = outerFunc(`Hello...,`)
        closure(`welcome to my World..!`)
    ```
  - ### ArchitecturalBestPractice
    - ✅ Minimize the use of global variables to prevent naming conflicts and unintended side effects.
    - ✅ Prefer const over let when a variable's value will not be reassigned, and let over var for block-scoping.
    - ✅ Leverage closures intentionally to create private variables and maintain state within functions, rather than relying on global scope.

## JavaScript Objects : Methods_&_Properties
- Properties
  - Objects, key-value pairs which describes the object's characteristics.
    - Working
      - Objects are the collection of properties. 
      - which each property consists of a name (a string or symbol) and a value (any js data type, objects or functions).
    ```js
        const car = {
            make:"mahindra", 
            model:"Thar", 
            year:2024
        }
        console.log(car.make)     //Access using dot notation
        console.log(car['model'])     // Access using bracket notation
    ```
- Methods
  - Functions stored as object properties, representing the actions that the object can perform.
  - Working
    - When a function is assigned as a property of an object, it becomes a method. 
    - Inside a method, `this` refers to the object on which the method was called, allowing it to access other properties of that object.
    ```js
        const person = {
          name:"Aawni", 
          age:30, 
          greet:function(){
            console.log(`Hello..! my name is ${this.name}`)
            }
          }
        person.greet();
    ```

  - `Object.keys()`
    - Returns an array of the given object's own enum property **key** names.
    - Syntax : `Object.keys(car);`    // ["make","model","year"]
    - Working
      - Iterates over object's own properties where the `enum` attribute is set to "true" and collects their string names to new Array.
  - `Object.values()`: 
    - Returns an array of a given object's own enumerable property **values**.
    - Syntax: Object.values(car); // ['Mahindra', 'Thar', 2024]
    - Working: Similar to Object.keys(), but collects the **values** associated with the enum properties.
  - `Object.entries()`: 
    - Returns an array of a given object's own enum string-keyed property **[key, value]** pairs.
    - Syntax: Object.entries(car); // [['make', 'Mahindra'], ['model', 'Thar'], ['year', 2024]]
    - Working: Combines the functionality of keys and values into an array of **[key, value]** arrays, useful for iterating or converting objects to maps.
  - `hasOwnProperty()`: 
    - Returns a boolean, checks if the object has the specified property as its own (not inherited).
    - Syntax:
    ```js
        car.hasOwnProperty('make')  //true
        car.hasOwnProperty('toString')   //false
    ```
    - Working
      - This method is available on all objects through the prototype chain.
      - where it checks if the property directly exists on the object itself, without looking up the prototype chain.
  - ### ArchitecturalBestPractice
    - ✅ Prefer using `Object.freeze()` or `Object.seal()` to prevent modifications to objects when immutability is desired.
    - ✅ Use property shorthand `({ a, b })` and computed property names `([expression])` for cleaner object creation.
## Array Method_&_Properties
- Properties
  - **`length`**: 
    - Property that returns the number of elements in an array.
    - Syntax : [1, 2, 3].length; // 3
    - Working: A mutable property that dynamically reflects the highest index plus one. Changing length can truncate or expand an array.
  - **`push() / pop()`**:
    - Add/remove elements from the end.
    - Syntax:
    ```js
        let arr = [1, 2];
        arr.push(3);    // arr is now [1, 2, 3]
        arr.pop();      // arr is now [1, 2], returns 3
    ```
    - Working: Both are O(1) operations (constant time) as they only modify the end of the array, requiring no re-indexing of other elements. 
      - push returns the new length, 
      - pop returns the removed element.
  - **`shift() / unshift()`**:
    - Add/remove elements from the beginning.
    - Syntax:
    ```js
        let arr = [1, 2];
        arr.unshift(0); // arr is now [0, 1, 2]
        arr.shift();    // arr is now [1, 2], returns 0
    ```
    - Working: Both are O(n) operations (linear time) because adding or removing an element from the beginning requires all subsequent elements to be re-indexed.
      - unshift returns the new length, 
      - shift returns the removed element.
  - **`splice()`**: 
    - Changes array contents by removing/replacing/adding elements.
    - Syntax:
    ```js
        let arr = [1, 2, 3, 4, 5];
        arr.splice(2, 1, 'a', 'b'); // From index 2, remove 1 element, add 'a', 'b'
        // arr is now [1, 2, 'a', 'b', 4, 5], returns [3] (removed elements)
    ```
    - Working: 
      - It takes a starting index, a number of elements to delete, and then any number of elements to add. 
      - Elements might need to be re-indexed depending on insertions/deletions.
  - **`slice()`**:
    - Returns a shallow copy of a portion of an array.
    - Syntax:
    ```js
        let arr = [1, 2, 3, 4, 5];
        let newArr = arr.slice(1, 4); // newArr is [2, 3, 4], arr is unchanged
    ```
    - Working: 
      - Creates a new array, containing elements from the original array from the start index (inclusive) up to the end index (exclusive.
      - Original array is not modified.
  - **`shift() / unshift()**`: 
    - Add/remove elements from the beginning.
    - Syntax:
    ```js
        let arr = [1, 2];
        arr.unshift(0); // arr is now [0, 1, 2]
        arr.shift();    // arr is now [1, 2], returns 0
    ```
    - Working: 
      - Both are O(n) operations (linear time) because adding or removing an element from the beginning requires all subsequent elements to be re-indexed.
      - unshift returns the new length,
      - shift returns the removed element.
  - **`splice()`**:
    - Changes array contents by removing/replacing/adding elements.
    - Syntax:
    ```js
        let arr = [1, 2, 3, 4, 5];
        arr.splice(2, 1, 'a', 'b'); // From index 2, remove 1 element, add 'a', 'b'
        // arr is now [1, 2, 'a', 'b', 4, 5], returns [3] (removed elements)
    ```
    - Working:
      - A highly versatile mutable method. It takes a starting index, a number of elements to delete, and then any number of elements to add. Elements might need to be re-indexed depending on insertions/deletions.
  - **`slice()`**:
    - Returns a shallow copy of a portion of an array.
    - Syntax:
    ```js
        let arr = [1, 2, 3, 4, 5];
        let newArr = arr.slice(1, 4); // newArr is [2, 3, 4], arr is unchanged
    ```
    - Working: Creates a new array, containing elements from the original array from the start index (inclusive) up to the end index (exclusive). Original array is not modified.
  - **`concat()`:** 
    - Merges two or more arrays.
    - Syntax:
    ```js
        let arr1 = [1, 2];
        let arr2 = [3, 4];
        let combined = arr1.concat(arr2); // combined is [1, 2, 3, 4]
        // Using spread operator (more modern):
        let spreadCombined = [...arr1, ...arr2]; // [1, 2, 3, 4]
    ```
    - Working: Creates a new array by joining arrays or values. It does not modify the original arrays.
  - **`indexOf()`:**
    - Returns the first index of an element, or -1.
    - Syntax: [1, 2, 3, 2].indexOf(2); // 1
    - Working: Performs a strict equality comparison (===) for each element until a match is found, returning its index.
  - **`forEach()`: **
    - Executes a provided function once for each element.
    - Syntax:
    ```js
        let arr = [1, 2, 3];
        arr.forEach(function(item) {
            console.log(item * 2);
        }); // Outputs 2, 4, 6
    ```
    - Working: Iterates over each element, calling the callback function. It does not return a new array; it's used for side effects.
  - **`map()`:**
    - Creates a new array with results of calling a function on every element.
    - Syntax:
    ```js
        let arr = [1, 2, 3];
        let doubled = arr.map(item => item * 2); // doubled is [2, 4, 6]
    ```
    Working: Creates a new array of the same length, where each element is the result of applying the callback function to the corresponding element in the original array.
  - **`filter()`: **
    - Creates a new array with all elements that pass a test.
    - Syntax:
    ```js
        let arr = [1, 2, 3, 4];
        let evens = arr.filter(item => item % 2 === 0); // evens is [2, 4]
    ```
    - Working: Creates a new array containing only the elements for which the callback function returns a truthy value.
  - **`reduce()`:** 
    - Executes a reducer function on each element, resulting in a single output value.
    - Syntax:
    ```js
        let arr = [1, 2, 3, 4];
        let sum = arr.reduce((accumulator, currentValue) => accumulator + currentValue, 0); // sum is 10
    ```
    - Working: Iterates through the array, applying a callback function that takes an accumulator (the result of the previous iteration) and the currentValue. It returns a single value at the end. An initial value for the accumulator can be provided.
  - **`find()`: **
    - Returns the value of the first element that satisfies a test.
    - Syntax : [1, 2, 3, 4].find(item => item > 2); // 3
    - Working: Iterates and returns the value of the first element for which the callback returns true. If no element passes the test, undefined is returned.
  - **`some()`**
    - Tests if at least one element passes a test.
    - Syntax : [1, 2, 3].some(item => item > 2); // true
    - Working: Returns true as soon as the callback returns a truthy value for any element. If no element passes, it returns false.
  - **`every()`:**
    - Tests if all elements pass a test.
    - Syntax : [1, 2, 3].every(item => item > 0); // true
    - Working: Returns true only if the callback returns a truthy value for all elements. If any element fails the test, it immediately returns false.: Merges two or more arrays.
    - Syntax :
      ```js
          let arr1 = [1, 2];
          let arr2 = [3, 4];
          let combined = arr1.concat(arr2); // combined is [1, 2, 3, 4]
          // Using spread operator (more modern):
          let spreadCombined = [...arr1, ...arr2]; // [1, 2, 3, 4]
      ```
    - Working: Creates a new array by joining arrays or values. It does not modify the original arrays.
  - **`indexOf()`:**
    - Returns the first index of an element, or -1.
    - Syntax : [1, 2, 3, 2].indexOf(2); // 1
    - Working: Performs a strict equality comparison (===) for each element until a match is found, returning its index.
  - **`forEach()`**: 
    - Executes a provided function once for each element.
    - Syntax :
    ```js
        let arr = [1, 2, 3];
        arr.forEach(function(item) {
            console.log(item * 2);
        }); // Outputs 2, 4, 6
    ```
    - Working: Iterates over each element, calling the callback function. It does not return a new array; it's used for side effects.
  - **`map()`**:
    - Creates a new array with results of calling a function on every element.
    - Syntax :
    ```js
        let arr = [1, 2, 3];
        let doubled = arr.map(item => item * 2); // doubled is [2, 4, 6]
    ```
    - Working: Creates a new array of the same length, where each element is the result of applying the callback function to the corresponding element in the original array.
  - **`filter()`**:
    - Creates a new array with all elements that pass a test.
    - Syntax :
    ```js
        let arr = [1, 2, 3, 4];
        let evens = arr.filter(item => item % 2 === 0); // evens is [2, 4]
    ```
    - Working: Creates a new array containing only the elements for which the callback function returns a truthy value.
  - **`reduce()`**:
    - Executes a reducer function on each element, resulting in a single output value.
    - Syntax :
    ```js
        let arr = [1, 2, 3, 4];
        let sum = arr.reduce((accumulator, currentValue) => accumulator + currentValue, 0); // sum is 10
    ```
    - Working: Iterates through the array, applying a callback function that takes an accumulator (the result of the previous iteration) and the currentValue. It returns a single value at the end. An initial value for the accumulator can be provided.
  - **`find()`**:
    - Returns the value of the first element that satisfies a test.
    - Syntax : [1, 2, 3, 4].find(item => item > 2); // 3
    - Working: Iterates and returns the value of the first element for which the callback returns true. If no element passes the test, undefined is returned.
  - **`some()`**:
    - Tests if at least one element passes a test.
    - Syntax : [1, 2, 3].some(item => item > 2); // true
    - Working: Returns true as soon as the callback returns a truthy value for any element. If no element passes, it returns false.
  - **`every()`**:
    - Tests if all elements pass a test.
    - Syntax : [1, 2, 3].every(item => item > 0); // true
    - Working: Returns true only if the callback returns a truthy value for all elements. If any element fails the test, it immediately returns false.
  - ### ArchitecturalBestPractice
    - ✅ Prefer **immutable array methods** (map, filter, slice, concat, spread operator) over mutable ones (push, pop, splice, sort) to avoid side effects and make code more predictable, especially in state management.
    - ✅ Choose the most semantically appropriate array method for the task (e.g., 
      - map for transformation, 
      - filter for selection, 
      - reduce for aggregation).


