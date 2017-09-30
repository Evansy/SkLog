## Array常用操作
push,pop,shift,unshift老是不记得谁是谁。
* pop,push是对数组尾部进行操作，push是添加，pop自然就是删除咯。
* shift，unshift是对数组头部进行操作，shift删除的意思，unshift自然就是添加咯。

map, some, every, filter, forEach, reduce的区别也老是区分不开。
* 其实具体用法并没有很大区别，字段不同，永不不同场景看意思会比较明了（这段瞎写的，后面了解了补充）
* 目前知道的就是，forEach可以遍历dom结构。新版本浏览器可以直接使用arr.forEach，老版本需要用Array.forEach.call(arr, callback)
* 补充（2017.9.29）已经理解几种的区别

* map遍历一个数组并对数组中每个元素操作并返回新数组，返回的数组长度和原数组长度一致。
```js
let array = arr.map(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])

var arr = [1, 3, 5, 8];
var arrMap = arr.map(item => item > 3);
// arrMap => [false, false, true, true];
```

* some 检查数组是否有元素满足条件，只要有一个满足则返回true。
```js
let array = arr.some(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])

var arr = [1, 3, 5, 8];
var arrSome = arr.some(item => item > 3);
// arrMap => true;
var arrSome1 = arr.some(item => item > 8);
// arrMap => false;
```

* every 检查数组所有元素是否满足条件，只要有一个不满足则返回false。
```js
let array = arr.every(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])

var arr = [1, 3, 5, 8];
var arrSome = arr.every(item => item > 3);
// arrMap => false;
var arrSome1 = arr.every(item => item > 0);
// arrMap => true;
```

* filter遍历数组并返回数组中满足条件的元素
```js
let array = arr.filter(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])

var arr = [1, 3, 5, 8];
var arrMap = arr.filter(item => item > 3);
// arrMap => [5, 8];
```

* forEach与for循环表现一致，不会有返回值
```js
let array = arr.forEach(function callback(currentValue, index, array) { 
    // Return element for new_array 
}[, thisArg])

var arr = [1, 3, 5, 8];
var arrMap = arr.forEach(item => item > 3);
// arrMap => undefined;
```

* reduce遍历数组并将这一次的循环结果与下一次的循环结果相加
```js
var array = array.reduce(function(accumulator, currentValue, currentIndex, array), initialValue);

var arr = [0, 1, 2, 3, 4];
var arrMap = arr.reduce((accumulator, currentValue) => accumulator + currentValue);

| callback    | accumulator | currentValue | currentIndex | array           | return value |
| ----------- | ----------- | ------------ | ------------ | --------------- | ------------ |
| first call  | 0           | 1            | 1            | [0,1,2,3,4]     | 1            |
| second call | 1           | 2            | 2            | [0,1,2,3,4]     | 3            |
| third call  | 3           | 3            | 3            | [0, 1, 2, 3, 4] | 6            |
| fourth call | 6           | 4            | 4            | [0, 1, 2, 3, 4] | 10           |
// arrMap => 10;
```