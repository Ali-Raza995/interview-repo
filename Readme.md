

Core JavaScript Concepts

1. var vs let vs const

var:

Function-scoped.

Hoisted and initialized as undefined.

Can be re-declared and updated.

let:

Block-scoped.

Hoisted but in the Temporal Dead Zone (TDZ).

Cannot be re-declared in the same scope but can be updated.

const:

Block-scoped.

Must be initialized at declaration.

Cannot be re-declared or reassigned.

2. Hoisting

Hoisting is JavaScript's default behavior of moving declarations to the top of the scope. Only declarations are hoisted, not initializations.

console.log(a); // undefined
var a = 5;

3. == vs ===

== (loose equality): performs type coercion before comparison.

=== (strict equality): compares both value and type.

4. Closures

A closure is formed when an inner function retains access to variables in its outer (enclosing) function even after the outer function has completed execution.

function outer() {
  let counter = 0;
  return function inner() {
    return ++counter;
  };
}

5. Promises vs Callbacks

Callbacks: functions passed as arguments for asynchronous operations.

Promises: objects representing eventual completion or failure of an asynchronous task.

fetch(url)
  .then(response => response.json())
  .catch(error => console.error(error));

6. Event Bubbling

Events propagate from the innermost target to the outer elements. You can stop this behavior with event.stopPropagation().

7. null vs undefined

undefined: variable declared but not assigned a value.

null: explicitly set to indicate no value.

8. this Keyword

In global context: refers to window (non-strict) or undefined (strict mode).

In methods: refers to the object.

In arrow functions: inherits this from the lexical context.

9. Synchronous vs Asynchronous

Synchronous: Executes line-by-line, blocking the next line.

Asynchronous: Non-blocking, executes tasks in the background (e.g., setTimeout, Promises).

10. Event Loop

JavaScript's concurrency model is designed to handle asynchronous operations in a single-threaded environment. It consists of:

Call Stack: The stack that keeps track of currently executing functions.

Web APIs: Browser-provided APIs like setTimeout, DOM events, fetch, etc. When an async operation is invoked, it’s handed off to these APIs.

Callback Queue (Macrotask Queue): Queues macrotasks like setTimeout, setInterval, etc.

Microtask Queue: Queues microtasks like Promise.then, MutationObserver, etc.

Execution Order:

JavaScript runs code in the call stack.

When an async task (like a setTimeout) completes, the callback is sent to the callback queue.

Meanwhile, microtasks from resolved Promises go to the microtask queue.

Before moving to the next macrotask, the event loop empties the microtask queue first.

Example:

console.log("Start");

setTimeout(() => console.log("Macrotask: Timeout"), 0);

Promise.resolve().then(() => console.log("Microtask: Promise"));

console.log("End");

Output:

Start
End
Microtask: Promise
Macrotask: Timeout

Advanced / Tricky Concepts

1. Weird Outputs

console.log([] + {}); // "[object Object]"
console.log({} + []); // 0 or "[object Object]" (depends on context)

2. Currying

Converting a function with multiple parameters into a sequence of functions each taking a single parameter.

const add = a => b => a + b;

3. Debounce vs Throttle

Debounce: waits for the user to stop triggering the event for a defined time.

Throttle: ensures the function is called at most once in a specified interval.

4. IIFE

Immediately Invoked Function Expression executes as soon as it is defined.

(function() {
  console.log("I run instantly");
})();

5. Temporal Dead Zone (TDZ)

The time between variable hoisting and initialization where accessing the variable throws a ReferenceError.

6. .call(), .apply(), .bind()

call: calls a function with a given this and arguments.

apply: same as call, but arguments passed as an array.

bind: returns a new function with this bound.

7. Garbage Collection

JavaScript automatically frees memory when objects are no longer reachable or referenced.

8. Prototypal Inheritance

Objects inherit from other objects via the [[Prototype]] or __proto__ chain.

9. Generators

Generator functions yield values one at a time and maintain their state between yields.

function* gen() {
  yield 1;
  yield 2;
}

10. Shallow vs Deep Copy

Shallow Copy: only top-level properties are copied.

Deep Copy: nested properties are copied too.

ES6+ Features

1. Arrow Functions

Shorter syntax and this is lexically bound.

2. Destructuring

Extract values from arrays or properties from objects.

const [a, b] = [1, 2];
const { name } = { name: "John" };

3. Spread vs Rest

Spread: expands elements.

Rest: collects remaining elements.

4. Template Literals

Allows embedding expressions.

const name = "Alex";
console.log(`Hi ${name}`);

5. Map vs Object

Map: any key type, remembers insertion order.

Object: string/symbol keys only.

6. Async/Await

Syntactic sugar for Promises. Cleaner async code.

async function getData() {
  const res = await fetch(url);
  return await res.json();
}

7. Modules

Support for importing/exporting files.

// module.js
export const greet = () => "Hello";

// main.js
import { greet } from './module.js';

Browser/DOM Concepts

1. DOM

The Document Object Model represents HTML as a tree structure that can be modified via JavaScript.

2. getElementById vs querySelector

getElementById: selects element by ID.

querySelector: supports full CSS selectors.

3. localStorage vs sessionStorage

localStorage: persists until explicitly cleared.

sessionStorage: cleared when the tab is closed.

4. preventDefault vs stopPropagation

preventDefault: stops default browser behavior.

stopPropagation: prevents event from bubbling up.

5. Global Error Handling

window.onerror = (msg, src, line, col, err) => {
  console.error("Error caught globally", err);
};

window.addEventListener("unhandledrejection", event => {
  console.error("Unhandled promise rejection", event.reason);
});

