---
tags: []
date: 2026-05-05
time: 16:50
---

# JavaScript Mock Test (Combined: Questions + Explanations)

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

**Answer: A**

**Explanation:**
`flatMap` is equivalent to `map` followed by `flat(1)`. Per element:
- `1` → `[1, 2]`
- `2` → `[]` (filtered out)
- `3` → `[3, 6]`
- `4` → `[]`
- `5` → `[5, 10]`

Flattening one level gives `[1, 2, 3, 6, 5, 10]`. A common idiom: returning `[]` from the mapper achieves a `map + filter` in one pass. (`flatMap` was introduced in ES2019.)

---

### Q2. Which statement about `Array.prototype.sort()` after ES2019 is **correct**?
- A. The result is unstable across all engines
- B. ES2019 requires `sort` to be a stable sort
- C. `sort` orders by numeric value by default
- D. `sort` does not mutate the original array

**Answer: B**

**Explanation:**
A key change in ES2019 (ECMAScript 10) is that `Array.prototype.sort` is now required to be **stable**: equal-keyed elements must preserve their relative order.
- A: false; ES2019 requires stability.
- C: false; the default comparator converts elements to strings and compares by UTF-16 code units, so `[10, 2, 1].sort()` yields `[1, 10, 2]`.
- D: false; `sort` mutates the array in place and returns the same reference.

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

**Answer: A**

**Explanation:**
Manually increasing `length` creates a **sparse array**: indices 3 and 4 are "empty slots", not actual values.
- Reading `arr[3]` returns `undefined` (the default for missing properties).
- `length` is indeed `5`.
- Critical gotcha: `includes(undefined)` returns **`true`** because `includes` treats empty slots as `undefined`. In contrast, `indexOf(undefined)` returns `-1` because `indexOf` skips empty slots.

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

**Answer: A**

**Explanation:**
- `new Animal('Leo')` creates an instance whose `__proto__` references `Animal.prototype`; calling `greet()` binds `this` to `a`.
- `Object.create(Animal.prototype)` produces an object whose `__proto__` also references `Animal.prototype`, so it can call `greet()` too.
- Both prototypes are the same object reference, so `===` is `true`.

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

**Answer: B**

**Explanation:**
When `Object.defineProperty` is called without explicit descriptors, all default to `false`: `writable: false`, `enumerable: false`, `configurable: false`.
- In **non-strict mode**, assigning to a non-writable property fails **silently** (no error, but no effect), so `obj.x` stays `1`.
- In strict mode, it would throw `TypeError`. The snippet has no `'use strict'`, so B.

---

### Q6. Which statement most precisely describes prototypal inheritance in JavaScript?
- A. An object copies all properties from its parent to form its own duplicate
- B. An object holds an internal `[[Prototype]]` link to another object; property lookups walk up the chain
- C. The child and parent objects share the same memory address
- D. JavaScript has no prototypal inheritance — only classical inheritance

**Answer: B**

**Explanation:**
Prototypal inheritance is built around the `[[Prototype]]` internal slot (observable via `__proto__` in most implementations; the standard APIs are `Object.getPrototypeOf` / `Object.setPrototypeOf`). Property access walks the chain until found; nothing is copied.
- A describes copy-based inheritance, which JS does not do.
- C is incorrect; the prototype is just a reference link.
- D is wrong; `class` is syntactic sugar over prototypes.

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

**Answer: B**

**Explanation:**
A default parameter triggers only when the argument is **strictly `undefined`** — `null` does not count.
- Line 1: `b` is `undefined`, default `10` applies, result is `1 + 10 + 3 = 14`.
- Line 2: `b` is `null`, default does **not** apply; `null` coerces to `0` in arithmetic, result is `1 + 0 + 3 = 4`.

---

### Q8. Which of the following is **not** a property of "first-class functions" in JavaScript?
- A. Functions can be assigned to variables
- B. Functions can be passed as arguments
- C. Functions can be returned from other functions
- D. Functions cannot have their own properties

**Answer: D**

