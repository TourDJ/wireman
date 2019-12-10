
## Javascript 中的 apply、call、bind

call、apply、bind 三者都是 JavaScript Function 的內建函数，他們与 this 的关系重大，除此之外，call & apply 可以作为调用 Function 的另一个手段，而 bind 则会返回一个经过包裹后的 Function 回来。

call、apply 是 ECMA-262 中老早就有的规范了，而 bind 是 es6 后才有的。

### 语法

ECMAScript 规范给所有函数都定义了 call 与 apply 两个方法，它们的应用非常广泛，它们的作用也是一模一样，只是传参的形式有区别而已。

call：
```javascript
fn.call(this, arg1, arg2..., argn)
```
call 方法第一个参数是作为函数上下文的对象，后面传入的是一个参数列表，而不是单个数组。

apply：
```javascript
    fn.apply(this, [arg1, arg2..., argn])
```
apply 方法传入两个参数：一个是作为函数上下文的对象，另外一个是作为函数参数所组成的数组。

在 EcmaScript5 中扩展了叫 bind 的方法，在低版本的 IE 中不兼容。它和 call 很相似，接受的参数有两部分，第一个参数是是作为函数上下文的对象，第二部分参数是个列表，可以接受多个参数。

bind：
```javascript
    fn.bind(this, arg1, arg2..., argn)
```
低版本浏览器没有 bind 方法，实现 bind 的一个 Polyfill：
```javascript
if (!Function.prototype.bind) {
    Function.prototype.bind = function () {
        var self = this,                        // 保存原函数
            context = [].shift.call(arguments), // 保存需要绑定的this上下文
            args = [].slice.call(arguments);    // 剩余的参数转为数组
            
        return function () {                    // 返回一个新函数
            self.apply(context,[].concat.call(args, [].slice.call(arguments)));
        }
    }
}
```
[MDN 中 bind] 的 Polyfill(https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)      
```javascript
// Does not work with `new funcA.bind(thisArg, args)`
if (!Function.prototype.bind) (function(){
  var slice = Array.prototype.slice;
  Function.prototype.bind = function() {
    var thatFunc = this, thatArg = arguments[0];
    var args = slice.call(arguments, 1);
    if (typeof thatFunc !== 'function') {
      // closest thing possible to the ECMAScript 5
      // internal IsCallable function
      throw new TypeError('Function.prototype.bind - ' +
             'what is trying to be bound is not callable');
    }
    return function(){
      var funcArgs = args.concat(slice.call(arguments))
      return thatFunc.apply(thatArg, funcArgs);
    };
  };
})();
```

### 示例

一个例子
```javascript
var list = [1, 5, 8];
function add() {
  return Array.from(arguments).reduce(function(sum, num) {
    return sum + num;
  });
}
console.log(add.call(null, 1, 2));			// 3
console.log(add.apply(null, list));			// 14
```
这里，用到了 [arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments), [Array.from()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/from), [array.reduce()](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 等语法。

### 总结

关于 call 和 apply 的使用，如果非要用一句简洁明了的话来阐述它，我就想引用 [stackoverflow](https://stackoverflow.com/questions/1986896/what-is-the-difference-between-call-and-apply) 上的一段解释：

*The difference is that apply lets you invoke the function with arguments as an array; call requires the parameters be listed explicitly. A useful mnemonic is "A for array and C for comma."*

### 延伸阅读
[JavaScript - call，apply，bind](https://ithelp.ithome.com.tw/articles/10195896)       
[call(), apply() and bind() Methods in JavaScript](https://www.codingame.com/playgrounds/9799/learn-solve-call-apply-and-bind-methods-in-javascript)      
[How-to: call() , apply() and bind() in JavaScript](https://www.codementor.io/niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp)     
[Understanding This, Bind, Call, and Apply in JavaScript](https://www.taniarascia.com/this-bind-call-apply-javascript/)     


### 参考资料
[apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)     
[call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)    
[spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)        
