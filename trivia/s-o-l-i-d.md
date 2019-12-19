
## `S.O.L.I.D`：面向对象设计的 5 大原则

`S.O.L.I.D` 是面向对象设计（OOD）的五大基本原则的首字母缩写:
* S – 单一职责原则（Single-Resposibility Principle）
* O – 开放封闭原则（Open-Closed principle）
* L – 里氏替换原则（Liskov-Substituion Principle）
* I – 接口隔离原则（Interface-Segregation Principle）
* D – 依赖倒置原则（Dependecy-Inversion Principle）

### S.R.P（单一职责原则）原则

一个类应该有且只有一个去改变它的理由，这意味着一个类应该只有一项工作。

### 开放封闭原则

对象或实体应该对扩展开放，对修改封闭。

### 里氏替换原则

在对象 x 为类型 T 时 q(x) 成立，那么当 S 是 T 的子类时，对象 y 为类型 S 时 q(y) 也应成立。（即对父类的调用同样适用于子类）

### 接口隔离原则

不应强迫客户端实现一个它用不上的接口，或是说客户端不应该被迫依赖它们不使用的方法。

### 依赖反转原则

实体必须依靠抽象而不是具体实现。它表示高层次的模块不应该依赖于低层次的模块，它们都应该依赖于抽象。

### 参考资料
[S.O.L.I.D：面向对象设计的头 5 大原则](https://www.jianshu.com/p/b56e098575db)      
[S.O.L.I.D: The First 5 Principles of Object Oriented Design](https://scotch.io/bar-talk/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)      
