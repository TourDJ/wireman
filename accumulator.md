
### 累加器多种语言实现

我们想要写一个能够生成累加器的函数，即这个函数接受一个参数n，然后返回另一个函数，后者接受参数i，然后返回n增加了i后的值。     
We want to write a function that generates accumulators-- a function that takes a number n, and returns a function that takes another number i and returns n incremented by i.    

出处：[Revenge of the Nerds](http://www.paulgraham.com/icad.html)   

#### Common Lisp
Lisp 的实现很简短。
```lisp
(defun foo (n)
　　　　(lambda (i) (incf n i)))
```

#### Perl 5
在Perl语言中，你不得不手工提取参数。
```perl
sub foo {  
  my ($n) = @_;
  sub {$n += shift}
}
```

#### Smalltalk
在Smalltalk中，局部变量（lexical variable）是有效的，但是你无法给一个参数赋值，因此不得不设置了一个新变量，接受累加后的值。
```smalltalk
foo: n                              
  |s|                      
  s := n.                          
  ^[:i| s := s+i. ]
```

#### Javascript
Javascript 区分语句和表达式，所以你需要明确指定 return语 句，来返回一个值。
```javascript
function foo (n) {
    return function (i) {
        return n += i 
    } 
}
```
es6 箭头语法
```javascript
foo = n => i => n += i
```

#### Python
Python并不完全支持局部变量，你不得不创造一种数据结构，来接受n的值。而且尽管Python确实支持函数数据类型，但是没有一种字面量的表示方式（literal representation）可以生成函数（除非函数体只有一个表达式），所以你需要创造一个命名函数，把它返回。
```python
def foo (n):
　　s = [n]
　　def bar (i):
　　　　s[0] += i
　　　　return s[0]
　　return bar
```
Python 面向对象的写法
```python
　　def foo (n):
　　　　class acc:
　　　　　　def _ _init_ _ (self, s):
　　　　　　　　self.s = s
　　　　　　def inc (self, i):
　　　　　　　　self.s += i
　　　　　　　　return self.s
　　　　return acc (n).inc
```
或者
```python
　　class foo:
　　　　def _ _init_ _ (self, n):
　　　　　　self.n = n
　　　　def _ _call_ _ (self, i):
　　　　　　self.n += i
　　　　　　return self.n
```

#### Java
面向对象的语言少不了 Java，
```java
　　public interface Inttoint {
　　　　public int call (int i);
　　}

　　public static Inttoint foo (final int n) {
　　　　return new Inttoint () {
　　　　int s = n;
　　　　public int call (int i) {
　　　　s = s + i;
　　　　return s;
　　　　}};
　　}
```
这不符合要求，因为它仅适用于整数。



