### [地址](http://davidshariff.com/quiz/)
#### 问题1："1" + 2 + "3" + 4结果是？
>1234，加法优先级等同，从左往右，数字与字符串相加，数字转换为字符串进行运算，结果等同于："12"+"3"+4="123"+4="1234";

#### 问题2：4 + 3 + 2 + "1"结果是？
>答案：91，优先级同上，从左往右，等同于7+2+"1"="91".

#### 问题3：下列输出什么
```javastipt
var foo=1;
function bar(){
    foo=10;
    return;
    function foo(){}
}
bar();
console.log(foo);
```
>答案：1,function的定义会提前到当前作用域之前，所以等同于：
```javasctipt
var foo = 1;
function bar() {
    function foo() {}
    foo = 10;
    return;
}
bar();
console.log(foo);//1
```
>所以，在foo=10的时候，foo是有定义的，属于局部变量，影响不到外层的foo。

#### 问题4:下列输出什么
```javascript
function bar(){
    return foo;
    foo=10;
    function foo(){}
    var foo=11;
}
console.log(typeof bar());
```
>答案：function,JavaScript中函数声明优先于变量声明，等同于：
```javascript
function bar(){
    var foo;
    function foo(){}
    return foo;
    foo=10;
    foo=11;
}
console.log(typeof bar());
```
>解析:js中的function声明和var声明都会被提前，最终得到function，是因为function声明优先级大于var声明，而不是由return语句返回导致

#### 问题5：下列输出什么
```jvascript
var x=3;
var foo={
    x:2,
    baz:{
        x:1,
        bar:function(){
            return this.x;
        }
    }
}
var go=foo.baz.bar;
console.log(go());
console.log(foo.baz.bar());
```
>答：3，1this指向执行时刻的作用域，go的作用域是全局，所以相当于window，取到的就是window.x,也就是var x=3；这里定义的x。而foo.baz.bar()里面，this指向foo.baz,所以取到的是这个上面的x，也就是1；

#### 问题6：下列输出什么
```javascript
var x=4,
obj={
    x:3,
    bar:function(){
        var x=2;
        setTimeout(function(){
            var x=1;
            console.log(this.x);
        },1000);
    }
}
obj.bar();
```
>答：4,不管有这个setTimeout还是把这个函数立即执行，它里面这个function都是孤立的，this只能是全局的window，即使不延时，改成立即执行结果同样是4。

#### 问题7：下列输出什么
```javscript
x=1;
function bar(){
    this.x=2;
    return x;
}
var foo= new bar();
console.log(foo.x);
```
>答：2,这里主要问题是最外面x的定义，试试把x=1改为x={},结果会不同的（undefined），这是为什么呢？在把函数当做构造器使用的时候，如果手动返回了一个值，要看这个值是否是简单类型，如果是，等同于不写返回，如果不是简单类型，得到的就是手动返回的值。如果，不手写返回值，就会默认从原型创建一个对象用于返回。

#### 问题8：下列输出什么
```javascript
function foo(a){
    console.log(arguments.length);
}
foo(1,2,3)
```
>答：3,arguments取的实参的个数，而foo.length取的是形参的个数

#### 问题9：下列输出什么
```javascript
var foo = function bar() {};

console.log(typeof bar);
console.log(typeof foo);
```
>答：undefined,function

### 问题10：下列输出什么
```javascript
var arr=[];
arr[0]='a';
arr[1]='b';
arr.foo='c';
console.log(arr.length);
```
>答：2，数组的原型是Object，所以可以像其他类型一样附加属性，不影响其固有性质。

#### 问题11：下列输出什么
```javascript
function foo(a,b){
    arguments[0]=2;
    arguments[1]=22;
    console.log(a);
    console.log(b);
}
foo(1);
```
>答:2，undefined，实参可以直接从arguments数组中修改，没有传进来的参数不能修改

#### 问题12：下列输出什么
```javascript
function foo(){}
delete foo.length;
console.log(typeof foo.length);
```
>答：number ,foo.length是无法删除的，它在Function原型上，重点它的 configurable是false