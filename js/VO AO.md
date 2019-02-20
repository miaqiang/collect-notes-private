[深入理解JavaScript系列（12）：变量对象（Variable Object）](http://www.cnblogs.com/TomXu/archive/2012/01/16/2309728.html)


[深入理解JavaScript系列（13）：This? Yes,this!](http://www.cnblogs.com/TomXu/archive/2012/01/17/2310479.html) 看不懂
### VO 变量对象 AO 活动对象

```
alert(x); // function
 
var x = 10;
alert(x); // 10
 
x = 20;
 
function x() {};
 
alert(x); // 20
```
为什么第一个alert “x” 的返回值是function，而且它还是在“x” 声明之前访问的“x” 的？为什么不是10或20呢？因为，根据规范函数声明是在当进入上下文时填入的； 同意周期，在进入上下文的时候还有一个变量声明“x”，那么正如我们在上一个阶段所说，变量声明在顺序上跟在函数声明和形式参数声明之后，而且在这个进入上下文阶段，变量声明不会干扰VO中已经存在的同名函数声明或形式参数声明，因此，在进入上下文时，VO的结构如下：
```
VO = {};
 
VO['x'] = <reference to FunctionDeclaration "x">
 
// 找到var x = 10;
// 如果function "x"没有已经声明的话
// 这时候"x"的值应该是undefined
// 但是这个case里变量声明没有影响同名的function的值
 
VO['x'] = <the value is not disturbed, still function>
```
紧接着，在执行代码阶段，VO做如下修改：
```
VO['x'] = 10;
VO['x'] = 20;
```

### 参考网址
- [前端基础进阶（三）：变量对象详解](http://www.jianshu.com/p/330b1505e41d)



![](http://upload-images.jianshu.io/upload_images/599584-391af3aad043c028.png?imageMogr2/auto-orient/strip)

在介绍变量对象与活动对象前，首先我们需要更深入的理解执行上文的声明周期，执行上下文的声明周期分为两个阶段：

第一个阶段是创建阶段，每当JS引擎在执行一段可执行代码时，都会先进入创建阶段。该阶段会分别创建变量对象，建立作用域链，以及确定this的指向。作用域链和this指向会在后文阐述。

所谓变量对象就是用于存储在执行上下文中定义的变量和函数声明，在当前上下文中每找到一个变量声明，就会在变量对象中建立一个同名的属性，每找到一个函数声明，就会建立一个以函数名命名的属性，属性值则为指向该函数所在内存地址的引用。这些预先建立好的属性以及属性值，存储着该上下文所有的变量数据，为后续代码的执行奠定基础。

第二个阶段是执行阶段，当变量对象、作用域链、this指向都建立之后，执行上下文会进入到执行阶段。在该阶段中变量对象会转换为活动对象，此时活动对象中的属性都允许被访问，并且可以执行其他数据性的操作。

两者区别：

执行上下文处于创建阶段时，变量对象中的属性是不允许被访问的的。但是在进入到执行阶段后，变量对象转化为活动对象，并且里面的属性都允许被外界访问。其实两者都属于同一个对象，只是处于执行上下文的不同生命周期而已

```
console.log(foo); // function foo
function foo() { console.log('function foo') }
var foo = 20;
```

```
// 上例的执行顺序为

// 首先将所有函数声明放入变量对象中
function foo() { console.log('function foo') }

// 其次将所有变量声明放入变量对象中，但是因为foo已经存在同名函数，因此此时会跳过undefined的赋值
// var foo = undefined;

// 然后开始执行阶段代码的执行
console.log(foo); // function foo
foo = 20;


```

![](http://upload-images.jianshu.io/upload_images/599584-7d131cfe82a20d37.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

> 变量对象和活动对象有什么区别：他们其实都是同一个对象，只是处于执行上下文的不同生命周期。不过只有处于函数调用栈栈顶的执行上下文中的变量对象，才会变成活动对象。