**Explanation:**
Functions in JS are objects and can carry their own properties:
```javascript
function f() {}
f.cache = {};
console.log(typeof f.cache); // 'object'
```
This is the classic backing for memoization. A, B, and C are all standard first-class function properties.

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

**Answer: B**

**Explanation:**
- A `function` declaration receives its own `arguments` object, so `sum` works.
- **Arrow functions have no `arguments`**; they look up the lexical scope. At top level (browser/ES module), there is no enclosing `arguments`, so referencing it throws `ReferenceError: arguments is not defined`.
- To collect parameters in an arrow function, use rest parameters: `(...args) => ...`.

> Note: at the top level of a Node.js CommonJS module, the wrapping function does provide an `arguments` object, so behavior may differ there. This question assumes a browser or ES module environment.

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

**Answer: A**

**Explanation:**
- `for...in` iterates over **enumerable string keys** (including inherited ones, though there are none here), yielding `'a'`, `'b'`, `'c'` in insertion order.
- `for...of` iterates over an **iterable**. A plain object is not iterable, but `Object.values(obj)` returns the array `[1, 2, 3]`, which is.

Concatenated: `'abc' + '123' = 'abc123'`.

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

**Answer: B**

**Explanation:**
`switch` uses **strict equality (`===`)** — no type coercion. `'1' === 1` is `false`, but `'1' === '1'` is `true`, so the second case runs and prints `string`.

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

**Answer: B**

**Explanation:**
`i` runs through `0, 1, 2, 3, 4` — five iterations. When `i === 2`, `continue` skips the print, leaving four prints. Note: the `i++` before `continue` is essential, otherwise the loop would be stuck at `i === 2`.

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

**Answer: A**

**Explanation:**
For `+`, if either operand is non-primitive, JS calls `ToPrimitive` (hint `default`):
- `[].toString()` → `''`
- `({}).toString()` → `'[object Object]'`

Therefore:
- `[] + []` → `'' + ''` → `''`
- `[] + {}` → `'' + '[object Object]'` → `'[object Object]'`
- `{} + []` (as expression) → `'[object Object]' + ''` → `'[object Object]'`.

> Caveat: in some REPLs at the statement level, the leading `{}` is parsed as a block, making `+[]` evaluate to `0`. The question explicitly fixes the expression context, so A.

---

### Q14. Which expression evaluates to `true`?
- A. `0.1 + 0.2 === 0.3`
- B. `NaN === NaN`
- C. `Object.is(NaN, NaN)`
- D. `[] === []`

**Answer: C**

**Explanation:**
- A: IEEE 754 rounding — `0.1 + 0.2` is actually `0.30000000000000004`.
- B: `NaN` is unequal to everything, including itself — the only non-reflexive value in JS.
- C: `Object.is` differs from `===` in two cases: `Object.is(NaN, NaN) === true` and `Object.is(+0, -0) === false`.
- D: two distinct array literals are different references.

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

**Answer: A**

**Explanation:**
ES2019 introduced **optional catch binding**: the `(e)` after `catch` is now optional when you do not need the error object. The first `try/catch` uses this new syntax, the second uses the traditional binding. Both work and run as expected.
- B: false; both errors are caught locally.
- C: false; the second catch binds `e` and prints its message.
- D: false; the catch parameter is in scope inside its own block.

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

**Answer: A**

**Explanation:**
ES2019 standardized `trimStart` and `trimEnd` (the legacy non-standard `trimLeft` / `trimRight` are kept as aliases).
- `trim()` removes whitespace from both ends.
- `trimStart()` removes only leading whitespace; trailing whitespace remains.
- `trimEnd()` removes only trailing whitespace; leading whitespace remains.

---

### Q17. Which regex correctly matches a string ending in `abc` preceded by exactly 3 digits?
- A. `/\d{3}abc$/`
- B. `/^\d+abc$/`
- C. `/^\d{3}abc/`
- D. `/\d*abc$/`

**Answer: A**

