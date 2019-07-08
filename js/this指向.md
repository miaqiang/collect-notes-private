- [嗨，你真的懂this吗](<https://github.com/YvetteLau/Blog/issues/6>)



> this的指向是由它所在函数调用的上下文决定的，而不是由它所在函数定义的上下文决定的

this的指向问题无疑是JavaScript语言中必须掌握的核心概念。上文提到，在执行上下文创建的阶段，就会创建this执向。而更细致的说，this的指向，是在函数被调用的时候确认的。

下面是this执行的4种场景：

1.如果一个函数中有this,但是它没有以对象方法的形式调用，而是以函数名的形式执行，那么this指向的就是全局对象。

```
funtion test(){
    console.log(this);
}
test()//window
```

2.如果一个函数中有this，并且这个函数是以对象方法的形式调用，那么this指向就是调用该方法的对象。

```
var obj={
    test:function(){
        console.log(this);
    }
}
obj.test()//obj
```

3.如果一个函数中有this，并且包含该函数的对象也同时被两一个对象所包含的，尽管这个函数是被最外层的对象所调用。this指向的也只是它上一级的对象。

```
var obj={
    test:{
        fun:function(){
            console.log(this);
        }
    }
}
obj.test.fun();//test
```

4.如果一个构造函数或类方法中有this，那么它指向由该构造函数或类创建出来的实例对象。

```
class Test{
    constructor(){
        this.test="test";//类实例
    }
    option(){
        console.log(this);//类实例
    }
}
```