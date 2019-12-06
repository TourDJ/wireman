
## 偏函数(Partial application)

In computer science, partial application (or partial function application) refers to the process of fixing a number of arguments to a function, producing another function of smaller arity.      
意思是：在计算机科学中，偏函数是指固定一个函数的一些参数，然后产生另一个更少参数的函数。

更通俗点：

Partial application can be described as taking a function that accepts some number of arguments, binding values to one or more of those arguments, and returning a new function that only accepts the remaining, un-bound arguments.

**示例一**      

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
* 调用偏函数
```javascript
var result = partial(add, 1);

var value = 1;
var obj = {
    value: 2,
    result: result
}

obj.result(2); // 5
```

* 使用 bind 实现
```javascript
var result = add.bind(null, 1);
obj.result(2); // 4 
```
此时，this 👈 全局对象。

**示例二**

偏函数中提供占位符。

```javascript
var _ = {};

function partial(fn) {
    var args = [].slice.call(arguments, 1);
    return function() {
        var position = 0, len = args.length;
        for(var i = 0; i < len; i++) {
            args[i] = args[i] === _ ? arguments[position++] : args[i]
        }
        while(position < arguments.length) args.push(arguments[position++]);
        return fn.apply(this, args);
    };
};
```

调用偏函数
```javascript
var subtract = function(a, b) { 
    return b - a; 
};

subFrom20 = partial(subtract, _, 20);

subFrom20(5);
```

### vue 中代码片段
```javascript
/**
 * Reduce the code which written in Vue.js for dispatch the action
 * @param {String} [namespace] - Module's namespace
 * @param {Object|Array} actions # Object's item can be a function which accept `dispatch` function as the first param, it can accept anthor params. You can dispatch action and do any other things in this function. specially, You need to pass anthor params from the mapped function.
 * @return {Object}
 */
export const mapActions = normalizeNamespace((namespace, actions) => {
  const res = {}
  if (process.env.NODE_ENV !== 'production' && !isValidMap(actions)) {
    console.error('[vuex] mapActions: mapper parameter must be either an Array or an Object')
  }
  normalizeMap(actions).forEach(({ key, val }) => {
    res[key] = function mappedAction (...args) {
      // get dispatch function from store
      let dispatch = this.$store.dispatch
      if (namespace) {
        const module = getModuleByNamespace(this.$store, 'mapActions', namespace)
        if (!module) {
          return
        }
        dispatch = module.context.dispatch
      }
      return typeof val === 'function'
        ? val.apply(this, [dispatch].concat(args))
        : dispatch.apply(this.$store, [val].concat(args))
    }
  })
  return res
})
```


### 参考资料
[偏函数](https://www.cnblogs.com/guaidianqiao/p/7771506.html)      
[Javascript中bind()方法的使用与实现](https://segmentfault.com/a/1190000002662251)     
[函数式编程术语](https://github.com/shfshanyue/fp-jargon-zh)      
