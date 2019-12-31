
## Javascript 原型链

JavaScript 是基于原型的。我们创建的每个函数都有一个 prototype(原型) 属性，这个属性是一个指针，指向一个对象，而这个对象有一个指向一个原型对象的链，它的用途是包含可以由特定类型的所有实例共享的属性和方法。

![Javascript 原型链图](../images/javascript-proto.jpg])     

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

重写原型对象，会导致原型对象的 constructor 属性指向 Object ，导致原型链关系混乱，所以我们应该在重写原型对象的时候指定 constructor( instanceof 仍然会返回正确的值)
```javascript
Foo.prototype.constructor === Foo // false
```


