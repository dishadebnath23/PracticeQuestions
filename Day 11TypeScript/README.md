Practice Questions – Day 11  
TypeScript

------------------------------------------------------------

Q1. What is TypeScript, and why is it used instead of plain JavaScript?

TypeScript is a **superset of JavaScript** that adds **static typing** to the language.  
It helps developers catch errors at compile time instead of runtime.

TypeScript is used instead of plain JavaScript because:
- It provides type safety
- Code is more readable and predictable
- Better support for large-scale applications
- Strong IDE support like auto-completion and refactoring

------------------------------------------------------------

Follow-up: How does TypeScript improve code maintainability?

TypeScript improves maintainability by:
- Making code self-documenting using types
- Catching errors early
- Making refactoring safer
- Improving team collaboration in large projects

------------------------------------------------------------

Follow-up: Is TypeScript compiled or interpreted?

TypeScript is **compiled**.

It is compiled into JavaScript using the TypeScript compiler (`tsc`) before execution.

------------------------------------------------------------

Follow-up: Can a browser run TypeScript directly?

No, browsers cannot run TypeScript directly.

Browsers only understand JavaScript, so TypeScript must be converted to JavaScript first.

============================================================

Q2. Explain types in TypeScript.  
What are any, unknown, and never?

TypeScript provides static types to define what kind of values a variable can hold.

any:
- Disables type checking
- Acts like plain JavaScript

unknown:
- Safer alternative to any
- Type checking is required before usage

never:
- Represents values that never occur
- Used for functions that never return

------------------------------------------------------------

Follow-up: Why should any be avoided?

any should be avoided because:
- It removes all type safety
- Errors move to runtime
- Defeats the purpose of using TypeScript

------------------------------------------------------------

Follow-up: When would you use unknown?

unknown is used when:
- Type of data is not known at compile time
- Data comes from external sources like APIs
- Type checking will be done before use

------------------------------------------------------------

Follow-up: What does never represent in a function?

never represents:
- A function that never finishes execution
- Functions that throw errors or run infinite loops

============================================================

Q3. What are interfaces in TypeScript, and how are they different from classes?

Interfaces:
- Define the structure of an object
- Contain only method and property declarations
- Do not have implementation

Classes:
- Provide implementation
- Can have constructors and methods
- Can be instantiated

------------------------------------------------------------

Follow-up: Can an interface be extended?

Yes, an interface can extend:
- Another interface
- Multiple interfaces

This helps in reusability.

------------------------------------------------------------

Follow-up: Can a class implement multiple interfaces?

Yes, a class can implement multiple interfaces.

This allows:
- Multiple behaviors
- Better abstraction

------------------------------------------------------------

Follow-up: Why are interfaces useful in large applications?

Interfaces are useful because:
- They enforce consistent structure
- Improve readability
- Help teams work independently
- Make code scalable and maintainable

============================================================

Q4. How do you handle errors in JavaScript and TypeScript applications?

Errors are handled using:
- try–catch blocks
- Promise error handling
- Global error handlers

TypeScript helps reduce errors before runtime.

------------------------------------------------------------

Follow-up: What is try–catch?

try–catch:
- Used to handle runtime errors
- try contains risky code
- catch handles exceptions

------------------------------------------------------------

Follow-up: How are promise rejections handled?

Promise rejections are handled using:
- `.catch()` method
- try–catch with async/await

------------------------------------------------------------

Follow-up: How does TypeScript help in reducing runtime errors?

TypeScript helps by:
- Catching type-related issues at compile time
- Preventing invalid assignments
- Improving code correctness

============================================================

Q5. What are modules in JavaScript/TypeScript, and why are they important?

Modules:
- Allow code to be split into reusable files
- Help organize large codebases
- Prevent global scope pollution

------------------------------------------------------------

Follow-up: Difference between import/export and require

import/export:
- ES6 module syntax
- Static and recommended

require:
- CommonJS syntax
- Mostly used in older Node.js projects

------------------------------------------------------------

Follow-up: What is a default export?

Default export:
- Allows exporting a single main value
- Imported without curly braces

------------------------------------------------------------

Follow-up: How do modules help with scalability?

Modules help scalability by:
- Improving code organization
- Allowing independent development
- Making maintenance easier

------------------------------------------------------------
