# javaScript_overView (Features added from ES2015(ES6) - ES2026(ES17)

## 1.`Date()` vs `Temporal()`

### `Date()`

If we store a date in one variable and copy it into another variable, changing the new variable also changes the original one.

```javascript
let today = new Date();

let copydate = today;

today.setDate(today.getDate() + 7);
```

### `Temporal()`

If we store a date in one variable and copy it into another variable, updating the new one does not affect the original one.

```javascript
let today = Temporal.Now.plainDateISO();

let updated = today.add({ weeks: 1 });
```
# 2. `file.close()` vs `using`

## Without `using`

We have to explicitly call `file.close()` or `connection.end()` to close the file or connection. If we forget to close it, memory and resources may be wasted.

```javascript
function file() {
  const file = openFile("meri_file.txt");
  file.close();
}
```

## With `using`

If we use the `using` keyword, the file is automatically closed after execution, so resources are released automatically.

```javascript
function file() {
  using file = openFile("meri_file.txt");
}
```

## 3. `reduce()` vs `Math.sumPrecise()`

### `reduce()`

When we use floating point values and calculate them using the `reduce()` method, it can give an inaccurate result.

```javascript
const items = [0.1, 0.2, 0.3];
const total = items.reduce((total, num) => total + num, 0);

console.log(total);
// Output: 0.6000000000000001
```

### `Math.sumPrecise()`

For floating point values, it gives an accurate or precise result.

```javascript
const items = [0.1, 0.2, 0.3];
const total = Math.sumPrecise(items);

console.log(total);
// Output: 0.6
```
## 4.`instanceof` vs `Error.isError()`

### `instanceof`

In a `catch` block, `instanceof Error` only recognizes errors from the same realm (such as the same window or script). Errors from other realms may not be considered proper `Error` objects.

```javascript
try {
} catch (err) {
  if (err instanceof Error) {
    console.log("Error");
  } else {
    console.log("Something Else or not an error");
  }
}
```

### `Error.isError()`

`Error.isError()` recognizes errors regardless of where they come from (window, script, or another realm).

```javascript
try {
} catch (err) {
  if (Error.isError(err)) {
    console.log("Error");
  }
}
```
## 5. `[...arr, ...arr1]` vs `Iterator.concat()`

### Spread Operator

It is used to combine two arrays/lists using the spread operator, but it takes more memory and time.

```javascript
const list1 = [1, 2];
const list2 = [3, 4];
const combined = [...list1, ...list2];

for (const num of combined) {
  console.log(num); // 1, 2, 3, 4
}
```

### `Iterator.concat()`

It combines two arrays/lists in less time and uses less memory compared to the spread operator.

```javascript
const list1 = [1, 2];
const list2 = [3, 4];
const combined = Iterator.concat(list1, list2);

for (const num of combined) {
  console.log(num); // 1, 2, 3, 4
}
```
## 6.`reduce()` vs `Object.groupBy()`

### `reduce()`

It can also be used to store or group values, but we have to do everything manually, such as checking whether the object exists and then storing the values.

```javascript
const items = [
  { name: "Apple", type: "fruit" },
  { name: "Tomato", type: "vegetable" },
  { name: "Banana", type: "fruit" }
];

const groups = items.reduce((acc, item) => {
  if (!acc[item.type]) {
    acc[item.type] = [];
  }

  acc[item.type].push(item);
  return acc;
}, {});
```

### `Object.groupBy()`

It automatically handles grouping, including checking whether the group exists or not.

```javascript
const items = [
  { name: "Apple", type: "fruit" },
  { name: "Tomato", type: "vegetable" },
  { name: "Banana", type: "fruit" }
];

const groups = Object.groupBy(items, item => item.type);
```
## 7.`JSON.parse()`

It converts a JSON string into a JavaScript object.

```javascript
const jsonString = '{"name": "Rahul", "age": 25, "city": "Delhi"}';
const userObject = JSON.parse(jsonString);

console.log(userObject.name); // "Rahul"
console.log(userObject.age);  // 25
```
## 8. Iterator Helpers (`map`, `filter`, `take`, `drop`)

These helper methods let you transform and process iterators without converting them into arrays first.

```javascript
const iterator = [1, 2, 3, 4, 5].values();

const result = iterator
  .filter(x => x % 2 !== 0)
  .take(2)
  .toArray();

console.log(result); // [1, 3]
```
## 9. `Array.fromAsync()`

It takes data from an async source and directly converts it into an array.

```javascript
async function* asyncGen() {
  yield await Promise.resolve(1);
  yield await Promise.resolve(2);
}

const arr = await Array.fromAsync(asyncGen());

console.log(arr); // [1, 2]
```
## 10. Pipeline Operator (`|>`)

It is used to pass the output of one function directly to another function.

```javascript
// Old way
const result = double(addFive(value));

// New way
const result = value |> addFive |> double;
```
## 11. `Promise.withResolvers()`

