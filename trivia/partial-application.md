
## 偏函数(Partial application)

In computer science, partial application (or partial function application) refers to the process of fixing a number of arguments to a function, producing another function of smaller arity.
在计算机科学中，偏函数是指固定一个函数的一些参数，然后产生另一个更少参数的函数。

Partial application can be described as taking a function that accepts some number of arguments, binding values to one or more of those arguments, and returning a new function that only accepts the remaining, un-bound arguments.

**示例**      

定义一个偏函数
```javascript
function partial(fn) {
    var args = [].slice.call(arguments, 1);
    return function() {
        var newArgs = args.concat([].slice.call(arguments));
        return fn.apply(this, newArgs);
    };
};
```
定义示例业务函数
```javascript
function add(a, b) {
    return a + b + this.value;
}
```
调用偏函数
```javascript
var result = partial(add, 1);
```
测试
```javascript
var value = 1;
var obj = {
    value: 2,
    addOne: addOne
}

obj.addOne(2); // 5
```

使用 bind 实现
```javascript
var addOne = add.bind(null, 1);
obj.addOne(2); // 4 
```
此时，this 👈 全局对象。


### 参考资料
[偏函数](https://www.cnblogs.com/guaidianqiao/p/7771506.html)      
[Javascript中bind()方法的使用与实现](https://segmentfault.com/a/1190000002662251)     
[函数式编程术语](https://github.com/shfshanyue/fp-jargon-zh)      
