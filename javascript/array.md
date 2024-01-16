# Array
39个方法
## Array 创建方法

1. **构造函数**：
```javascript
let arr2 = new Array(1, 2, 3, 4, 5);  // [1, 2, 3, 4, 5]
let arr3 = new Array(3);  // 创建一个长度为3的空数组 [empty * 3] || [undefined, undefined, undefined]
```

2. **字面量方法**：

```javascript
let arr1 = [1, 2, 3, 4, 5]; // [1, 2, 3, 4, 5]
let arr2 = [1, 2, ]; // [1, 2]
let arr3 = []; // []
```

2. **from**： 将类数组（有索引和length）或者可迭代对象生成数组
```javascript
let arr1 = Array.from("Matt") // ['M', 'a', 't', 't']
const m = new Map().set(1, 2)
                   .set(3, 4);
const s = new Set().add(1)
                   .add(2)
                   .add(3)
                   .add(4);
let arr2 = Array.from(m); // [[1, 2], [3, 4]]
let arr3 = Array.from(s); // [1, 2, 3, 4]

// 浅拷贝
const a1 = [1, 2, 3, 4];
const a2 = Array.from(a1); // [1, 2, 3, 4]   a1 !== a2

// 迭代器
const iter = {
  *[Symbol.iterator]() {
    yield 1;
    yield 2;
    yield 3;
    yield 4;
} };
let arr4 = Array.from(iter); // [1, 2, 3, 4]

// 类数组
const arrayLikeObject = {
   0: 1,
   1: 2,
   2: 3,
   3: 4,
   length: 4
};
let arr5 = Array.from(arrayLikeObject); // [1, 2, 3, 4]
```

3. **of**： 将一组参数变成数组
```javascript
Array.of(1, 2, 3, 4) // [1, 2, 3, 4]
Array.of(undefined) // [undefined]
```

## Array 取值赋值
1. **索引**：
```javascript
[0, 1, 2][0] // 0
[0, 1, 2][1] // 1
```

2. **at**:
```javascript
[0, 1, 2].at(0) // 0
[0, 1, 2].at(1) // 1
[0, 1, 2].at(-1) // 2
```

3. **with**:
```javascript
[0, 1, 2].with(0, 2) // [2, 1, 2]
[0, 1, 2].with(1) // [0, undefined, 2]
[0, 1, 2].with(-1, 3) // [0, 1, 3]
```

## 检测数组
Array.isArray()
```javascript
Array.isArray([]) // true
```

## 迭代器方法
1. **keys、values、entries**：
```javascript
const a = ["foo", "bar", "baz", "qux"];

const aKeys = Array.from(a.keys()); // [0, 1, 2, 3]
const aValues = Array.from(a.values()); // ["foo", "bar", "baz", "qux"]
const aEntries = Array.from(a.entries()); // [[0, "foo"], [1, "bar"], [2, "baz"], [3, "qux"]]
```

## 复制填充
1. **fill**：往数组指定位置填充一个值
```javascript
[0, 0, 0, 0, 0].fill(5); // [5, 5, 5, 5, 5]
[0, 0, 0, 0, 0].fill(5, 3); // [0, 0, 0, 5, 5]
[0, 0, 0, 0, 0].fill(5, 1, 3); // [0, 5, 5, 0, 0]
// (-4 + arr.length)
[0, 0, 0, 0, 0].fill(5, -4, -1); // [0, 5, 5, 5, 0];
// 忽略超出边界
[0, 0, 0, 0, 0].fill(5, -10, -6); // [0, 0, 0, 0, 0]
[0, 0, 0, 0, 0].fill(5, 10, 15); // [0, 0, 0, 0, 0]
// 忽略反向索引
[0, 0, 0, 0, 0].fill(5, 4, 2); // [0, 0, 0, 0, 0]
// 部分可用。填充可用部分
[0, 0, 0, 0, 0].fill(5, 4, 10); // [0, 0, 0, 0, 5]

```

2. **copyWithin**：按照指定范围浅复制数组中的部分内容，然后将它们插入到指 定索引开始的位置
```javascript
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(5); // [0, 1, 2, 3, 4, 0, 1, 2, 3, 4]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(0, 5); // [5, 6, 7, 8, 9, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(4, 0, 3); // [0, 1, 2, 3, 0, 1, 2, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(2, 0, 6); // [0, 1, 0, 1, 2, 3, 4, 5, 8, 9] 
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(-4, -7, -3); // [0, 1, 2, 3, 4, 5, 3, 4, 5, 6]
//静默忽略超出数组边界、零长度及方向相反的索引范围
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(1, -15, -12); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(1, 12, 15); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(1, 4, 2); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
// 部分可用
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9].copyWithin(4, 7, 11); // [0, 1, 2, 3, 7, 8, 9, 7, 8, 9]

```

