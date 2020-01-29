# My JavaScript Notes

> This is my random JavaScript notes ;)

---

## The find() and the filter() methods:

**Similarities:** Both of them are only used for searching through an **array**, **not string**. And they will return actual value (`find()`) or an `array` with all elements (`filter()`) if they satisfy the provided testing `function`, **not `true` or `false`**. Also we need to write a testing `function` for them.
It means those methods take a _`callback`_, and that _`callback`_ is invoked for each item in an `array`.

These methods do **not mutate** the `array` on which it is called, but the `function` provided to _`callback`_ can. If so, the elements processed by them are set before the first invocation of _`callback`_. Therefore:

- _`callback`_ will not visit any elements added to the `array` after the call to `find()` or `filter()` begins.
- If an existing, yet-unvisited element of the `array` is changed by _`callback`_, its value passed to the _`callback`_ will be the value at the time `find()` or `filter()` visit that element.
- Elements that are _`deleted`_ are still visited.

**Differences:** The `find()` method will stop after the **first match** with testing `function`, and it returns the **actual item** (value), but the `filter()` method will continue searching through the entire `array`, and it returns the **new `array`** with all the matching items.

If no element passed the test the `find()` method returns **`undefined`**, while the `filter()` method returns an **empty `array`**.

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

## The find() and the findIndex() methodes:

**Similarities:** Both of them are only used for searching through an **array**, **not string**. And they will return actual value (`find()`) or **index** (`findIndex()`) of the **first element** if they satisfy the provided testing function, **not `true` or `false`**. It means they will stop after the **first match** with testing `function`. Also we need to write a testing `function` for them.
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
    for (i = 2; i < num; i++ ) {
        if (num % i === 0) return false;
    }
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

## The includes() and the indexOf() methodes:

**Similarities:** Both of these methods can be used on `string` or `array` to find out whether the element is present in the `array` (`string`) or not. They don't return actual value. Also we don't need to write testing `function` (_`callback`_) for them, we just simply pass the value to them.

Both of this statement `myArray.includes('some value')` and `myArray.indexOf('some value') !== -1` do the same thing. Although the first statement (`includes`) is the syntactic sugar for the second statement (`indexOf`) which was an old way to write.

`.includes(valueToFind [, startSromThisIndex])`
`.indexOf(valueToFind [, startSromThisIndex])`

The second argument for both of them is optional and use from set which index to start the search. the default is 0.

```JavaScript
[-0].indexOf(0) > -1                         // true

[-0].includes(0)                             // true
```

Values of zero are all considered to be equal, regardless of sign. (That is, `-0` is considered to be equal to both `0` and `+0`), but `false` is not considered to be the same as `0`.

**Differences:** The `includes()` returns a `boolean` value — `true` or `false`. But `indexOf` doesn’t return a `boolean`. It returns the **first index** of the element (or character) found in the `array` (`string`), or it will return `-1` (which represents that the element or character is not found).

```JavaScript
[NaN].indexOf(NaN) > -1                      // false

[NaN].includes(NaN)                          // true
```

If `NaN` present in `array`, the `indexOf` method returns `-1` for `NaN` but on the other hand, `includes` method returns `true`.

The `indexOf()` compares valueToFind to elements of the `Array` using `strict equality` (the same method used by the `===` or `triple-equals operator`).

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
        console.log('New veggies collection is : ' + veggies);
    } else if (veggies.indexOf(veggie) > -1) {
        console.log(veggie + ' already exists in the veggies collection.');
    }

}

var veggies = ['potato', 'tomato', 'chillies', 'green-pepper'];

updateVegetablesCollection(veggies, 'spinach');
// New veggies collection is : potato,tomato,chillies,green-pepper,spinach

updateVegetablesCollection(veggies, 'spinach');
// spinach already exists in the veggies collection.


// ================================ String =============================== //

const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?';

const searchTerm = 'dog';
const indexOfFirst = paragraph.indexOf(searchTerm);

console.log(indexOfFirst);
// 40

console.log(paragraph.indexOf(searchTerm, (indexOfFirst + 1)));
//52

// ---------------------------------------

// If no string is explicitly provided for first argument, it will be coerced to
// "undefined", and this value will be searched for in entire string.

const paragraph = 'The quick brown fox jumps over the lazy dog. undefined If the dog barked, was it really lazy?';

console.log(paragraph.indexOf());            // 45

//or
"undefined".indexOf();                       // 0
"undefine".indexOf();                        // -1

// ---------------------------------------

// If the second argument values lower than 0, or greater than str.length,
// the search starts at index 0 and str.length, respectively.

'hello world'.indexOf('o', -5);              // 4
'hello world'.includes('o', 11);             // -1 (and with any number greater than 11)

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

## Sorting by Name or Number:

The `sort()` method **mutate** array.

**Sorting by number:**

```JavaScript
const numbers = [4, 5, 10000, 50, 3, 27, 50]

numbers.sort((a, b) => a - b);

console.log(numbers);
// expected output: [3, 4, 5, 27, 50, 50, 10000]
```

**Sorting by name:**

Suppose we have an array users. We may use users.sort and pass a function
that takes two arguments and compare them (comparator). It should returns:

- something negative if first argument is less than second (should be placed before the second in resulting array)
- something positive if first argument is greater (should be placed after second one)
- 0 if those two elements are equal.

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
