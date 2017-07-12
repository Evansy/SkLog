## 复杂类型数据包括，Object,Array,Function
> 复杂类型的数据，赋值给其他变量，不像基本类型数据，复杂类型数据赋值只是传递了内存地址，并没有传静态值过去，我们对赋值之后的变量操作会影响原始变量的值。
我们有时候，只想对原数据进行一次备份，并不想影响到原始数据，下面是项目中用到的复杂类型数据复制方法
#### Object
```js
var obj = {a: 1};
var copyObj = obj;
copyObj.a = 5;
console.log(obj, copyObj);    // {a: 5} {a: 5}

var newObj = Object.assign({}, obj);
newObj.a = 2;
console.log(obj, newObject);    // {a: 5} {a: 2}
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


#### Function
> 暂未用到，后续补充