**Explanation:**
- A: `\d{3}` matches exactly 3 digits, `abc$` anchors to end. The pattern allows arbitrary leading text but ensures the tail is `<3 digits>abc`. (For exactly that and nothing else, you would write `/^\d{3}abc$/`.)
- B: `\d+` matches one or more, not exactly three.
- C: missing `$`, so it does not require ending.
- D: `\d*` allows zero or more.

> Reasoning: among the four options, A matches the requirement "ending in `abc` with exactly 3 digits before it" most precisely.

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

**Answer: B**

**Explanation:**
- `String.prototype.length` returns the number of **UTF-16 code units**. `c`, `a`, `f`, `e`, and the combining accent occupy 5 code units total.
- The string iterator walks **code points** (handling surrogate pairs), but treats `e` and the combining accent as two separate code points, giving 4 elements when spread.

To count user-perceived characters (grapheme clusters) you would need `Intl.Segmenter` (ES2022+) — outside ES2019.

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

**Answer: B**

**Explanation:**
- `typeof null === 'object'` — a long-standing historical quirk now baked into the spec.
- `typeof undefined === 'undefined'`.
- `typeof NaN === 'number'` — `NaN` is a number type value.
- `typeof [] === 'object'` — arrays are objects. Use `Array.isArray()` to test for arrays.

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

**Answer: B**

**Explanation:**
`Object.freeze` sets `writable: false` and `configurable: false` on every property and makes the object non-extensible.
- Modifying `a` fails silently in non-strict mode.
- Adding `c` fails silently in non-strict mode.

The object stays `{ a: 2, b: 3 }`. Note: `freeze` is shallow — nested objects need recursion to deep-freeze.

---

### Q21. Which of the following is a **primitive** type?
- A. `Array`
- B. `Symbol`
- C. `Map`
- D. `Date`

**Answer: B**

**Explanation:**
ES2019 has 7 primitive types: `undefined`, `null`, `boolean`, `number`, `string`, `symbol`, `bigint`. Everything else (Array, Map, Set, Date, Object, Function, etc.) is an object.

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

**Answer: B**

**Explanation:**
`super.speak()` invokes the parent method while keeping `this` bound to the subclass instance `d`, so `this.name` is `'Rex'`. The combined string is `'Rex makes a sound - woof'`.

---

### Q23. Which statement about ES classes vs. prototypes is **correct**?
- A. `class` is a brand-new mechanism unrelated to prototypes
- B. `class` is syntactic sugar over prototypes; methods live on `Class.prototype`
- C. `class` methods are copied into every instance
- D. A `class` cannot extend a prototype-style constructor function

**Answer: B**

**Explanation:**
`class` is sugar over constructor function + prototype, with a few semantic adjustments (class body is in strict mode by default, calls without `new` throw, TDZ for the binding, etc.). `extends` works with **any constructible callable**, including legacy constructor functions.

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

**Answer: B**

**Explanation:**
- `Counter.create()` is a **static method** — it lives on the constructor (`Counter`) itself, not on `Counter.prototype`. So `Counter.create()` works, returning a new instance.
- `c.inc().inc().inc()` chains three increments because `inc` returns `this`. `c.value` ends at `3`.
- `Counter.prototype.create` is `undefined` — static methods are not put on the prototype. So `typeof undefined === 'undefined'`.

This is a frequent source of confusion: `static` puts the method where instances cannot reach it via the prototype chain.

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

**Answer: D**

**Explanation:**
`Map` uses the **SameValueZero** algorithm for key equality. Objects compare by **reference**.
- `k1` and `k2` are distinct references despite identical contents — they count as two keys.
- `'1'` (string) and `1` (number) are also two distinct keys (`Map` does no coercion, unlike object property keys).

Total: 4 keys.

---

### Q26. Which is a **unique** advantage of `Map` over a plain object?
- A. Any value (including objects and functions) can be used as a key
- B. The `size` property gives element count directly
- C. Iteration order is guaranteed to follow insertion order
- D. All of the above

**Answer: D**

