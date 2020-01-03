
## Javascript 原型链

JavaScript 是基于原型的。我们创建的每个函数都有一个 prototype(原型) 属性，这个属性是一个指针，指向一个对象，而这个对象有一个指向一个原型对象的链，它的用途是包含可以由特定类型的所有实例共享的属性和方法。

### 原型和实例的关系
* 每一个构造函数都拥有一个 `prototype` 属性，这个属性指向一个对象，也就是原型对象
* 原型对象默认拥有一个 `constructor` 属性，指向指向它的那个构造函数
* 每个对象都拥有一个隐藏的属性 `__proto__`，指向它的原型对象

### 分析

```javascript
function Foo(){
  this.name = 'tom'
  this.age = 20
}

Foo.prototype.score = 90;

var foo1 = new Foo();
foo1.name   // "tom"
foo1.age    // 20
foo1.score  // 90
```

在已经创建了实例的情况下重写原型，会切断现有实例与新原型之间的联系。
```javascript
Foo.prototype = {
	birth: 20
}

foo1.score  // 90
foo1.birth  // undefined

var foo2 = new Foo();
foo2.birth  // 20
```

重写原型对象，会导致原型对象的 `constructor` 属性指向 Object ，导致原型链关系混乱。
```javascript
Foo.prototype.constructor === Foo // false
```

所以我们应该在重写原型对象的时候指定 `constructor`( `instanceof` 仍然会返回正确的值)。
```javascript
Foo.prototype = {
    constructor: Foo
}
```

### `constructor` 探究
```javascript
function A(name){
  this.name = name
}
A.prototype.toString = function(){
  return this.name
}
var a = new A('hehe')
```
分析一下 new A 到底发生了什么：
```javascript
var a = new A('hehe') 
```
=>
```javascript
var a = new Object();
a.__proto__ = A.prototype;
A.call(a, 'hehe');
```
A.call 的意思是先把A的this设置为a，然后执行A的body也就是 `this.name = name`。

`__proto__` 是内部 `[[Prototype]]` 。从 ECMAScript 6 开始，`[[Prototype]]` 可以通过 `Object.getPrototypeOf()` 和 `Object.setPrototypeOf()` 访问器来访问。这个等同于 JavaScript 的非标准但许多浏览器实现的属性 `__proto__`。

以下代码显示了 js 引擎如何获取属性的：
```javascript
function getProperty(obj, prop) {
  if (obj.hasOwnProperty(prop))
    return obj[prop]
 
  else if (obj.__proto__ !== null)
    return getProperty(obj.__proto__, prop)
 
  else
    return undefined
}
```

### 原型链

如果一个实例的原型对象等于另一个类型的实例，而那个实例的原型对象又等于其他类型的实例，如此层层递进，就构成了实例与原型的链条，这就是所谓的原型链。

![Javascript 原型链图](../images/javascript-proto.jpg)     

原型链大致分为：
* 原型链指向 `Function.prototype` 的函数们
* 原型链指向 `Object.propotype` 的对象们


### instanceof 运算符

instanceof 运算符可以用来判断某个构造函数的prototype属性是否存在另外一个要检测对象的原型链上。


### 参考资料
[理解JavaScript的原型链和继承](https://blog.oyanglul.us/javascript/understand-prototype.html)      
[彻底理解JavaScript原型](http://www.imooc.com/article/2088)      
[JavaScript原型链与继承](https://juejin.im/post/5daf0d205188252aa65beaf4)      
[Javascript – How Prototypal Inheritance really works](http://blog.vjeux.com/2011/javascript/how-prototypal-inheritance-really-works.html)       


