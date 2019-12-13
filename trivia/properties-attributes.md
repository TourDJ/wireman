
## HTML 中特性（attribute） 和 属性（property）差异

使用 Javascript 操纵 DOM 对象时，很容易混淆 `attribute` 和 `property` 这两个概念。

* `attribute` 是 HTML 中定义的，而 `property` 是 DOM 中定义的。
* `attribute` 的主要作用是初始化 DOM 的 `property`. 所以， 当 DOM 初始化完毕，`attribute` 的工作也做完了。
* `property` 的值是可以改变的，而 `attribute` 的永远不能被改变。

例如， 有一个 HTML标签：
```html
<div id="test" class="button" custom-attr="1"></div>
```

操作 attribute ：
```javascript
document.getElementById('test').attributes; 
// return: [custom-attr="hello", class="button", id="test"]
document.getElementById('test').getAttribute('custom-attr')   // 1
```

操作 property ：
```javascript
document.getElementById('test').foo = 1;    // set property: foo to a number: 1
document.getElementById('test').foo;        // get property, return number: 1
```

### 总结

摘录 [stackoverflow](https://stackoverflow.com/questions/6003819/what-is-the-difference-between-properties-and-attributes-in-html#answer-6004028) 一句简短而精辟的总结:

*The value property reflects the current text-content inside the input box, whereas the value attribute contains the initial text-content of the value attribute from the HTML source code.*

### 延伸阅读
[JavaScript: What's the difference between HTML attribute and DOM property?](https://joji.me/en-us/blog/html-attribute-vs-dom-property/)   
