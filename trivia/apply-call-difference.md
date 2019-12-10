
## Javascript 中的 apply、call、bind

call、apply、bind 三者都是 JavaScript Function 的內建函数，他們与 this 的关系重大，除此之外，call & apply 可以作為调用 Function 的另一个手段，而 bind 则会返回一个经过包裹后的 Function 回来。

call、apply 是 ECMA-262 中老早就有的规范了，而 bind 是 es6 后才有的。

### 语法
call：

    fn.call(this, arg1, arg2..., argn)

apply：

    fn.apply(this, [arg1, arg2..., argn])

bind：

    fn.bind(this, arg1, arg2..., argn)

关于 call 和 apply 的使用区别，如果非要用一句简洁明了的话来阐述它，我就想引用 [stackoverflow](https://stackoverflow.com/questions/1986896/what-is-the-difference-between-call-and-apply) 上的一段解释：

*The difference is that apply lets you invoke the function with arguments as an array; call requires the parameters be listed explicitly. A useful mnemonic is "A for array and C for comma."*

示例
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

### 延伸阅读
[JavaScript - call，apply，bind](https://ithelp.ithome.com.tw/articles/10195896)       
[call(), apply() and bind() Methods in JavaScript](https://www.codingame.com/playgrounds/9799/learn-solve-call-apply-and-bind-methods-in-javascript)      
[How-to: call() , apply() and bind() in JavaScript](https://www.codementor.io/niladrisekhardutta/how-to-call-apply-and-bind-in-javascript-8i1jca6jp)     
[Understanding This, Bind, Call, and Apply in JavaScript](https://www.taniarascia.com/this-bind-call-apply-javascript/)     


### 参考资料
[apply](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)     
[call](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/call)    
[spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)        