It returns an object containing `promise`, `resolve`, and `reject`, so you don't need to create them manually.

```javascript
const { promise, resolve, reject } = Promise.withResolvers();

setTimeout(() => resolve("Kaam ho gaya!"), 1000);

promise.then(msg => console.log(msg));
```
## 12. `String.isWellFormed()` & `toWellFormed()`

It checks whether a string contains invalid characters. `toWellFormed()` removes or replaces those invalid characters.

```javascript
const goodString = "Hello";

console.log(goodString.isWellFormed()); // true

const badString = "\uD800"; // Invalid character

console.log(badString.toWellFormed()); // only valid characters
```
## 13. Exponentiation Operator (`**`)

If we want to find the power of a number, we can use the `Math.pow()` method. Now we can directly calculate power using the `**` operator.

```javascript
let square = Math.pow(5, 2); // 25

let cube = 2 ** 3; // 8
```
## 14.`Array.includes()`

To check whether an element exists in an array, we used `indexOf()` which returns `-1` if the element is not found. Now, `includes()` makes it easier by returning `true` or `false`.

```javascript
let fruits = ['apple', 'banana', 'mango'];

// Using indexOf()
if (fruits.indexOf('banana') !== -1) {
    console.log("found");
}

// Using includes()
if (fruits.includes('banana')) {
    console.log("Found");
}
```
## 15.`async` & `await`

It helps to write asynchronous code in a synchronous way. Instead of using `.then()` with promises, we can use `async` and `await`.

```javascript
// Promises
fetch('https://api.example.com/data')
  .then(res => res.json())
  .then(data => console.log(data));

// Async/Await
async function getData() {
  const response = await fetch('https://api.example.com/data');
  const data = await response.json();
  console.log(data);
}
```
## 16.`Object.values()`

It returns object values in an array.

```javascript
const user = { name: 'Rahul', age: 25 };

console.log(Object.values(user)); // ['Rahul', 25]
```

## 17.`Object.entries()`

It converts key-value pairs into an array format.

```javascript
const user = { name: 'Rahul', age: 25 };

console.log(Object.entries(user)); 
// [['name', 'Rahul'], ['age', 25]]
```

##18. String Padding (`padStart`, `padEnd`)

It is used to add characters to a string with a fixed length at the start or end.

```javascript
let id = "5";

console.log(id.padStart(3, '0')); // "005"
console.log(id.padEnd(3, 'x'));   // "5xx"
```

## 19.`Object.getOwnPropertyDescriptors()`

It shows the configuration details of object properties like writable and editable.

```javascript
const obj = { name: 'Kanchan' };

console.log(Object.getOwnPropertyDescriptors(obj));
```
## 20. Trailing Commas

We can add a comma after the last parameter or property.

```javascript
function greet(
  name,
  age, // trailing comma
) {
  console.log(name, age);
}
```

## 21.Rest/Spread Properties (`...`)

**Rest:** It is used to store remaining properties in an object or array.

**Spread:** It is used to copy one object or array into another.

```javascript
const user = { name: 'Rahul', age: 25, city: 'Delhi' };

// Rest
const { name, ...details } = user;

console.log(name);    // 'Rahul'
console.log(details); // { age: 25, city: 'Delhi' }

// Spread
const newUser = { ...user, country: 'India' };
```
## 22. Asynchronous Iteration (`for await...of`)

If there is an `await` function inside a loop, a normal `for...of` loop does not wait for the promise to resolve. `for await...of` solves this problem by waiting until the promise is resolved.

```javascript
async function getNumbers() {
  const promises = [
    Promise.resolve(1),
    Promise.resolve(2),
    Promise.resolve(3)
  ];

  for await (const num of promises) {
    console.log(num);
  }
}
```

## 23.`Promise.finally()`

It executes in every case, whether the promise is resolved or rejected. It is useful for tasks like hiding loading spinners.

```javascript
fetch('https://api.example.com')
  .then(data => console.log(data))
  .catch(err => console.error(err))
  .finally(() => console.log('Loading Spinner closed!'));
```

## 24.`Array.flat()` / `Array.flatMap()`

**`flat()`**: Converts a nested array into a single array.

**`flatMap()`**: First performs mapping (transformation) and then converts the nested array into a level-1 array.

```javascript
const arr = [1, 2, [3, 4, [5, 6]]];

console.log(arr.flat()); 
// [1, 2, 3, 4, [5, 6]] (default 1 level)

console.log(arr.flat(2)); 
// [1, 2, 3, 4, 5, 6] (2 levels deep)

const nums = [1, 2, 3];

console.log(nums.flatMap(x => [x, x * 2]));
// [1, 2, 2, 4, 3, 6]
```
## 25.`Object.fromEntries()`

It converts an array into an object.

```javascript
const entries = [['name', 'Rahul'], ['age', 25]];

const user = Object.fromEntries(entries);

console.log(user); // { name: 'Rahul', age: 25 }
```

## 26. `String.trimStart()` / `String.trimEnd()`

