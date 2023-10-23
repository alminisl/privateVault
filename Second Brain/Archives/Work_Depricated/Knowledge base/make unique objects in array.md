```const arrayUniqueByKey = [...new Map(array.map(item =>
  [item[key], item])).values()];
  ```
  