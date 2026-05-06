---
tags: []
date: 2026-05-05
time: 16:20
---

# JavaScript Mock Test (Questions)

> Based on the IKM JAVASCRIPT (ECMAScript 2019 / ES10) Secure Evaluation Mode spec — 42 single-choice questions (4 options each).
> Strictly scoped to ES2019 (ECMA-262, 10th edition) and earlier. No features from ES2020+ (no `??`, no optional chaining, no `Promise.allSettled`, no private class fields, no dynamic `import()`, no `String.prototype.replaceAll`, no `String.prototype.matchAll`).
> Sub-topics: Arrays, Defining Custom Objects, Standard Functions, Flow Control, Operators and Expressions, String Handling, Variables and Syntax, Classes, Keyed Collections, Arrow Functions, JavaScript Modules, Iteration Functions, Scope/Hoisting/Closures, Promises.

---

## 1. Arrays

### Q1. What does the following code output?
```javascript
const arr = [1, 2, 3, 4, 5];
const result = arr.flatMap(x => x % 2 === 0 ? [] : [x, x * 2]);
console.log(result);
```
- A. `[1, 2, 3, 6, 5, 10]`
- B. `[1, 2, 2, 4, 3, 6, 4, 8, 5, 10]`
- C. `[1, 3, 5, 2, 6, 10]`
- D. `[2, 6, 10]`

---

### Q2. Which statement about `Array.prototype.sort()` after ES2019 is **correct**?
- A. The result is unstable across all engines
- B. ES2019 requires `sort` to be a stable sort
- C. `sort` orders by numeric value by default
- D. `sort` does not mutate the original array

---

### Q3. What does the following code output?
```javascript
const arr = [1, 2, 3];
arr.length = 5;
console.log(arr[3], arr.length, arr.includes(undefined));
```
- A. `undefined 5 true`
- B. `undefined 3 false`
- C. `null 5 false`
- D. `undefined 5 false`

---

## 2. Defining Custom Objects

### Q4. What does the following code output?
```javascript
function Animal(name) {
  this.name = name;
}
Animal.prototype.greet = function() {
  return `Hello, ${this.name}`;
};

const a = new Animal('Leo');
const b = Object.create(Animal.prototype);
b.name = 'Mia';

console.log(a.greet(), b.greet(), a.__proto__ === b.__proto__);
```
- A. `Hello, Leo Hello, Mia true`
- B. `Hello, Leo Hello, Mia false`
- C. `Hello, Leo TypeError`
- D. `Hello, undefined Hello, Mia true`

---

### Q5. What is the result of the `Object.defineProperty` call below?
```javascript
const obj = {};
Object.defineProperty(obj, 'x', { value: 1 });
obj.x = 99;
console.log(obj.x);
```
- A. `99`
- B. `1`
- C. `undefined`
- D. Throws `TypeError`

---

### Q6. Which statement most precisely describes prototypal inheritance in JavaScript?
- A. An object copies all properties from its parent to form its own duplicate
- B. An object holds an internal `[[Prototype]]` link to another object; property lookups walk up the chain
- C. The child and parent objects share the same memory address
- D. JavaScript has no prototypal inheritance — only classical inheritance

---

## 3. Standard Functions

### Q7. What does the following code output?
```javascript
function fn(a, b = 10, c) {
  return a + b + c;
}
console.log(fn(1, undefined, 3));
console.log(fn(1, null, 3));
```
- A. `14 NaN`
- B. `14 4`
- C. `4 4`
- D. `NaN NaN`

---

### Q8. Which of the following is **not** a property of "first-class functions" in JavaScript?
- A. Functions can be assigned to variables
- B. Functions can be passed as arguments
- C. Functions can be returned from other functions
- D. Functions cannot have their own properties

---

### Q9. What does the following code output?
```javascript
function sum() {
  return [...arguments].reduce((a, b) => a + b, 0);
}
const arrow = () => [...arguments].reduce((a, b) => a + b, 0);

console.log(sum(1, 2, 3));
try {
  console.log(arrow(1, 2, 3));
} catch (e) {
  console.log(e.constructor.name);
}
```
- A. `6 6`
- B. `6 ReferenceError`
- C. `6 TypeError`
- D. `[1,2,3] 6`

