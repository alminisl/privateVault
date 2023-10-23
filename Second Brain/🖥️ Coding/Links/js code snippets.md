
### Item to an array without mutation
```
const insert = (arr, index, newItem) => [
  ...arr.slice(0, index), // first half of array
  newItem,                // new item
  ...arr.slice(index)     // rest of array
];

const items = ['S', 'L', 'C', 'E']

const result = insert(items, 2, 'I');

console.log(result); // ["S", "L", "I", "C", "E"]
```
