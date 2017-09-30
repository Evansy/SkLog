## 复杂类型数据包括，Object,Array,Function
> 复杂类型的数据，赋值给其他变量，不像基本类型数据，复杂类型数据赋值只是传递了内存地址，并没有传静态值过去，我们对赋值之后的变量操作会影响原始变量的值。
我们有时候，只想对原数据进行一次备份，并不想影响到原始数据，下面是项目中用到的复杂类型数据复制方法
#### Object
```js
// 浅复制
// assign复制objct，当里面的值为非基本类型是，复制的也是一个指针
var obj = {a: 1, b: [1, 5]};
var copyObj = obj;
copyObj.a = 5;
console.log(obj, copyObj);    // {a: 1, b: [1, 5]} {a: 1, b: [1, 5]}

var newObj = Object.assign({}, obj);
newObj.a = 2;
console.log(obj, newObject);    // {a: 1, b: [1, 5]} {a: 2, b: [1, 5]}
newObj.b[0] = 10;
console.log(obj, newObject);    // {a: 1, b: [1, 10]} {a: 2, b: [1, 10]}
// Object.assign属于ES5方法，对于不支持该属性的也有polyfill
var assign = Object.assign || function (target) {
	for (var i = 1; i < arguments.length; i++) {
		var source = arguments[i];
		for (var key in source) {
			if (Object.prototype.hasOwnProperty.call(source, key)) {
				target[key] = source[key];
			}
		}
	}
	return target;
};

// 深复制 简单方法(有弊端，数据受到JSON类型限制，无法传递function，会丢失原型链)
var obj = {a: 1, b: [1, 5]};
var newObj = JSON.parse(JSON.stringify({}, obj));

newObj.a = 2;
newObj.b[0] = 10;
console.log(obj, newObject);    // {a: 1, b: [1, 5]} {a: 2, b: [1, 10]}

// 深复制 递归实现
function deepClone(obj) {
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }
    if (obj instanceof Array) {
        var copy = [];
        for (var i = 0; i < obj.length; i++) {
            copy.push(obj[i]);
        }
        return copy;
    }
    if (obj instanceof Date) {
        var copy = new Date();
        copy.setTime(obj.getTime());
        return copy;
    }
    if (obj instanceof Object) {
        var copy = {};
        for (var key in obj) { //递归 
            if (obj.hasOwnProperty(key)) {
                copy[key] = deepClone(obj[key]);
            }
        }
        return copy;
    }
}
```

#### Array
```js
var arr = [1, 6, 9];
var copyArr = arr;
copyArr[1] = 5;
console.log(arr, copyArr);    // [1, 5, 9] [1, 5, 9]

var newArr = [].concat(arr);
newArr[2] = 2;
console.log(arr, newArr);     // [1, 5, 9] [1, 5, 2]
```