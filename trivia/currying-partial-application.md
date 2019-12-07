
## 函数柯里化(Currying)和偏函数应用(Partial Application)

> Currying：因为是美国数理逻辑学家哈斯凯尔·加里(Haskell Curry)发明了这种函数使用技巧，所以这样用法就以他的名字命名为Currying，中文翻译为“加里化”或“柯里化”。

### 函数柯里化(Currying)

Currying(柯里化) 是把一个接受 N 个参数的函数转换成接受一个单一参数（最初函数的第一个参数）的函数，并且返回接受余下的参数而且返回结果的新函数的技术。也就是说每个函数都接受1个参数。

#### 一个通用的 curry() 函数接口
```javascript
function curry(fn) {
    return function curried() {
        var args = [].slice.call(arguments);
        return args.length >= fn.length ?
            fn.apply(null, args) :
            function () {
                var rest = [].slice.call(arguments);
                return curried.apply(null, args.concat(rest));
            };
    };
}
```
说明：
* 第 2 行：我们的 curry 函数返回一个新的函数，在这个例子中是一个名为 curried() 的命名函数表达式。
* 第 3 行：每次此函数被调用时，我们在 args 中存储传递给它的参数；
* 第 4 行：如果参数的数量大于等于原始函数的数量，那么
* 第 5 行：返回使用所有参数调用的原始函数
* 第 6 行：否则，返回一个接受更多参数的函数，当被调用时，将使用之前传递的原始参数与传递给新返回的函数的参数结合在一起，再次调用我们的 curried 函数。

业务函数 `add` 
```javascript
function add(a,b,c) { 
    return a + b + c; 
} 
```
测试
```javascript
var curriedAdd = curry(add); 

curriedAdd(1)(2)(3);  // 6
curriedAdd(1)(2,3);   // 6
```

**支持对象**

使用我们的 curry() 函数作为一个 *方法修饰器* 似乎破坏了该方法所期望的对象上下文。我们必须保留原始的上下文，并确保并将其传递给已返回的 curried 函数的连续调用。
```javascript
function curry(fn) {  
    return function curried() {
        var args = [].slice.call(arguments), 
            context = this;
 
        return args.length >= fn.length ?
            fn.apply(context, args) :
            function () {
                var rest = [].slice.call(arguments);
                return curried.apply(context, args.concat(rest));
            };
    }
}
```
业务对象 `border`
```javascript
var border = {  
  style: 'border',
  generate: function(length, measure, type, color) {
    return [this.style + ':', length + measure, type, color].join(' ') +';';
  }
};
```
测试
```javascript
border.curriedGenerate = curry(border.generate);
 
border.curriedGenerate(2)('px')('solid')('#369')    // => "border: 2px solid #369;"
```

说明：一个 “[function decorator(函数装饰器)](http://raganwald.com/2013/01/03/function_and_method_decorators.html)” 是一个函数，它执行一个函数并返回它所执行的函数的修饰或修改版本。

## 偏函数应用(Partial Application)

Partial Application(偏函数应用) 是指使用一个函数并将其应用一个或多个参数，但不是全部参数，在这个过程中创建一个新函数。

在 JavaScript 中已经可以使用 Function.prototype.bind() 偏函数应用。
```javascript
function add(a, b, c) { return a+b+c; }  
add(2,4,8);  // 14
 
var test = add.bind(this, 2, 4);  
test(8);  // 14 
```

### 参考资料
[JavaScript 中的 Currying(柯里化) 和 Partial Application(偏函数应用)](https://www.html.cn/archives/7781)    
