# Data with position

Pseudo AST that contains data with its positions attached.
Its main goal is to work with the data from YAML and be able to report errors at specific locations.
Inspired by [pseudo-yaml-ast](https://github.com/yldio/pseudo-yaml-ast).

This module is a part of [litvis](https://github.com/gicentre/litvis).

## Usage example

```js
import { fromYaml, getPosition, getValue } from "data-with-position";

const dataWithPosition = fromYaml(`obj:
  arr:
  - nums:
    - 1
    - 2
    - 3
    strs:
    - '1'
    - '2'
    - '3'
  num: 1
  str: '1'
`);

console.log(getValue(dataWithPosition.obj.str));
// "1"

console.log(getValue(dataWithPosition.obj.num));
// 1

console.log(getValue(dataWithPosition.obj.arr[0].nums));
// [1, 2, 3]

console.log(getValue(dataWithPosition.obj.arr[0].strs));
// ["1", "2", "3"]

console.log(getPosition(dataWithPosition.obj.str));
// { start: { line: 12, column: 3 }, end: { line: 12, column: 11 } }

console.log(getPosition(dataWithPosition.obj.arr.0));
// { start: { line: 3, column: 5 }, end: { line: 11, column: 3 } }
```

Rows and columns in position are 1-indexed for compatibility with [unist Position](https://github.com/syntax-tree/unist#position).
