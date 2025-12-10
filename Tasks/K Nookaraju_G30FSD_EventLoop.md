JavaScript Event Loop – Learning Summary (By  K nookaraju , G30 FSD)

1. What is the Event Loop?

The Event Loop is a system in JavaScript that decides what code runs first and what runs later.
Because JavaScript is single-threaded, it can run only one thing at a time, so Event Loop helps manage tasks without blocking the program.


---

2. Call Stack

This is where JavaScript executes code line by line.

It runs synchronous tasks (normal code).

If the stack is busy, nothing else happens.



---

3. Web APIs

These are features provided by the browser, like:

setTimeout

DOM events

fetch API

timers

network requests


They run outside the call stack.


---

4. Task Queue (Callback Queue)

Whenever a Web API finishes (like setTimeout), its callback goes here.

Tasks wait here until the Call Stack becomes empty.



---

5. Microtask Queue

This has higher priority than the Task Queue.

Things like:

Promise.then()

MutationObserver


Microtasks run before normal tasks.



---

6. Order of Execution (Very Important)

1. Call Stack runs synchronous code


2. Microtask Queue runs NEXT


3. Task Queue runs LAST



This is why Promises often run before setTimeout.


---

7. Why is this important?

Because it explains WHY JavaScript behaves unexpectedly sometimes,
Example:

console.log("1");
setTimeout(() => console.log("2"));
Promise.resolve().then(() => console.log("3"));
console.log("4");

Output will be:
1, 4, 3, 2

Because:

1,4 → synchronous

3 → microtask

2 → task queue



---

Final Understanding

The Event Loop keeps checking:
✔ Is the Call Stack empty?
→ If yes → Run all microtasks
→ Then run tasks from Task Queue

This helps JavaScript stay non-blocking and fast.