---

## 4. JavaScript Flow Control

### Q10. What does the following code output?
```javascript
const obj = { a: 1, b: 2, c: 3 };
let result = '';
for (const key in obj) {
  result += key;
}
for (const val of Object.values(obj)) {
  result += val;
}
console.log(result);
```
- A. `abc123`
- B. `123abc`
- C. `a1b2c3`
- D. `abcabc`

---

### Q11. What does the following `switch` print?
```javascript
const x = '1';
switch (x) {
  case 1:
    console.log('number');
    break;
  case '1':
    console.log('string');
    break;
  default:
    console.log('default');
}
```
- A. `number`
- B. `string`
- C. `default`
- D. Both `number` and `string`

---

### Q12. How many times will the loop print "tick"?
```javascript
let i = 0;
while (i < 5) {
  if (i === 2) {
    i++;
    continue;
  }
  console.log('tick');
  i++;
}
```
- A. 3
- B. 4
- C. 5
- D. Infinite loop

---

## 5. Operators and Expressions

### Q13. What is the result of the following expressions?
```javascript
console.log([] + []);
console.log([] + {});
console.log({} + []);
```
(Assume each line is evaluated as an expression, not interpreted at statement level where `{}` could be parsed as a block.)
- A. `'' '[object Object]' '[object Object]'`
- B. `0 NaN NaN`
- C. `'' '[object Object]' '0'`
- D. `[] [] []`

---

### Q14. Which expression evaluates to `true`?
- A. `0.1 + 0.2 === 0.3`
- B. `NaN === NaN`
- C. `Object.is(NaN, NaN)`
- D. `[] === []`

---

### Q15. What does the following code output?
```javascript
try {
  JSON.parse('{ invalid json }');
} catch {
  console.log('caught without binding');
}

try {
  throw new Error('boom');
} catch (e) {
  console.log('caught:', e.message);
}
```
- A. `caught without binding` then `caught: boom`
- B. `SyntaxError` thrown — not caught
- C. `caught without binding` then `caught: undefined`
- D. `ReferenceError: e is not defined`

---

## 6. String Handling

### Q16. What does the following code output?
```javascript
const s = '   hello world   ';
console.log(`[${s.trim()}]`);
console.log(`[${s.trimStart()}]`);
console.log(`[${s.trimEnd()}]`);
```
- A. `[hello world] [hello world   ] [   hello world]`
- B. `[hello world] [hello world] [hello world]`
- C. `[hello world] [   hello world] [hello world   ]`
- D. `[   hello world   ] [hello world   ] [   hello world]`

---

### Q17. Which regex correctly matches a string ending in `abc` preceded by exactly 3 digits?
- A. `/\d{3}abc$/`
- B. `/^\d+abc$/`
- C. `/^\d{3}abc/`
- D. `/\d*abc$/`

---

### Q18. What does the following code output?
```javascript
const s = 'café';
console.log(s.length);
console.log([...s].length);
```
(Assume `é` is encoded as the two code points "e" + combining acute accent U+0301.)
- A. `4 4`
- B. `5 4`
- C. `5 5`
- D. `4 5`

---

## 7. Variables and Syntax

### Q19. What does the following code output?
```javascript
console.log(typeof null);
console.log(typeof undefined);
console.log(typeof NaN);
console.log(typeof []);
```
- A. `null undefined number object`
- B. `object undefined number object`
- C. `object undefined NaN array`
- D. `null undefined NaN array`

---

### Q20. What is the final value of `obj`?
```javascript
const obj = { a: 1 };
obj.a = 2;
obj.b = 3;
Object.freeze(obj);
obj.a = 99;
obj.c = 4;
console.log(obj);
```
(Non-strict mode.)
- A. `{ a: 99, b: 3, c: 4 }`
- B. `{ a: 2, b: 3 }`
- C. Throws `TypeError`
- D. `{ a: 2, b: 3, c: 4 }`

---

