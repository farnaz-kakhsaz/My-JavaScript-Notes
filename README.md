# My JavaScript Notes

> This is my random JavaScript notes ;)

---

## Difference between find() and filter() methodes:

Both of them use to search through an array although the `find()` method will stop after the first match, and it returns the actual item (value), but the `filter()` method will continue searching through the entire array, and it returns the new array with all the matching items. if the `find()` method doesn't find anything it will return `undefined`, while the `filter()` method will return an empty array `[]`.

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