**Explanation:**
- A: object property keys can only be strings or symbols; other types coerce to strings. Maps have no such restriction.
- B: for plain objects you compute `Object.keys(o).length`.
- C: `Map` iteration order is specified to be insertion order. Plain object key order is more nuanced (integer-index keys first in ascending order, then string keys in insertion order, then symbols).

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

**Answer: C**

**Explanation:**
`WeakSet` and `WeakMap` hold members by **weak reference**: when no other strong references exist, members can be reclaimed. But `WeakSet` has **no `size` property, no iteration, no `clear`** — by spec, to avoid leaking GC timing observability. Hence `undefined` on the second line.

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

**Answer: B**

**Explanation:**
- `greet1` is a regular function; `this` is determined by the call site. With `obj.greet1()`, `this === obj`.
- `greet2` is an arrow function with **no `this` of its own** — it inherits from the enclosing lexical scope, which is `window`. `window.name` is the empty string `''` by default (a DOM-spec quirk, not `undefined`).

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

**Answer: B**

**Explanation:**
This is the canonical motivation for arrow functions: preserving the enclosing `this` inside callbacks. Inside `new Timer()`, `this` is the new instance `t`. The arrow function inside `setInterval` lexically inherits that `this`, so `this.seconds++` updates `t.seconds`.
With `function() { this.seconds++ }`, `this` would be the global object in non-strict mode — a classic bug.

---

### Q30. Which of these can an arrow function **not** do?
- A. Be used as an array method callback
- B. Be used as a Promise `.then` callback
- C. Be invoked with `new` as a constructor
- D. Be used as an immediately-invoked function expression (IIFE)

**Answer: C**

**Explanation:**
Arrow functions have no `[[Construct]]` internal method, so `new (() => {})()` throws `TypeError: ... is not a constructor`. Arrow functions also have no `prototype` property, no own `arguments`, and no own `this`.

---

## 11. JavaScript Modules

### Q31. Which statement about ES Modules (`import` / `export`) is **incorrect**?
- A. `import` is static and must appear at the top level of the module
- B. ES Modules are in strict mode by default
- C. `export default` and named `export` can coexist in one module
- D. ES Module loading semantics are identical to CommonJS `require`

**Answer: D**

**Explanation:**
- A: `import` is statically resolved at parse time, hence the top-level requirement.
- B: ES Modules are automatically strict.
- C: default + named exports commonly coexist (libraries do this all the time).
- D: **incorrect**. CommonJS `require` is synchronous and runtime-evaluated, returning a snapshot value (objects are by reference). ES Modules go through parse → instantiate → evaluate, and exported bindings are **live bindings** — the importer sees later mutations on the export side.

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

**Answer: A**

**Explanation:**
This is a legal and common pattern. The default import takes no braces (and may be renamed freely); named imports use braces and must match the exported name (or use `as` to rename).
- B: false; they coexist.
- C: false; the default import always comes **before** the braces.
- D: false; wrapping `add` in braces would actually break it.

---

### Q33. Which statement about `export` semantics is **correct**?
- A. `export default` exports the value at export time; later reassignment in the source module has no effect on importers
- B. Named exports export a snapshot of the value at the moment of export
- C. Named exports are live bindings: importers see updates from the source module
- D. All exports are deep clones to prevent mutation

**Answer: C**

**Explanation:**
Named exports are **live bindings**, not values:
```javascript
// counter.js
export let count = 0;
export function inc() { count++; }

// main.js
import { count, inc } from './counter.js';
console.log(count); // 0
inc();
console.log(count); // 1 — importer sees the update
```
- A: false; default-exported bindings are also live (the importer observes whatever the export-side binding currently holds).
- B: false; named exports are not snapshots.
- D: false; no cloning happens — that would defeat the purpose.

> Note: imported bindings are read-only on the importer side (`count = 5` from `main.js` would throw). Live binding means the *importer reads the latest value*, not that it can write back.

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

**Answer: A**

**Explanation:**
`yield` produces `{ done: false }` results; `return` produces `{ done: true }` carrying its `value`. The `yield 4` after `return` is unreachable. Once exhausted, additional calls to `it.next()` keep returning `{ value: undefined, done: true }` — they do not throw.

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