### Q21. Which of the following is a **primitive** type?
- A. `Array`
- B. `Symbol`
- C. `Map`
- D. `Date`

---

## 8. Classes

### Q22. What does the following code output?
```javascript
class Animal {
  constructor(name) { this.name = name; }
  speak() { return `${this.name} makes a sound`; }
}
class Dog extends Animal {
  speak() { return `${super.speak()} - woof`; }
}
const d = new Dog('Rex');
console.log(d.speak());
```
- A. `Rex makes a sound`
- B. `Rex makes a sound - woof`
- C. `undefined - woof`
- D. `TypeError`

---

### Q23. Which statement about ES classes vs. prototypes is **correct**?
- A. `class` is a brand-new mechanism unrelated to prototypes
- B. `class` is syntactic sugar over prototypes; methods live on `Class.prototype`
- C. `class` methods are copied into every instance
- D. A `class` cannot extend a prototype-style constructor function

---

### Q24. What does the following code output?
```javascript
class Counter {
  constructor() { this.count = 0; }
  static create() { return new Counter(); }
  inc() { this.count++; return this; }
  get value() { return this.count; }
}

const c = Counter.create();
c.inc().inc().inc();
console.log(c.value, typeof Counter.prototype.create);
```
- A. `3 'function'`
- B. `3 'undefined'`
- C. `0 'function'`
- D. `TypeError: Counter.create is not a function`

---

## 9. Keyed Collections

### Q25. What does the following code output?
```javascript
const m = new Map();
const k1 = { id: 1 };
const k2 = { id: 1 };
m.set(k1, 'a');
m.set(k2, 'b');
m.set('1', 'c');
m.set(1, 'd');
console.log(m.size);
```
- A. `1`
- B. `2`
- C. `3`
- D. `4`

---

### Q26. Which is a **unique** advantage of `Map` over a plain object?
- A. Any value (including objects and functions) can be used as a key
- B. The `size` property gives element count directly
- C. Iteration order is guaranteed to follow insertion order
- D. All of the above

---

### Q27. What does the following code output?
```javascript
const ws = new WeakSet();
let obj = { a: 1 };
ws.add(obj);
console.log(ws.has(obj));
obj = null;
// Assume garbage collection has run.
console.log(ws.size);
```
- A. `true 1`
- B. `true 0`
- C. `true undefined`
- D. `false undefined`

---

## 10. Arrow Functions

### Q28. What does the following code output?
```javascript
const obj = {
  name: 'Leo',
  greet1: function() { return this.name; },
  greet2: () => this.name,
};
console.log(obj.greet1());
console.log(obj.greet2());
```
(Run at the top level in a browser; `this` is `window`, and `window.name` defaults to an empty string.)
- A. `Leo Leo`
- B. `Leo ''`
- C. `Leo undefined`
- D. `undefined ''`

---

### Q29. What is the value of `t.seconds` after about 3 seconds?
```javascript
function Timer() {
  this.seconds = 0;
  setInterval(() => { this.seconds++; }, 1000);
}
const t = new Timer();
```
- A. Always 0 (because `this` is wrong)
- B. Increments by roughly 1 per second
- C. Throws `TypeError`
- D. Becomes `NaN`

---

### Q30. Which of these can an arrow function **not** do?
- A. Be used as an array method callback
- B. Be used as a Promise `.then` callback
- C. Be invoked with `new` as a constructor
- D. Be used as an immediately-invoked function expression (IIFE)

---

## 11. JavaScript Modules

### Q31. Which statement about ES Modules (`import` / `export`) is **incorrect**?
- A. `import` is static and must appear at the top level of the module
- B. ES Modules are in strict mode by default
- C. `export default` and named `export` can coexist in one module
- D. ES Module loading semantics are identical to CommonJS `require`

---

### Q32. Is the following code valid?
```javascript
// math.js
export const pi = 3.14;
export default function add(a, b) { return a + b; }

// main.js
import add, { pi } from './math.js';
```
- A. Valid syntax
- B. `default` cannot coexist with named exports
- C. Import order must be `{ pi }, add`
- D. `add` must be wrapped in braces

