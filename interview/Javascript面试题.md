* ####  介绍js的基本数据类型
> Undefined、Null、Boolean、Number、String
* #### 介绍js有哪些内置对象
> Object 是JavaScript中所有对象的父对象   
> **数据封装类对象**：Object、Array、Boolean、Number和String    
> **其他对象**：Function、Argument、Math、Date、RegExp、Error
* #### 说几条写javascript的基本规范？
> 1.不要在同一行声明多个变量  
> 2.请使用===/!==来比较true/false或者数值   
> 3.使用对象字面量替代new Array这种形式   
> 4.不要使用全部函数  
> 5.Switch语句必须带有default分支  
> 6.函数不应该有时候有返回值，有时候没有返回值   
> 7.For 循环必须使用大括号   
> 8.If语句必须使用大括号   
> 9.for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污染
* #### JavaScript原型，原型链？有什么特点？
>每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时说的原型链的概念。

>**特点:** JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。

>当我们需要一个属性时，JavaScript引擎会先看当前对象中是否有这个属性，如果没有的话，就会查找他的prototype对象是否有这个属性，如此递推下去，一直检索到Object内建对象
```javascript
function Func(){}
Func.prototype.name="Sean";
Func.prototype.getInfo=function(){
    return this.name;
}
var person=new Func();//现在可以参考var person=Object.create(oldObject);
console.log(person.getInfo()); //"Sean"
console.log(Func.prototype);//Func { name="Sean", getInfo=function()}
```
* #### JavaScript中有几种类型的值？能画一下他们的内存图吗？
  **栈:** 原始数据类型（Undefined，Null，Boolean，Number，String）  
  **堆:** 引用数据类型（对象、数组和函数）          
  **两种类型的区别:**:存储位置不同
> 原始数据直接存储在栈（stack）中的简单数据段，占据空间小、大小固定，属于被频繁使用数据，所以放入栈中存储； 