## 转换方法
1. **valueOf**：返回数组本身
```javascript
[1, 2, 3].valueOf() // [1, 2, 3]
```
2. **toString**：用逗号分隔的字符串。数组每一项调用toString获取string值
```javascript
[1,true,{}].toString() // '1,true,[object Object]'
```
3. **toLocaleString**：用逗号分隔的字符串。数组每一项调用toLocaleString获取string值
```javascript
let person1 = {
   toLocaleString() {
     return "Nikolaos";
   },
   toString() {
     return "Nicholas";
   }
};
let person2 = {
   toLocaleString() {
     return "Grigorios";
   },
   toString() {
     return "Greg";
   }
};
[person1, person2].toString(); // 'Nicholas,Greg'
[person1, person2].toLocaleString(); // 'Nikolaos,Grigorios'
```

4. **join**：用指定分隔符号连接数组。数组每一项调用toString获取string值
```javascript
[1,true,{}].join() // '1,true,[object Object]'
[1, , 3].join() // '1,,3'
[1, undefined, 3].join() // '1,,3'
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
].join() // '1,2,3,4,5,6,7,8,9'
[
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
].join() // '1,2,3;4,5,6;7,8,9'
```

## 栈、队列方法
1. **push**：在数组尾部增加一个或多个项，返回数组长度
```javascript
let arr1 = [];
let count = arr1.push(1, 2, 3);
console.log(arr1); // [1, 2, 3]
console.log(count); // 3

```
2. **pop**：删除数组最后一项，返回被删除的项
```javascript
let arr1 = [1, 2, 3, 4];
let item = arr1.pop();
console.log(arr1); // [1, 2, 3]
console.log(item); // 4
```
3. **unshift**：在数组头增加一个或多个项，返回数组长度
```javascript
let arr1 = [2, 3, 4];
let item = arr1.unshift(1);
console.log(arr1); // [1, 2, 3, 4]
console.log(item); // 4
```

4. **shift**：删除数组第一项，返回被删除的项
```javascript
let arr1 = [1, 2, 3, 4];
let item = arr1.shift();
console.log(arr1); // [2, 3, 4]
console.log(item); // 1
```

## 排序
1. **sort**：  改变原数组
```javascript
let values = [0, 1, 5, 10, 15];
values.sort(); // 对每一项实用toString后升序排序

function compare(value1, value2) {
   if (value1 < value2) {
     return -1; 
   } else if (value1 > value2) {
     return 1; // value1在后面
   } else {
      return 0; 
   }
}
let values = [0, 1, 5, 15, 10];
values.sort(compare); // [0, 1, 5, 10, 15]
console.log(values) // [0, 1, 5, 10, 15]

```

2. **toSorted**： 不改变原数组
```javascript
function compare(value1, value2) {
   if (value1 < value2) {
     return -1; 
   } else if (value1 > value2) {
     return 1; // value1在后面
   } else {
      return 0; 
   }
}
let values = [0, 1, 5, 15, 10];
values.toSorted(compare); // [0, 1, 5, 10, 15]
console.log(values) // [0, 1, 5, 15, 10];
```

3. **reverse**： 将数组反过来. 改变原数组
```javascript
[1, 3, 2, 4].reverse() // [4, 2, 3, 1]
```

4. **toReversed**： 将数组反过来. 不改变原数组
```javascript
[1, 3, 2, 4].toReversed() // [4, 2, 3, 1]
```

## 操作函数
1. **concat**： 创建当前数组副本，将参数加到数组副本末尾
```javascript
["red", "green", "blue"].concat("yellow", ["black", "brown"]) //  ['red', 'green', 'blue', 'yellow', 'black', 'brown']

```

2. **slice**： 创建一个包含原数组一个或者多个元素的数组
```javascript
['red', 'green', 'blue', 'yellow', 'black', 'brown'].slice(1); // ['green', 'blue', 'yellow', 'black', 'brown']
['red', 'green', 'blue', 'yellow', 'black', 'brown'].slice(1, 4); // ['green', 'blue', 'yellow']

```
3. **splice**： 删除、插入、替换一个活着多个元素
```javascript
let arr1 = ['red', 'green', 'blue', 'yellow', 'black', 'brown']
let result1 = arr1.splice(1, 1);
console.log(arr1); // ['red', 'blue', 'yellow', 'black', 'brown']
console.log(result1) // ['green']

let arr2 = ['red', 'green', 'blue', 'yellow', 'black', 'brown']
let result2 = arr2.splice(2, 0, 'white');
console.log(arr2); // ['red', 'green', 'white', 'blue', 'yellow', 'black', 'brown']
console.log(result2) // []

let arr3 = ['red', 'green', 'blue', 'yellow', 'black', 'brown']
let result3 = arr3.splice(3, 1, 'red', 'purple');
console.log(arr3); // ['red', 'green', 'blue', 'red', 'purple', 'black', 'brown']
console.log(result3) // ['yellow']
```

