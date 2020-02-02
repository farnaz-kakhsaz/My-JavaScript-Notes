# My JavaScript Notes

> This is my random JavaScript notes ;)

---

## Table of Contents:

- [The `find()` Method](<## The `find()` and the `filter()` methods:>)
- [The `filter()` Method](<## The `find()` and the `filter()` methods:>)
- [The `findIndex()` Method](<## The `find()` and the `findIndex()` methods:>)
- [The `includes()` Method](<## The `includes()()` and the `indexOf()` methods:>)
- [The `indexOf()` Method](<## The `includes()()` and the `indexOf()` methods:>)
- [The `splice()` Method](<## The `splice()`, the `slice()` and `split()` methods:>)
- [The `slice()` Method](<## The `splice()`, the `slice()` and `split()` methods:>)
- [The `split()` Method](<## The `splice()`, the `slice()` and `split()` methods:>)
- [Sorting by Name or Number](<## Sorting by Name or Number:>)

---

## The `find()` and the `filter()` methods:

**Syntax:**

```JavaScript
array.find(callback(element, [index], [array]), [thisArg])

array.filter(callback(element, [index], [array]), [thisArg])
```

**Similarities:** Both of them are only used for searching through an **array**, **not string**. And they will return actual value (for `find()` method) or an `array` with all elements (for `filter()` method) if they satisfy the provided testing `function`, **not `true` or `false`**. Also we need to write a testing `function` for them.
It means those methods take a _`callback`_, and that _`callback`_ is invoked for each item in an `array`.

These methods do **not mutate** the `array` on which it is called, but the `function` provided to _`callback`_ can. If so, the elements processed by them are set before the first invocation of _`callback`_. Therefore:

- _`callback`_ will not visit any elements added to the `array` after the call to `find()` or `filter()` begins.
- If an existing, yet-unvisited element of the `array` is changed by _`callback`_, its value passed to the _`callback`_ will be the value at the time `find()` or `filter()` visit that element.
- Elements that are _`deleted`_ are still visited.

**Differences:** The `find()` method will stop after the **first match** with testing `function`, and it returns the **actual item** (value), but the `filter()` method will continue searching through the entire `array`, and it returns the **new `array`** with all the matched items with testing `function`.

If no elements pass the test, the `find()` method returns **`undefined`**, while the `filter()` method returns an **empty `array`**.

**`Array.prototype.find()`:**

```JavaScript
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);                          // 12
```

Array.prototype.filter():

```JavaScript
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);                          // [12, 130, 44]
```

---

## The `find()` and the `findIndex()` methods:

**Syntax:**

```JavaScript
array.findIndex(callback(element, [index], [array]), [thisArg])
```

**Similarities:** Both of them are only used for searching through an **array**, **not string**. And they will return actual value (for `find()` method) or **index** (for `findIndex()` method) of the **first element** if they satisfy the provided testing function, **not `true` or `false`**. It means they will stop after the **first match** with testing `function`. Also we need to write a testing `function` for them.
It means those methods take a _`callback`_, and that _`callback`_ is invoked for each item in an `array`.

These methods do **not mutate** the `array` on which it is called, but the `function` provided to _`callback`_ can. If so, the elements processed by them are set before the first invocation of _`callback`_. Therefore:

- _`callback`_ will not visit any elements added to the `array` after the call to `find()` or `findIndex()` begins.
- If an existing, yet-unvisited element of the `array` is changed by _`callback`_, its value passed to the _`callback`_ will be the value at the time `find()` or `findIndex()` visit that element's index.
- Elements that are _`deleted`_ are still visited.

**Differences:** The `find()` method will return the **actual value** but `findIndex()` method will return the **index** of elemet if they satisfy the provided testing `function`.

If no element passed the test, the `find()` method returns **`undefined`**, while the `findIndex()` method returns an **`-1`**.

**`Array.prototype.findIndex()`:**

```JavaScript
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = (element) => element > 13;

console.log(array1.findIndex(isLargeNumber)); // 3

// ---------------------------------------

// Find the index of a prime number in an array:

function isPrime(num) {
    if (num > 2 && num % 2 == 0)
        return false;
    return num > 1;
}

console.log([4, 6, 8, 12].findIndex(isPrime)); // -1, not found
console.log([4, 6, 7, 12].findIndex(isPrime)); // 2 (array[2] is 7)

// ---------------------------------------

// Find index using arrow function

const fruits = ["apple", "banana", "cantaloupe", "blueberries", "grapefruit"];

const index = fruits.findIndex(fruit => fruit === "blueberries");

console.log(index);                          // 3
console.log(fruits[index]);                  // blueberries
```

---

## The `includes()` and the `indexOf()` methods:

**Syntax:**

```JavaScript
arrayOrString.includes(valueToFind, [startFromThisIndex])

arrayOrString.indexOf(valueToFind, [startFromThisIndex])
```

**Similarities:** Both of these methods can be used on **`string`** and **`array`** to find out whether the element is present in the `array` (or `string`) or not. They will return **`true`** (for `includes()` method) or **index** (for `indexOf()` method) if element matched **not actual value**. Also we don't need to write testing `function` (_`callback`_) for them, we just simply pass the value to them.

```JavaScript
// These two statements are the same
myArray.includes('some value')

myArray.indexOf('some value') !== -1
```

Both of the above statements do the same thing. Although the first statement (the `includes()` method) is the syntactic sugar for the second statement (the `indexOf()` method) which was an old way to write.

`.includes(valueToFind [, startFromThisIndex])`

`.indexOf(valueToFind [, startFromThisIndex])`

The second argument for both of them is **optional** and shows the index to start the search from. the default is 0.

```JavaScript
[-0].indexOf(0) > -1                         // true

[-0].includes(0)                             // true
```

Values of zero are all considered to be equal, regardless of sign. (That is, `-0` is considered to be equal to both `0` and `+0`), but `false` is not considered to be the same as `0`.

**Differences:** The `includes()` (ES2016) returns a `boolean` value — `true` or `false`. But `indexOf()` (ES5) returns the **first index** of the element (or character) found in the `array` (`string`), or it will return `-1` (which represents that the element or character is not found).

```JavaScript
[NaN].includes(NaN)                          // true

[NaN].indexOf(NaN) > -1                      // false
```

If `NaN` present in `array`, the `indexOf()` method for `NaN`, returns `-1` but on the other hand, `includes()` method returns `true`.

The `indexOf()` compares valueToFind to elements of the `Array` using `strict equality` (the same method used by the `===` or `triple-equals operator`).

```JavaScript
[, , , ,].includes(undefined)                // true
// Or [].includes(undefined)                 // true

[, , , ,].indexOf(undefined) > -1            // false
// Or [].indexOf(undefined)                  // false
```

Also for empty `array`, the `includes()` method returns `true` but `indexOf()` method returns `-1`.

**When to use?**

Usually suggest using the `includes()` method to check if the element is present in the `array` or `string`. And if we need to know where the element (character) is in the `array` or `string`, we need to use the `indexOf()` method.

**`Array.prototype.includes()` and `String.prototype.includes()`:**

```JavaScript
// ================================ Array ================================ //

const pets = ['cat', 'dog', 'bat'];

pets.includes('cat');                        // true
pets.includes('at');                         // false

// ---------------------------------------

[1, 2, 3].includes(2);                       // true
[1, 2, 3].includes(4);                       // false
[1, 2, 3].includes(3, 3);                    // false
[1, 2, 3].includes(3, -1);                   // true
[1, 2, NaN].includes(NaN);                   // true

// ---------------------------------------

// If the second argument is greater than or equal to the length of the array,
// false is returned. The array will not be searched.

let arr = ['a', 'b', 'c'];

arr.includes('c', 3);                        // false
arr.includes('c', 100);                      // false

// ---------------------------------------

// For negative values of the second argument it use arr.length + second argument
// (using the absolute value of fromIndex as the number of characters
// from the end of the array at which to start the search).

// If the computed index is less or equal than -1 * arr.length,
// the entire array will be searched.

// array length is 3
// the second argument is -100
// computed index is 3 + (-100) = -97

let arr = ['a', 'b', 'c']

arr.includes('a', -100);                     // true
arr.includes('b', -100);                     // true
arr.includes('c', -100);                     // true
arr.includes('a', -2);                       // false

// ================================ String =============================== //

const str = 'To be, or not to be, that is the question.'

str.includes('To be');                       // true
str.includes('question');                    // true
str.includes('nonexistent');                 // false
str.includes('To be', 1);                    // false
str.includes('TO BE');                       // false
str.includes('');                            // true

// ---------------------------------------

// If no string is explicitly provided for first argument, it will be coerced to
// "undefined", and this value will be searched for in entire string.

const str = 'To be, or not to be, undefined that is the question.'

str.includes();                              // true

// ---------------------------------------

// The includes() method is case sensitive.

'Blue Whale'.includes('blue');               // false

// ---------------------------------------

// If the second argument values lower than 0, or greater than str.length,
// the search starts at index 0 and str.length, respectively.

'hello world'.includes('o', -5);             // true
'hello world'.includes('o', 11);             // false

// The 'hello world'.length is equal to 11.
// The second statement is false because search is started at position 11,
// a position after the end of the string.
```

**`Array.prototype.indexOf()` and `String.prototype.indexOf()`:**

```JavaScript
// ================================ Array ================================ //

const beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

beasts.indexOf('bison');                     // 1
beasts.indexOf('giraffe');                   // -1
// start from index 2
beasts.indexOf('bison', 2);                  // 4

// ---------------------------------------

// If the second argument is greater than or equal to the array's length, -1 is returned,
// which means the array will not be searched. If the second argument is a negative number,
// it is taken as the offset from the end of the array.
// Note: if the provided index is negative, the array is still searched from front to back.
// If the provided index is 0, then the whole array will be searched.
// Default: 0 (entire array is searched).

var array = [2, 9, 9];

array.indexOf(2);                            // 0
array.indexOf(7);                            // -1
array.indexOf(9, 2);                         // 2
array.indexOf(9, -1);                        // 2
array.indexOf(2, -1);                        // -1
array.indexOf(2, -3);                        // 0

// ---------------------------------------

// How to find index of all occurrence of element in an array?

var indices = [];
var array = ['a', 'b', 'a', 'c', 'a', 'd'];
var element = 'a';
var idx = array.indexOf(element);

while(idx != -1) {
    indices.push(idx);
    idx = array.indexOf(element, idx + 1);
}

console.log(indices);                        // [0, 2, 4]


// ---------------------------------------

// How to find out if an element exists in the array or not,
// and if it wasn't there, update the array?

function updateVegetablesCollection (veggies, veggie) {

    if (veggies.indexOf(veggie) === -1) {
        veggies.push(veggie);
        console.log("New veggies collection is : " + veggies);
    } else if (veggies.indexOf(veggie) > -1) {
        console.log(veggie + " already exists in the veggies collection.");
    }

}

var veggies = ["potato", "tomato", "chillies", "green-pepper"];

updateVegetablesCollection(veggies, "spinach");
// New veggies collection is : potato,tomato,chillies,green-pepper,spinach

updateVegetablesCollection(veggies, "spinach");
// spinach already exists in the veggies collection.


// ================================ String =============================== //

const str = "The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?";

const searchTerm = "dog";
const indexOfFirst = str.indexOf(searchTerm);

console.log(indexOfFirst);
// 40

console.log(str.indexOf(searchTerm, (indexOfFirst + 1)));
//52

// ---------------------------------------

// If no string is explicitly provided for first argument, it will be coerced to
// "undefined", and this value will be searched for in entire string.

const str = "The quick brown fox jumps over the lazy dog. undefined If the dog barked, was it really lazy?";

console.log(str.indexOf());                  // 45

//or
"undefined".indexOf();                       // 0
"undefine".indexOf();                        // -1

// ---------------------------------------

// If the second argument values lower than 0, or greater than str.length,
// the search starts at index 0 and str.length, respectively.

"hello world".indexOf("o", -5);              // 4
"hello world".includes("o", 11);             // -1 (and with any number greater than 11)

// The 'hello world'.length is equal to 11.
// The second statement returns -1 because search is started at position 11,
// a position after the end of the string.

// ---------------------------------------

// An empty string for first argument produces strange results.
// If we have no second argument value, or any second argument value lower than
// the string's length, the returned value is the same as the second argument value:

"hello world".indexOf("");                   // returns 0
"hello world".indexOf("", 0);                // returns 0
"hello world".indexOf("", 3);                // returns 3
"hello world".indexOf("", 8);                // returns 8

// However, with any second argument value equal to or greater than the string's length,
// the returned value is the string's length:

"hello world".indexOf("", 11);               // returns 11
"hello world".indexOf("", 13);               // returns 11
"hello world".indexOf("", 22);               // returns 11

// In the former instance, JS seems to find an empty string just after the specified index value.
// In the latter instance, JS seems to be finding an empty string at the end of the searched string.

// ---------------------------------------

// The indexOf() method is case sensitive.

"Blue Whale".indexOf("blue");                // returns -1

// ---------------------------------------

// Note that 0 doesn't evaluate to true and -1 doesn't evaluate to false. Therefore, when checking
// if a specific string exists within another string, the correct way to check would be:

"Blue Whale".indexOf("Blue") !== -1          // true
"Blue Whale".indexOf("Bloe") !== -1          // false

// ---------------------------------------

"Blue Whale".indexOf("Blue");                // returns  0
"Blue Whale".indexOf("Blute");               // returns -1
"Blue Whale".indexOf("Whale", 0);            // returns  5
"Blue Whale".indexOf("Whale", 5);            // returns  5
"Blue Whale".indexOf("Whale", 7);            // returns -1
"Blue Whale".indexOf("");                    // returns  0
"Blue Whale".indexOf("", 9);                 // returns  9
"Blue Whale".indexOf("", 10);                // returns 10
"Blue Whale".indexOf("", 11);                // returns 10
```

---

## The `splice()`, the `slice()` and `split()` methods:

**Syntax:**

```JavaScript
array.splice(startIndex, [deleteCount], [itemToAdd1, itemToAdd2, ...])

arrayOrString.slice(startIndex, [endIndex])

array.split(separator, [limit])
```

**`splice()`**: This method can only be used on `arrays`. The `splice` method **mutates** the original `array`, by removing or adding elements from it, and returns removed elements (if it had removed any element).

**`slice()`:** This method can be used on both `arrays` and `strings`. It does **not mutate** the original `array` or `string`, and returns a **shallow copy** of a portion of an `array` into a **new `array`**, with all the selected elements from `begin` to `end` (or extracts a section of a `string` and returns it as a **new `string`**), and we should know that the `end` will **not** be included.

**`split()`:** This method turns a `string` into an `array` of `strings` by separating the string into substrings, using a specified separator `string` and returns an `array` of strings.

**`Array.prototype.splice()`:**

```JavaScript
// Inserts at index 1

const months = ["Jan", "March", "April", "June"];

console.log(months.splice(1, 0, "Feb"));     // []

console.log(months);                         // ["Jan", "Feb", "March", "April", "June"]

// Note: If second argument is 0 or negative, no elements are removed.
// In this case, you should specify at least one new element.

// ---------------------------------------

// Replaces 1 element at index 1

const months = ["Jan", "March", "April", "June"];

console.log(months.splice(1, 1, "Feb"));     // ["March"]

console.log(months);                         // ["Jan", "Feb", "April", "June"]

// ---------------------------------------

// Delete 2 element start from index 1

const months = ["Jan", "March", "April", "June"];

console.log(months.splice(1, 2));            // ["March", "April"]

console.log(months);                         // ["Jan", "June"]

// ---------------------------------------

// Delete elements from index 1 until end of array

const months = ["Jan", "March", "April", "June"];

console.log(months.splice(1));               // ["March", "April", "June"]

console.log(months);                         // ["Jan"]

// ---------------------------------------

// Start index from last of array: Replaces 1 element in last index

const months = ["Jan", "March", "April", "June"];

console.log(months.splice(-1, 1, "Feb"));    // ["June"]

console.log(months);                         // ["Jan", "March", "April", "Feb"]

// ---------------------------------------

// Start index from last of array: Remove to last elements of array

const months = ["Jan", "March", "April", "June"];

console.log(months.splice(-2));              // ["April", "June"]

console.log(months);                         // ["Jan", "March"]
```

**`Array.prototype.slice()` and `String.prototype.slice()`:**

```JavaScript
// ================================ Array ================================ //

// The index of end will not be included.
// The slice method doesn't mutate array.

const animals = ["ant", "bison", "camel", "duck", "elephant"];

console.log(animals.slice(2, 4));            // ["camel", "duck"]
console.log(animals.slice(2, 1));            // []
console.log(animals.slice(2, 2));            // []
console.log(animals.slice(2, 3));            // ["camel"]
console.log(animals.slice(2));               // ["camel", "duck", "elephant"]
console.log(animals.slice(-2));              // ["duck", "elephant"]
console.log(animals.slice(-2, -2));          // []
console.log(animals.slice(-3, -2));          // ["camel"]
console.log(animals.slice(-3, 3));           // ["camel"]

// ---------------------------------------

// Array-like objects:
// Convert Array-like objects / collections to a new Array

function list() {
    console.log(arguments)                   // Object { 0: 1, 1: 2, 2: 3 }
    return Array.prototype.slice.call(arguments)
}

let list1 = list(1, 2, 3);                   // [1, 2, 3]

// ================================ String =============================== //
// The character at the end index will not be included.
// Obviously the slice method doesn't mutate string.

const str = "The quick brown fox jumps over the lazy dog.";

console.log(str.length)                      // 44

console.log(str.slice(4, 9));                // "quick"
console.log(str.slice(4, 3));                // ""
console.log(str.slice(4, 4));                // ""
console.log(str.slice(4, 15));               // "quick brown"
console.log(str.slice(4));                   // "quick brown fox jumps over the lazy dog."
console.log(str.slice(-4));                  // "dog."
console.log(str.slice(-4, -4));              // ""
console.log(str.slice(-9, -5));              // "lazy"
console.log(str.slice(-9, 39));              // "lazy"
console.log(str.slice(4, 60));               // "quick brown fox jumps over the lazy dog."
```

**`String.prototype.split()`:**

```JavaScript
const str = "The brown fox.";

console.log(str.split(" "));                 // ["The", "brown", "fox."]
console.log(str.split(" ", 1));              // ["The"]
console.log(str.split(""));
// ["T", "h", "e", " ", "b", "r", "o", "w", "n", " ", "f", "o", "x", "."]
console.log(str.split("", 5));               // ["T", "h", "e", " ", "b"]
console.log(str.split());                    // ["The brown fox."]

// Important Note:
// Do NOT use empty string ("") as a separator specially with unicode characters.
// The best way for getting a string to a character array is using one of ES2015 features:

"𝟙𝟚𝟛".split("");                            // ["�", "�", "�", "�", "�", "�"]

[...'𝟘𝟙𝟚𝟛'];                                // ["𝟘", "𝟙", "𝟚", "𝟛"]
Array.from('𝟘𝟙𝟚𝟛');                         // ["𝟘", "𝟙", "𝟚", "𝟛"]
```

---

## Sorting by Name or Number:

The `sort()` method **mutate** array.

The compare `function` in `sort()` method is optional. But if omitted, the array elements are converted to strings, then sorted according to each character's Unicode code point value.

The compare `function` receives two parameters:

- If `compareFunction(a, b)` returns less than 0, sort `a` to an index lower than `b` (i.e. `a` comes first).
- If `compareFunction(a, b)` returns 0, leave `a` and `b` unchanged with respect to each other, but sorted with respect to all different elements. Note: the ECMAscript standard does not guarantee this behavior, thus, not all browsers (e.g. Mozilla versions dating back to at least 2003) respect this.
- If `compareFunction(a, b)` returns greater than 0, sort `b` to an index lower than `a` (i.e. `b` comes first).
- `compareFunction(a, b)` must always return the same value when given a specific pair of elements `a` and `b` as its two arguments. If inconsistent results are returned, then the sort order is undefined.

**Sorting by number:**

```JavaScript
const numbers = [4, 5, 10000, 50, 3, 27, 50]

numbers.sort((a, b) => a - b);

console.log(numbers);
// expected output: [3, 4, 5, 27, 50, 50, 10000]
```

**Sorting by name:**

```JavaScript
users.sort(function(a, b) {
    if(a.firstname < b.firstname) { return -1; }
    if(a.firstname > b.firstname) { return 1; }
    return 0;
})
```

```JavaScript
const names = ["Edward", "Sharpe", "and", "The", "robert", "Magnetic", "zeros"]

names.sort((a, b) => {
    var nameA = a.toUpperCase(); // ignore upper and lowercase
    var nameB = b.toUpperCase(); // ignore upper and lowercase

    if(nameA < nameB) return -1;
    else if(nameA > nameB) return 1;
    else return 0;
})

console.log(names);
// expected output: ["and", "Edward", "Magnetic", "robert", "Sharpe", "The", "zeros"]
```

---
