
## CSS 中伪元素与伪类

css 官网对伪类与伪元素的描述：

*CSS introduces the concepts of pseudo-elements and pseudo-classes to permit formatting based on information that lies outside the document tree.*

### 伪类

伪类用于当已有元素处于的某个状态时，为其添加对应的样式，这个状态是根据用户行为而动态变化的。

伪类包含两种：状态伪类和结构性伪类。

#### 状态伪类
状态伪类是基于元素当前状态进行选择的。在与用户的交互过程中元素的状态是动态变化的，因此该元素会根据其状态呈现不同的样式。

常见的状态伪类主要包括：

* `:link` 应用于未被访问过的链接；
* `:hover` 应用于鼠标悬停到的元素；
* `:active` 应用于被激活的元素；
* `:visited` 应用于被访问过的链接，与:link互斥。
* `:focus` 应用于拥有键盘输入焦点的元素。

#### 结构性伪类
结构性伪类是 css3 新增选择器，利用dom树进行元素过滤，通过文档结构的互相关系来匹配元素，能够减少class和id属性的定义，使文档结构更简洁。

常见的包括：

* `:first-child` 选择某个元素的第一个子元素；
* `:last-child` 选择某个元素的最后一个子元素；
* `:nth-child()` 选择某个元素的一个或多个特定的子元素；
* `:nth-last-child()` 选择某个元素的一个或多个特定的子元素，从这个元素的最后一个子元素开始算；
* `:nth-of-type()` 选择指定的元素；
* `:nth-last-of-type()` 选择指定的元素，从元素的最后一个开始计算；
* `:first-of-type` 选择一个上级元素下的第一个同类子元素；
* `:last-of-type` 选择一个上级元素的最后一个同类子元素；
* `:only-child` 选择的元素是它的父元素的唯一一个子元素；
* `:only-of-type` 选择一个元素是它的上级元素的唯一一个相同类型的子元素；
* `:empty` 选择的元素里面没有任何内容。

### 伪元素
伪元素是对元素中的特定内容进行操作，而不是描述状态。它的操作层次比伪类更深一层，因此动态性比伪类低很多。

实际上，伪元素就是选取某些元素前面或后面这种普通选择器无法完成的工作。控制的内容和元素是相同的，但它本身是基于元素的抽象，并不存在于文档结构中。

常见的伪元素选择器包括：

* `:first-letter` 选择元素文本的第一个字（母）。
* `:first-line` 选择元素文本的第一行。
* `:before` 在元素内容的最前面添加新内容。
* `:after` 在元素内容的最后面添加新内容。

### 单冒号还是双冒号?
w3c标准中的描述如下：

*Please note that the new CSS3 way of writing pseudo-elements is to use a double colon, eg a::after { … }, to set them apart from pseudo-classes. You may see this sometimes in CSS. CSS3 however also still allows for single colon pseudo-elements, for the sake of backwards compatibility, and we would advise that you stick with this syntax for the time being.*

CSS3规范中的要求使用双冒号(`::`)表示伪元素，以此来区分伪元素和伪类，比如`::before`和`::after`等伪元素使用双冒号(::)，`:hover`和`:active`等伪类使用单冒号(`:`)。对于 CSS2 中已经有的伪元素，例如 :before，单冒号和双冒号的写法 ::before 作用是一样的。

为了向后兼容，我们建议你在目前还是使用单冒号的写法。