> 引用数据类型存储在堆（heap）中的对象，占据空间大、大小不固定，如果存储在栈中，将会影响程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当 解释器寻找引用指时，会首先检索其在栈中的地址，取得地址后从堆中获得实体![image](https://camo.githubusercontent.com/d1947e624a0444d1032a85800013df487adc5550/687474703a2f2f7777772e77337363686f6f6c2e636f6d2e636e2f692f63745f6a735f76616c75652e676966)

* #### JavaScript如何实现继承
>1.构造继承  
>2.原型继承   
>3.实例继承   
>4.拷贝继承   

>原型prototype机制或applay和call方法去实现交简单，建议使用构造函数和原型混合方式。
```JavaScript
function Parent(){
    this.name='Wang';
}
function Child(){
    this.age=28;
}
Child.prototype=new Parent();//继承Parent，通过原型
var demo=new  Child();
console.log(demo.age);
console.log(demo.name);//得到被继承的属性
```
* #### JavaScript继承的几种方式实现？

参考：[构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance.html)，[非构造函数的继承](http://www.ruanyifeng.com/blog/2010/05/object-oriented_javascript_inheritance_continued.html)；

* #### JavaScript创建对象的几种方式？
> JavaScript创建对象简单来说，无非就是使用内置对象或者各自自定义对象，当然还可以用json；但写法有很多种，也能混合使用。

> 1.对象字面量的方式
```javascript
person={firstname:"mark",lastname:"yun"};
```
>2.用function来模拟无参数的构造函数
```javascript
function Person(){
    var person=new Person();//定义一个function，如果使用new"实例化"，该function可以看做是一个Class
    person.name='Mark';
    person.age=25;
    person.work=function(){
        console.log(person.name+'hello ');
    }
}
person.work();
```
>3.用function来模拟有参数的构造函数来实现（用this关键字定义构造的上下文属性）
```javascript
function Pet(name,age,hobby){
    this.name=name;
    this.age=age;
    this.hobby=hobby;
    this.eat=function(){
        console.log("我叫"+this.name+",我喜欢"+this.hobby+",是个程序员");
    }
}
var maidou=new Pet("麦兜",25,"coding");//实例化、创建对象
maidou.eat();//调用eat方法
```
>4.用工厂方式来创建(内置对象)
```javascript
var wcDog=new Object();
wcDog.name="旺财";
wcDog.age=3;
wcDog.work=function(){
    console.log("我是"+wcDog.name+'，汪汪汪...')
}
wcDog.work();
```
>5.用原型方式来创建
```javascript
function Dog(){}
Dog.prototype.name="旺财";
Dog.prototype.eat=function(){
    console.log(this.name+"是个吃货");
}
var wangcai=new Dog();
wangcai.eat();
```
>6.用混合方式来创建
```javascript
function Car(name,price){
    this.name=name;
    this.price=price;
}
Car.prototype.sell=function(){
    console.log("我是"+this.name+",我现在卖"+this.price+"万元")
}
var camry=new Car("凯美瑞",27);
camry.sell();
```
* #### javascript作用域链
> 全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。   
> 当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，直至全局函数，这种组织形式就是作用域链。

* #### 谈谈This对象的理解
>1.this总是指向函数的直接调用者（而非间接调用者）;    
>2.如果有new关键字，this指向new出来的那个对象；    
>3.在事件中，this指向触发这个事件的对象，特殊的是，IS中的attachEvent中的this总是指向全局对象window；
* #### eval是做什么的？
> 它的功能是把对应的字符串解析成js代码并执行    
> 应该避免使用eval，不安全，非常耗性能（2次，一次解析成js语句，一次执行）。    
> 由json字符串转换为JSon对象的时候可以用eval，var obj=eval（'（'+str+'）'）;
* #### 什么是window 对象？什么是document 对象？
>简单来说，document是window的一个对象属性。    
>Window对象表示浏览器中打开的窗口。    
>如果文档包含框架（frame或iframe标签），浏览器会为html文档创建一个window对象，并为每个框架创建一个额外的window对象。    
>所有的全局函数和对象都属于window对象的属性和方法。
>document对Document的只读引用

* #### null，undefined的区别
> null是一个表示"无"的对象，转为数值的时候为0；undefined是一个表示"无"的原始值，转换为数值时为NaN

>**undefined**    
>1.变量被生命了，但是没有赋值时，等于undefined。    
>2.调用函数时，应该提供的参数没有提供，该参数为undefined。    
>3.对象没有赋值的属性，该属性为undefined    
>4.函数没有返回值时，默认返回undefined    
>5.typeof undefined//undefined

>**null**   
>1.作为函数的蚕食，表示该函数的参数不是对象。   
>2.作为对象原型链的重点。   
>3.typeof null//object

>注意：在验证null时，一定要用===，因为==无法分别null和undefined
* #### call()和apply()的区别和作用
>apply()函数有两个参数：第一个参数是上下文，第二个参数是参数组成的数组。如何上下文是null，则使用全局对象代替。    
>如：function.apply(this,[1,2,3]);

>call()的第一个参数是上下文，后续是实例传入的参数序列。   
>如：function.call(this,1,2,3);

* #### JSON的了解
>JSON(javascript Object Notation)是一种轻量级的数据交换格式。它是基于javascript的一个子集。数据格式简单，易于读写，占用带宽小。    
>格式：采用键值对，例如：{"age":"12","name":"back"};

```javascript
JSON字符串转换为JSON对象:
var obj =eval('('+ str +')');
var obj = str.parseJSON();
var obj = JSON.parse(str);

JSON对象转换为JSON字符串：
var last=obj.toJSONString();
var last=JSON.stringify(obj);
```
* #### new操作符具体干了什么呢？
> 1.创建一个空对象，并且this变量引用该变量，同时还继承了该函数的原型。    
> 2.属性和方法被加入到this引用的对象中。    
> 3.新创建的对象由this所引用，并且最后返回隐式的this。
```javascript
{'age':'12','name':'back'}
```

* #### DOM怎样添加、移除、移动、赋值、创建和查找节点
* #### 写一个通用的事件侦听器函数。
* ####  ["1","2","3"].map(parseInt)答案是多少？
>[1,NaN,NaN]因为parseInt需要两个参数（val,radix）   其中radix表示解析时用的基数。    
>map传了三个（element,index,array）,对应的radix不合法导致解析失败。

* #### 事件是？IE和火狐的事件机制有什么区别？如何阻止冒泡？
> 1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被javascript侦测到的行为。    
> 2. 事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件。    
> 3. ev.stopPropagation()；(旧ie的方法ev。cancelBubble=true)

* #### 什么是闭包（closure）,为什么要用它
>闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数

>**闭包的特性**    
>1.函数内再嵌套函数    
>2.内部函数可以引用外层的参数和变量   
>3.参数和变量不会被垃圾回收机制回收
```javascript
//li节点的onclick事件都能正确的弹出当前被点击的li索引
 <ul id="testUL">
    <li> index = 0</li>
    <li> index = 1</li>
    <li> index = 2</li>
    <li> index = 3</li>
</ul>
<script type="text/javascript">
    var nodes = document.getElementsByTagName("li");
    for(i = 0;i<nodes.length;i+= 1){
        nodes[i].onclick = function(){
            console.log(i+1);//不用闭包的话，值每次都是4
        }(i);
    }
</script>
```
>执行say667()后,say667()闭包内部变量会存在,而闭包内部函数的内部变量不会存在
>使得Javascript的垃圾回收机制GC不会收回say667()所占用的资源
>因为say667()的内部函数的执行需要依赖say667()中的变量
>这是对闭包作用的非常直白的描述
```javascript
 function say667() {
    // Local variable that ends up within closure
    var num = 666;
    var sayAlert = function() {
        alert(num);
    }
    num++;
    return sayAlert;
}

 var sayAlert = say667();
 sayAlert()//执行结果应该弹出的667
```
* #### javascript代码中的"use strict"是什么意思？使用它区别是什么？
>use strict 是一种ECMAscript 5添加的（严格）运行模式，这种模式使得javascript在更严格的条件下运行         
>使编码更加规范化的模式，消除javascript语法的的一些不合理、不严谨之处，减少一些怪异行为。         
>默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值；       
>全局变量的显示声明，函数必须声明在顶层，不允许在非函数代码块内声明函数，argument.callee也不允许使用；
>消除代码运行的一些不安全之处，保证代码运行的安全，限制函数中的argument修改，严格模式下的eval函数的行为和非严格模式的也不相同；

>提高编译器效率，增加运行速度；
>为未来新版本的javascript标准做铺垫

* #### 如何判断一个对象是否属于某各类
>使用instanceof 
```javascript
  if(a instanceof Person){
       alert('yes');
   }
```
* ### javascript中，有一个函数，执行时对象查找时，永远不会查找原型，这个函数是？
>**hasOwnProperty**

>javascript中hasOwnProperty函数是返回一个布尔值，指出一个对象是否具有制定名称的属性。此方法无法检查该对象的原型链中是否有该属性，该属性必须是对象本身的一个成员。    
>使用方法：    
>object.hasOwnProperty(proname)    
>如果object具有指定名称的属性，那么javascript中hasOwnProperty函数方法返回true，反之返回false

* #### js延时加载的方式有哪些？
>defer和async、动态创建DOM方式（用的最多）、按需异步载入js

* #### Ajax是什么？如何创建一个Ajax
>ajax的全称：Asynchronous javascript And XMl    
>异步传输+JS+XML   
>所谓异步，在这里简单的解释就是：像服务器发送请求的时候，我们不必等待结果，而是同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验。

>1.创建XMLHttpRequest对象，也就是创建一个异步调用对象；    
>2.创建一个新的httpRequest对象，也就是创建一个异步调用对象；    
>3.设置响应http请求状态变化的函数；    
>4.发送http请求；   
>5.获取异步调用返回的数据；    
>6.使用javascript和dom实现局部刷新

* #### 同步和异步的区别?
>同步的概念应该是来自OS中关于同步的概念：不同进行为协同完成某项工作而在先后次序上调整（通过阻塞，唤醒等方式），同步强调的是顺序性，谁先谁后，异步则不存在这种顺序性。

>同步：浏览器访问服务器请求，用户看的到页面刷新，重新发送请求，等请求完，页面刷新，新内容出现，用户看到新内容，进行下一步操作。    
>异步：浏览器访问服务器请求，用户正常操作，浏览器后端进行请求，等请求完，页面不刷新，新内容也会出现，用户看到新内容。

* #### 如何解决跨域问题 [参考](http://blog.csdn.net/joyhen/article/details/21631833)
* #### 页面编码和被请求的资源编码如果不一致如何处理
* #### 模块化开发怎么做？
>立即执行函数，不暴露私有成员
```javascript
 var module1 = (function(){
    　　　　var _count = 0;
    　　　　var m1 = function(){
    　　　　　　//...
    　　　　};
    　　　　var m2 = function(){
    　　　　　　//...
    　　　　};
    　　　　return {
    　　　　　　m1 : m1,
    　　　　　　m2 : m2
    　　　　};
    　　})();
```
* #### document.write和innerHTMl的区别
>document.write只能重绘整个页面    
>innerHtml可以重绘页面的一部分

* #### DOM操作，怎样添加、移除、移动、复制、创建和查找节点？
>创建节点    
>  createDocumentFragment()    //创建一个DOM片段
>  createElement()   //创建一个具体的元素
>  createTextNode()   //创建一个文本节点
>（2）添加、移除、替换、插入
>  appendChild()
>  removeChild()
>  replaceChild()
>  insertBefore() //在已有的子节点前插入一个新的子节点
>（3）查找
>  getElementsByTagName()    //通过标签名称
>  getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
>  getElementById()    //通过元素Id，唯一性
* #### 检测浏览器版本有哪些方式？
>功能检测、userAgent特征检测

比如：navigator.userAgent
//"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_2) AppleWebKit/537.36
  (KHTML, like Gecko) Chrome/41.0.2272.101 Safari/537.36"