4. **toSpliced**： 删除、插入、替换一个活着多个元素. 不改变原始值
```javascript

```

## 搜索和位置方法
1. **indexOf**： 从第一个往后找，匹配值（全等）的索引
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].indexOf(4) // 3
[1, 2, 3, 4, 5, 4, 3, 2, 1].indexOf(4, 4) // 5
[1, 2, 3, 4, 5, 4, 3, 2, 1].indexOf(9) // -1
```

2. **lastIndexOf**： 从最后一个往前找，匹配值（全等）的索引
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].lastIndexOf(4) // 5
[1, 2, 3, 4, 5, 4, 3, 2, 1].lastIndexOf(4, 4) // 3
[1, 2, 3, 4, 5, 4, 3, 2, 1].lastIndexOf(9) // -1
```

3. **includes**： 从第一个往后找，看是否有匹配值（全等）
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].includes(4) // true
[1, 2, 3, 4, 5, 4, 3, 2, 1].includes(4, 4) // true
[1, 2, 3, 4, 5, 4, 3, 2, 1].includes(9) // false
```

4. **find**： 从第一个往后找，查找第一个匹配项
```javascript
const people = [
  {
    name: "Matt",
    age: 27 
  },
  {
    name: "Nicholas",
    age: 29
  } 
];
people.find((element, index, array) => element.age < 28); // {name: "Matt", age: 27}
```

5. **findIndex**： 从第一个往后找，查找第一个匹配项的索引
```javascript
const people = [
  {
    name: "Matt",
    age: 27 
  },
  {
    name: "Nicholas",
    age: 29
  } 
];
people.findIndex((element, index, array) => element.age < 28); // 0
```

## 迭代方法
1. **every**： 对数组每一项都运行传入的函数，如果对每一项函数都返回 true，则这个方法返回 true。
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].every((item, index, array) => item > 2); // false
```

2. **some**： 对数组每一项都运行传入的函数，如果有一项函数返回 true，则这个方法返回 true
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].some((item, index, array) => item > 2); // true
```

3. **filter**： 对数组每一项都运行传入的函数，函数返回 true 的项会组成数组之后返回。
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].filter((item, index, array) => item > 2); // [3, 4, 5, 4, 3]
```

4. **forEach**： 对数组每一项都运行传入的函数，没有返回值。
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].forEach((item, index, array) => item > 2); // undefined
```

5. **map**： 对数组每一项都运行传入的函数，返回由每次函数调用的结果构成的数组。
```javascript
[1, 2, 3, 4, 5, 4, 3, 2, 1].map((item, index, array) => item * 2); // [2, 4, 6, 8, 10, 8, 6, 4, 2]
```

## 归并方法
1. **reduce**： 从第一项开始。如果传入第二个参数，从第一项开始；否则从第二项开始，第一项是pre
```javascript
[1, 2, 3, 4, 5].reduce((prev, cur, index, array) => prev + cur); // 15
[1, 2, 3, 4, 5].reduce((prev, cur, index, array) => prev + cur, 2); // 17
```
2. **reduceRight**： 从最后一项开始。如果传入第二个参数，从倒数第一项开始；否则从倒数第二项开始，倒数第一项是pre
```javascript
[1, 2, 3, 4, 5].reduceRight((prev, cur, index, array) => prev + cur); // 15
[1, 2, 3, 4, 5].reduceRight((prev, cur, index, array) => prev + cur, 2); // 17
```

## 扁平化方法
1. **flat**： 扁平化数组，可用指定扁平化层级。undefined将被删除。返回一个新数组
```javascript
[1, 2, [3, 4]].flat(); // [1, 2, 3, 4]
[1, 2, [3, 4, [5, 6]]].flat(); // [1, 2, 3, 4, [5, 6]]
[1, 2, [3, 4, [5, 6]]].flat(2); // [1, 2, 3, 4, 5, 6]
[1, 2, [3, 4, [5, 6, [7, 8, [9, 10]]]]].flat(Infinity); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[1, , 3, ["a", , ["d", , "e"]]].flat(); // [1, 3, 'a', ["d", , "e"]]
[1, , 3, ["a", , ["d", , "e"]]].flat(2); // [1, 3, 'a', 'd', 'e']
```

2. **flatMap**： 入参是一个函数，函数返回值被一层扁平化组成一个新的数组
```javascript
[1, 2, 3, 4].flatMap((x) => [x * 2]); //  [2, 4, 6, 8]
```