**Answer: A**

**Explanation:**
Implementing `[Symbol.iterator]()` that returns an object with `next()` makes the object an **iterable**, usable with spread, `for...of`, `Array.from`, etc. `[...obj]` consumes `data[i++]` until exhausted.

---

### Q36. Which statement about `yield` vs. `yield*` is **correct**?
- A. They are identical
- B. `yield*` delegates to another iterable, yielding each of its values in turn
- C. `yield*` only works inside async generators
- D. `yield*` returns the iterable itself rather than expanding it

**Answer: B**

**Explanation:**
`yield*` delegates to another iterable, equivalent to:
```javascript
function* outer() { yield* [1, 2, 3]; }
// is equivalent to
function* outer() { yield 1; yield 2; yield 3; }
```
It composes generators cleanly and correctly forwards the delegated generator's `return` value.

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

**Answer: B**

**Explanation:**
- `var` declarations are hoisted and initialized to `undefined`, so the first line prints `undefined`.
- `let` and `const` are also hoisted, but enter the **TDZ (Temporal Dead Zone)**: reading them before the declaration runs throws `ReferenceError`. The second line throws.

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

**Answer: B**

**Explanation:**
`var` is function-scoped, so the loop shares a single `i`. After the loop, `i === 3`; all three closures see the same `i` and print `3`.
With `let i`, a fresh binding is created per iteration, yielding `[0, 1, 2]` — a key reason `let` was added.

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

**Answer: A**

**Explanation:**
Each call to `makeCounter()` creates a fresh closure environment with its own `count`. `c1` and `c2` are independent: `c1.count` reaches 2; `c2.count` reaches 1. This is the classic encapsulation-via-closure pattern.

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

**Answer: B**

**Explanation:**
Event loop:
1. Synchronous code runs first: `1`, `4`.
2. After the current sync task, the **microtask queue is drained**: Promise `.then` callbacks are microtasks, so `3` prints.
3. Then the next macrotask runs: `setTimeout` callback prints `2`.

Key takeaway: microtasks have priority over macrotasks; `Promise.resolve().then` runs before `setTimeout(..., 0)`.

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

**Answer: A**

**Explanation:**
`await` on a rejected promise behaves like `throw`-ing the rejection reason, so it can be caught by `try/catch`. The catch block returns a string; the `async` function wraps it as a fulfilled promise; the outer `.then` receives `'caught: oops'`.

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

**Answer: B**

**Explanation:**
`Promise.prototype.finally` (ES2018) runs regardless of fulfillment or rejection. **Critically, it does not consume or change the value**: the promise it returns adopts the previous promise's state and value — but the function's return value is ignored, and its argument list is empty (no value passed in).

Sequence:
1. `then1` receives `'done'` and returns `undefined`.
2. The next `.finally` runs (no argument), prints `finally`. The promise it returns resolves with the value `then1` returned: `undefined`.
3. `then2` receives `undefined`.

If `finally`'s callback throws or returns a rejected promise, that **does** override the chain's outcome — but a normal return value (or no return) is ignored. This pass-through behavior is its main use: cleanup without disturbing the value.

---

## Answer Key

| #   | Ans | #   | Ans | #   | Ans | #   | Ans | #   | Ans | #   | Ans |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1   | A   | 8   | D   | 15  | A   | 22  | B   | 29  | B   | 36  | B   |
| 2   | B   | 9   | B   | 16  | A   | 23  | B   | 30  | C   | 37  | B   |
| 3   | A   | 10  | A   | 17  | A   | 24  | B   | 31  | D   | 38  | B   |
| 4   | A   | 11  | B   | 18  | B   | 25  | D   | 32  | A   | 39  | A   |
| 5   | B   | 12  | B   | 19  | B   | 26  | D   | 33  | C   | 40  | B   |
| 6   | B   | 13  | A   | 20  | B   | 27  | C   | 34  | A   | 41  | A   |
| 7   | B   | 14  | C   | 21  | B   | 28  | B   | 35  | A   | 42  | B   |
