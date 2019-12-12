
## HTML 中特性（attribute） 和 属性（property）差异

* `Attributes` 是 HTML 中定义的，而 `properties` 是 DOM 中定义的。
* `Attributes` 的主要作用是初始化 DOM 的 `properties`. 所以， 当 DOM 初始化完毕，`attributes` 的工作也做完了。
* `Property` 的值是可以改变的，而 `attribute` 的永远不能被改变。

### 总结

摘录 [stackoverflow](https://stackoverflow.com/questions/6003819/what-is-the-difference-between-properties-and-attributes-in-html#answer-6004028) 一句简短而精辟的总结:

*The value property reflects the current text-content inside the input box, whereas the value attribute contains the initial text-content of the value attribute from the HTML source code.*

### 延伸阅读
[JavaScript: What's the difference between HTML attribute and DOM property?](https://joji.me/en-us/blog/html-attribute-vs-dom-property/)   
