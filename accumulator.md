
### 累加器多种语言实现

我们想要写一个能够生成累加器的函数，即这个函数接受一个参数n，然后返回另一个函数，后者接受参数i，然后返回n增加了i后的值。     
We want to write a function that generates accumulators-- a function that takes a number n, and returns a function that takes another number i and returns n incremented by i.    

出处：[Revenge of the Nerds](http://www.paulgraham.com/icad.html)   

#### Common Lisp
```lisp
(defun foo (n)
　　　　(lambda (i) (incf n i)))
```

#### Javascript
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
#### Perl 5
```perl
sub foo {  
  my ($n) = @_;
  sub {$n += shift}
}
```

#### Smalltalk
```Smalltalk
foo: n                              
  |s|                      
  s := n.                          
  ^[:i| s := s+i. ]
```

#### Python
```python
def foo (n):
　　s = [n]
　　def bar (i):
　　　　s[0] += i
　　　　return s[0]
　　return bar
```

#### Java
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




