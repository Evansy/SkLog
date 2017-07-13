## Array常用操作
push,pop,shift,unshift老是不记得谁是谁。
* pop,push是对数组尾部进行操作，push是添加，pop自然就是删除咯。
* shift，unshift是对数组头部进行操作，shift删除的意思，unshift自然就是添加咯。

map, some, filter, forEach的区别也老是区分不开。
* 其实具体用法并没有很大区别，字段不同，永不不同场景看意思会比较明了（这段瞎写的，后面了解了补充）
* 目前知道的就是，forEach可以遍历dom结构。新版本浏览器可以直接使用arr.forEach，老版本需要用Array.forEach.call(arr, callback)