---

### Q33. Which statement about `export` semantics is **correct**?
- A. `export default` exports the value at export time; later reassignment in the source module has no effect on importers
- B. Named exports export a snapshot of the value at the moment of export
- C. Named exports are live bindings: importers see updates from the source module
- D. All exports are deep clones to prevent mutation

---

## 12. Iteration Functions

### Q34. What does the following code output?
```javascript
function* gen() {
  yield 1;
  yield 2;
  return 3;
  yield 4;
}
const it = gen();
console.log(it.next());
console.log(it.next());
console.log(it.next());
console.log(it.next());
```
- A. `{value:1,done:false} {value:2,done:false} {value:3,done:true} {value:undefined,done:true}`
- B. `{value:1,done:false} {value:2,done:false} {value:3,done:false} {value:4,done:true}`
- C. `{value:1,done:false} {value:2,done:false} {value:4,done:false} {value:3,done:true}`
- D. After `return`, all subsequent calls throw

---

### Q35. What does the following code output?
```javascript
const obj = {
  data: [10, 20, 30],
  [Symbol.iterator]() {
    let i = 0;
    const data = this.data;
    return {
      next() {
        return i < data.length
          ? { value: data[i++], done: false }
          : { value: undefined, done: true };
      }
    };
  }
};
console.log([...obj]);
```
- A. `[10, 20, 30]`
- B. `[]`
- C. `TypeError`
- D. `[{value:10}, {value:20}, {value:30}]`

---

### Q36. Which statement about `yield` vs. `yield*` is **correct**?
- A. They are identical
- B. `yield*` delegates to another iterable, yielding each of its values in turn
- C. `yield*` only works inside async generators
- D. `yield*` returns the iterable itself rather than expanding it

---

## 13. Scope, Hoisting and Closures

### Q37. What does the following code output?
```javascript
console.log(a);
console.log(b);
var a = 1;
let b = 2;
```
- A. `undefined undefined`
- B. `undefined ReferenceError`
- C. `ReferenceError` (thrown on the first line)
- D. `1 2`

---

### Q38. What does the following code output?
```javascript
const fns = [];
for (var i = 0; i < 3; i++) {
  fns.push(() => i);
}
console.log(fns.map(f => f()));
```
- A. `[0, 1, 2]`
- B. `[3, 3, 3]`
- C. `[2, 2, 2]`
- D. `[undefined, undefined, undefined]`

---

### Q39. What does the following code output?
```javascript
function makeCounter() {
  let count = 0;
  return {
    inc() { return ++count; },
    get() { return count; },
  };
}
const c1 = makeCounter();
const c2 = makeCounter();
c1.inc(); c1.inc(); c2.inc();
console.log(c1.get(), c2.get());
```
- A. `2 1`
- B. `3 3`
- C. `2 2`
- D. `1 1`

---

## 14. Promises / async-await

### Q40. What is the output order?
```javascript
console.log('1');
setTimeout(() => console.log('2'), 0);
Promise.resolve().then(() => console.log('3'));
console.log('4');
```
- A. `1 2 3 4`
- B. `1 4 3 2`
- C. `1 4 2 3`
- D. `1 3 4 2`

---

### Q41. What does the following code output?
```javascript
async function f() {
  try {
    const r = await Promise.reject(new Error('oops'));
    return r;
  } catch (e) {
    return 'caught: ' + e.message;
  }
}
f().then(v => console.log(v));
```
- A. `caught: oops`
- B. `Error: oops` (unhandled rejection)
- C. `undefined`
- D. `Promise { <rejected> }`

---

### Q42. What does the following code output?
```javascript
const p = new Promise((resolve, reject) => {
  setTimeout(() => resolve('done'), 0);
});

p
  .then(v => console.log('then1:', v))
  .finally(() => console.log('finally'))
  .then(v => console.log('then2:', v));
```
- A. `then1: done` `finally` `then2: done`
- B. `then1: done` `finally` `then2: undefined`
- C. `finally` `then1: done` `then2: undefined`
- D. `then1: done` `then2: undefined` `finally`

---