It is used to remove spaces from the start or end of a string.

```javascript
const text = "   Hello World   ";

console.log(text.trimStart()); // "Hello World   "
console.log(text.trimEnd());   // "   Hello World"
```

## 27. Optional Catch Binding

We can remove the error parameter from the `catch` block if we do not need it.

```javascript
// Old way
try {
  // code...
} catch (e) {
  // code
}

// New way
try {
  // code...
} catch {
  console.log("Error");
}
```
## 28.`Symbol.description`

It is used to read the description of a Symbol.

```javascript
const sym = Symbol("MySymbol");

console.log(sym.description); // "MySymbol"
```

## 29.`JSON.stringify()` Improvements

If it finds complex characters, it returns a valid JSON format.

```javascript
const badString = '\uD800';

console.log(JSON.stringify(badString));
// Result: "\uD800"

console.log(JSON.stringify(badString));
// Output: "\ud800"
```

## 30. `globalThis`

It provides a standard way to access the global object.

```javascript
console.log(globalThis); // Browser: window, Node: global
```

## 31.`Promise.allSettled()`

It waits for all promises to complete and returns their results.

```javascript
const p1 = Promise.resolve("Success");
const p2 = Promise.reject("Error");

Promise.allSettled([p1, p2])
  .then((results) => console.log(results));
```

## 32. `BigInt`

It is a primitive datatype used to store large numbers.

## 33.Nullish Coalescing Operator (`??`)

It is used to provide a default value when the value is `null` or `undefined`.

```javascript
const count = 0;

// Old way
console.log(count || 10); // 10

// New way
console.log(count ?? 10); // 0
```

## 34.Optional Chaining (`?.`)

It is used to access nested object values safely. If the value does not exist, it returns `undefined` instead of crashing the application.

```javascript
const user = { name: "Rahul", address: { city: "Delhi" } };

console.log(user?.address?.zip); // undefined
```

## 35. Logical Assignment Operators (`||=`, `&&=`, `??=`)

```javascript
// 1. OR Assignment (||=)
let a = 0;

a ||= 10; // if a is false, assign 10
console.log(a); // 10


// 2. AND Assignment (&&=)
let b = 1;

b &&= 5; // if b is true, assign 5
console.log(b); // 5


// 3. Nullish Assignment (??=)
let c = null;

c ??= 20; // if null or undefined, assign 20
console.log(c); // 20
```
## 36.`String.replaceAll()`

It is used to replace all occurrences of a word with a new word.

```javascript
const text = "JS is great. I love JS.";

console.log(text.replaceAll("JS", "Python"));
// "Python is great. I love Python."
```

## 37.`Promise.any()`

It returns the result of the first resolved promise.

```javascript
const p1 = new Promise((res) => 
  setTimeout(() => res("P1"), 1000)
);

const p2 = new Promise((res) => 
  setTimeout(() => res("P2"), 500)
);

Promise.any([p1, p2])
  .then(result => console.log(result));

// Output: "P2"
```

## 38.Numeric Separators (`_` in numbers)

It helps to add `_` in numbers for better readability.

```javascript
const budget = 1000000000;

const easyBudget = 1_000_000_000;

console.log(easyBudget);
```

## 39.Class Field Declarations / Private Class Features (`#`)

We can define class properties without using a constructor.

```javascript
class User {
  name = "Rahul";
  age = 25;
}

const user1 = new User();

console.log(user1.name); // "Rahul"
```

We can also declare private properties in a class using `#`.

```javascript
class BankAccount {
  #balance = 0; // Private property

  deposit(amount) {
    this.#balance += amount;
  }
}
```

## 40.Top-Level `await`

We can use `await` without an `async` function (in modules) for data retrieval.

```javascript
const response = await fetch("https://api.example.com/data");
const data = await response.json();

console.log(data);
```

### 41.`Array.at()`

It returns the element at the given index.

```javascript
const arr = [10, 20, 30, 40];

console.log(arr.at(1));  // 20
console.log(arr.at(-1)); // 40 (Last element)
```

### 42.`Object.hasOwn()`

It checks whether a property belongs to an object or not.

```javascript
const person = { name: "Rahul" };

console.log(Object.hasOwn(person, "name")); // true
```

## 43. Error Cause

It displays the reason for an error using the `cause` property.

```javascript
try {
  throw new Error("error", { cause: "Database connection failed" });
} catch (err) {
  console.log(err.message); // "error"
  console.log(err.cause);   // "Database connection failed"
}
```

## 44. Array Copying Methods (Non-mutating methods)

Methods like `toSorted()`, `toReversed()`, `toSpliced()`, `with(index, value)`, `findLast()`, and `findLastIndex()` do not update the original array. They create a new array.

```javascript
const arr = [3, 1, 2];

const sorted = arr.toSorted();

const updated = arr.with(1, 10);

console.log(updated); // [3, 10, 2]
console.log(arr);     // [3, 1, 2]
```
