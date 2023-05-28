---
title: 2023-05-28-筆記-When is the Use case Between Map and Reduce
tags:
  - JavaScript
categories:
  - JavaScript
abbrlink: 1054889874
---
前言：
In my mind, when I want to do something to API data , my intuition is always comes up with above two methods.Before we started, we can take a look at the purpose of `map` and `reduce` method 

<!-- more -->
---
參考資料：
- [mdn](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 
- [reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#counting_instances_of_values_in_an_object)
---
## Map
map will return a new array, and this new array length is same as original one. and it will not mutate original value.
Below is sample form [mdn](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 

```javascript
const numbers = [1, 4, 9];
const roots = numbers.map((item) => Math.sqrt(item));

console.log(numbers, roots);
// roots 現在是 [1, 2, 3]
/* numbers 還是 [1, 4, 9]，這證明了 map() 不會去變動到 numbers 的值，
   map 內部是做了 immutable 的機制，Array.prototype 底下的這些高階函式
   大多都具有這樣函數式編程裡非常注重的特性 - immutable，不會去改變資料
   來源本身原有的值
*/

```

### Use case of Map

1. when you want to iterate array but you only want some key data like below 

```javascript
const people = [
  { name: "Mike", items: ["hammer", "axe"] },
  { name: "Steve", items: ["rock", "stick"] },
];

const allItems = people.map((d) => d.items);

// console.log(allItems); [ [ 'hammer', 'axe' ], [ 'rock', 'stick' ] ]

```
先延續上面這個說法，我們通常想要資料結構是展開而非 `multi-dimensional`
這時我們通常就會使用 `flat` method 或是直接使用 `flatMap`

```javascript
const people = [
  { name: "Mike", items: ["hammer", "axe"] },
  { name: "Steve", items: ["rock", "stick"] },
];

const allItems = people.map((d) => d.items).flat();

// console.log(allItems);  [ 'hammer', 'axe' , 'rock', 'stick' ]


const flatMapItems = people.flatMap((d) => d.items);
// console.log(flatMapItems);  [ 'hammer', 'axe' , 'rock', 'stick' ]

```
1. Data transformation:

```javascript
const numbers = [1, 2, 3, 4, 5];

// Double each number using map
const doubledNumbers = numbers.map((num) => num * 2);

console.log(doubledNumbers); // Output: [2, 4, 6, 8, 10]
```

## Reduce
[reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce#counting_instances_of_values_in_an_object) is a method that will iterate an array and in most of case this method is used to aggregate elements. If I do not give reduce method initial value it will use first elements as initial value

### Use cases for reduce

1. Aggregation:

```javascript
const numbers = [1, 2, 3, 4, 5];

// Calculate the sum of all numbers using reduce
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);

console.log(sum); // Output: 15
```

2. Counting instances of values in an object:

```javascript
const countedNames = names.reduce((acc, curr) => {
  if (acc[curr]) {
    acc[curr] += 1;
  } else {
    acc[curr] = 1;
  }
  return acc;
}, {});
// countedNames is:
// { 'Alice': 2, 'Bob': 1, 'Tiff': 1, 'Bruce': 1 } 
```

3. Grouping objects by a property

```javascript
const people = [
  { name: "Alice", age: 21 },
  { name: "Max", age: 20 },
  { name: "Jane", age: 20 },
];

function groupBy(objectArray, property) {
  return objectArray.reduce((acc, obj) => {
    const key = obj[property];
    const curGroup = acc[key] ?? [];

    return { ...acc, [key]: [...curGroup, obj] };
  }, {});
}

const groupedPeople = groupBy(people, "age");
console.log(groupedPeople);
// {
//   20: [
//     { name: 'Max', age: 20 },
//     { name: 'Jane', age: 20 }
//   ],
//   21: [{ name: 'Alice', age: 21 }]
// }

```