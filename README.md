# My JavaScript Notes

> This is my random JavaScript notes ;)

---

## The find() and the filter() methods:

**Similarities:** Both of them are only used for searching through an **array**, **not string**. And they will return actual value if the searching matched (`find()`) or an `array` with all the matching items (`filter()`), **not `true` or `false`**. Also we need to write a testing `function` for them.

**Differences:** The `find()` method will stop after the **first match**, and it returns the **actual item** (value), but the `filter()` method will continue searching through the entire `array`, and it returns the **new `array`** with all the matching items.

If the `find()` method doesn't find anything it will return **`undefined`**, while the `filter()` method will return an **empty `array`**.

Array.prototype.find():

```JavaScript
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);
// expected output: 12
```

Array.prototype.filter():

```JavaScript
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);
// expected output: [12, 130, 44]
```

---

## Sorting by Name or Number:

**Sorting by number:**

```JavaScript
const numbers = [4, 5, 10000, 50, 3, 27, 50]

numbers.sort((a, b) => a - b);

console.log(numbers);
// expected output: [3, 4, 5, 27, 50, 50, 10000]
```

**Sorting by name:**

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
