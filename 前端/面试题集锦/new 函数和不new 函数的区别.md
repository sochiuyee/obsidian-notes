
>[!INFO]  **new 和不 new的区别：**
>如果 new 了函数内的 this 会指向当前这个 person 并且就算函数内部不 return 也会返回一个对象。
>如果不 new，函数内的this指向window

>[!INFO] 
>instanceof 用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。
>
>语法：`object instanceof constructor`
	 `object`：某个实例对象
    `constructor`：某个构造函数

  
```js
function SnapPea(name) {
	this.name = name ;
}

var tick = new SnapPea('tick');
var tock = SnapPea('tock');
console.log((tick instanceof snapPea) && (tock instanceof snapPea));
// 请问输出是否为 true，如果是请简述理由。如果不是请修改代码使输出为 true.
false，没有用new 只是普通调用，返回的是undefined，tock是undefined
/*
* tick._proto_ === SnapPea.proptotype
*/
// 改造
function SnapPea(name) {
	let obj = {}
	obj._proto_ = SnapPea.prototype
	this.name = name ;
	return obj
}
```