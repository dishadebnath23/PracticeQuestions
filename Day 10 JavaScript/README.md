Practice Questions – Day 10  
JavaScript

------------------------------------------------------------

Q1. What is the difference between var, let, and const in JavaScript?

var:
- Function scoped
- Can be redeclared and reassigned
- Hoisted with undefined value

let:
- Block scoped
- Cannot be redeclared
- Can be reassigned

const:
- Block scoped
- Cannot be redeclared or reassigned
- Must be initialized at declaration

------------------------------------------------------------

Follow-up: What is block scope vs function scope?

Block scope:
- Variable exists only inside `{ }`
- Used by let and const

Function scope:
- Variable exists inside the entire function
- Used by var

------------------------------------------------------------

Follow-up: Why is const preferred in modern JavaScript?

const is preferred because:
- Prevents accidental reassignment
- Makes code more predictable
- Improves readability and safety

------------------------------------------------------------

Follow-up: Can a const object be modified? Why?

Yes, a const object can be modified.

Reason:
- const prevents reassignment of the reference
- It does not make the object immutable

Example:
- Object properties can be updated
- But the object itself cannot be reassigned

============================================================

Q2. Explain closures in JavaScript.  
Where are they used in real applications?

A closure is created when:
- An inner function remembers variables from its outer function
- Even after the outer function has finished execution

Closures allow functions to access outer scope variables later.

------------------------------------------------------------

Follow-up: Give a simple real-world example of a closure

Example use case:
- Counter function
- Private variables
- Maintaining state in functions

A function remembers the previous value without using global variables.

------------------------------------------------------------

Follow-up: How do closures help in data encapsulation?

Closures:
- Hide variables from global scope
- Allow controlled access to data
- Act like private variables

This helps in writing secure and clean code.

------------------------------------------------------------

Follow-up: Can closures cause memory issues? How?

Yes, closures can cause memory issues if:
- Large objects are captured unnecessarily
- References are not released

This may lead to memory leaks if not handled properly.

============================================================

Q3. What is the difference between synchronous and asynchronous JavaScript?

Synchronous JavaScript:
- Executes code line by line
- Blocks execution until task completes

Asynchronous JavaScript:
- Non-blocking
- Long-running tasks run in background
- Improves performance and responsiveness

------------------------------------------------------------

Follow-up: How does the JavaScript event loop work?

Event loop:
- Executes synchronous code first
- Then checks callback queue
- Pushes async callbacks to call stack when stack is empty

This enables non-blocking behavior in JavaScript.

------------------------------------------------------------

Follow-up: What are callbacks, promises, and async/await?

Callbacks:
- Functions passed as arguments
- Can lead to callback hell

Promises:
- Handle async operations
- Have states: pending, fulfilled, rejected

async/await:
- Syntactic sugar over promises
- Makes async code look synchronous

------------------------------------------------------------

Follow-up: Why is async/await preferred over callbacks?

async/await is preferred because:
- Code is cleaner and readable
- Easier error handling using try-catch
- Avoids callback nesting

============================================================

Q4. What ES6 features do you commonly use in your projects?

Common ES6 features:
- let and const
- Arrow functions
- Destructuring
- Spread operator
- Template literals
- Modules (import/export)

------------------------------------------------------------

Follow-up: Explain arrow functions and how this behaves in them

Arrow functions:
- Shorter syntax
- Do not have their own this
- Inherit this from surrounding scope

This avoids common this-related bugs.

------------------------------------------------------------

Follow-up: What is destructuring and where is it useful?

Destructuring:
- Extract values from arrays or objects
- Assign them to variables easily

Useful when:
- Handling API responses
- Accessing object properties cleanly

------------------------------------------------------------

Follow-up: What is the spread operator? Give a use case

Spread operator (...):
- Expands elements of array or object

Use cases:
- Copying arrays or objects
- Merging arrays
- Passing arguments to functions

============================================================

Q5. What is the difference between == and === in JavaScript?

== (Loose equality):
- Compares values after type conversion

=== (Strict equality):
- Compares value and type
- No type coercion

------------------------------------------------------------

Follow-up: Why is === preferred?

=== is preferred because:
- Avoids unexpected type conversion
- Makes comparisons more predictable

------------------------------------------------------------

Follow-up: What is type coercion? Give an example

Type coercion:
- Automatic conversion of one data type to another

Example:
- "5" == 5 → true
- "5" === 5 → false

------------------------------------------------------------

Follow-up: Can null == undefined be true? Why?

Yes, null == undefined is true.

Reason:
- JavaScript treats them as loosely equal
- But they are not strictly equal

Example:
- null === undefined → false

------------------------------------------------------------
