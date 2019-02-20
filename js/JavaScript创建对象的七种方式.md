七种方式
1. 工厂模式
2. 构造函数模式
3. 原型模式
4. 组合使用构造函数模式和原型模式
5. 动态原型模式  =》 构造函数+动态原型
6. 寄生构造函数模式 =》工厂模式+new
7. 稳妥构造函数模式 =》工厂模式 去掉this

### 参考地址

- [JavaScript创建对象的七种方式](https://xxxgitone.github.io/2017/06/10/JavaScript%E5%88%9B%E5%BB%BA%E5%AF%B9%E8%B1%A1%E7%9A%84%E4%B8%83%E7%A7%8D%E6%96%B9%E5%BC%8F/)

> JavaScript创建对象的方式有很多，通过Object构造函数或对象字面量的方式也可以创建单个对象，显然这两种方式会产生大量的重复代码，并不适合量产。接下来介绍七种非常经典的创建对象的方式，他们也各有优缺点

### 1.工厂模式

```
function createPerson(name,job){
    var o=new Object();
    o.name=name;
    o.sayName=function(){
        consle.log(this.name)
    }
    return o;
}

var person1=createPerson('Jiang','student');
var person2=createPerson('X',"Doctor");
console.log(person1);
console.log(person2)
```

可以无数个调用这个工厂函数，每次都会返回一个包含两个属性和一个方法的对象

工厂模式虽然解决了创建多个相似对象的问题，但是没有解决对象识别的问题，即不能知道一个对象的类型

### 2.构造函数模式

```
function Person(name,job){
    this.name=name;
    this.job=job;
    this.sayName=function(){
        console.log(this.name);
    }
}

var person1=new Person('Jiang','student');
var person2=new Person('X','Doctor');
```

没有显示的创建对象，使用new来调用这个构造函数，使用new后会自动执行如下操作

- 创建一个新对象
- 这个新对象会被执行[[prototype]]链接
- 这个新对象会绑定到函数调用的this
- 返回这个对象

使用这个方式创建对象可以检测对象类型

```
person1 instanceof Object//true
person2 instanceof Person//true
```

但是使用构造函数创建对象，每个方法都要在每个实例上重新创建一次

### 3.原型模式

```
function Person(){

}
Person.prototype.name='Jiang';
Person.prototype.job='studeng';
Person.prototype.sayName=function(){
    console.log(this.name);
}
var person1=new Person();
```
将信息直接添加到原型对象上。使用原型的好处是可以让所有的实例对象共享它包含的属性和方法，不必再构造函数中定义对象实例信息。

更简单的写法

```
function Person(){

}
Person.prototype={
    name:'Jiang',
    job:'studeng',
    sayName:function(){
        console.log(this.name);
    }
}

var person1=new Person();
```

将Person.prototype设置为等于一个以对象字面量形式创建的对象，但是会导致.constructor不在指向Person了。

使用这种方式，完全重写了默认的Person.prototype对象，因此，.constructor也不会存在这里

    Person.prototype.constructor===Person//false


如果需要这个属性的话，可以手动添加

```
function Person(){

}
Person.prototype={
    constructor:Person,
    name:'Jiang',
    job:'studeng',
    sayName:function(){
        console.log(this.name);
    }
}

var person1=new Person();
```
不过这种方式还是不够好，应为constructor属性默认为不可枚举的，这样直接设置，它是可枚举的，所以可以使用，Object.defineProperty方法


```
Object.defineProperty(Person.prototype,'constructor',{
    enumerable:false,
    value:Person
})
```
#### 缺点

使用原型，所有的属性都将被共享，这是很大的有点，同样也会带来一些缺点


原型中所有属性实例是被很多实例共享的，这种共享对于函数非常适合。对于那些包含基本值的属性也勉强可以，毕竟实例属性可以屏蔽原型属性。但是引用类型值，就会出现问题了

```
function Person(){

}
Person.prototype={
    name:'jiang',
    friends:['shelby','Court']
}

var person1=new Person();
var person2=new Person();

person1.friends.push('Van');
console.log(person1.friends);
console.loh(person2.friends);

console.log(person1.friends===person2.friends)//true

```

friends存在于原型中，实例person1和person2指向同一个原型，person1修改了引用的数组，也会反应到实例person2中

### 4.组合使用构造函数模式和原型模式

这是使用最为广泛、认同度最高的一种创建自定义类型的方法。它可以解决上面那些模式的缺点

使用此模式可以让每个实例都会有自己的一份实例属性副本，但同时又共享着对方法的引用

这样的话，即使实例属性修改引用类型的值，也不会影响其他实例的属性值了

```
function Person(){
    this.name=name;
    this.friends=['Shelby','Court']
}

Person.prototype.sayName=function(){
    console.log(this.name)
}

var person1=new Person();
var person2=new Person();

person1.friends.push('Van');

console.log(person1.friends);
console.log(person2.friends);

console.log(person1.friends===person2.friends)//false
```

### 5.动态原型模式


动态原型模式将所有信息都封装在了构造函数中，初始化的时候，通过检测某个应该存在的方法时候有效，来决定是否需要初始化类型

```
function Person(){
    this.name=name;
    this.job=job;

    if(typeof this.sayName!=='function'){
        Person.protoytype.sayName=function(){
            console.log(this.name)
        }
    }
}

var person1=new Person('Jiang','student');

person1.sayName();
```

只有在sayName方法不存在的时候，才会将它添加到原型中。这段代码只会初次调用构造函数的时候才会执行。

此后原型已经完成初始化，不需要在做什么修改了

这里对原型所做的修改，能够立即在所有实例中得到反映

其次，if语句检查的可以是初始化之后应该存在的任何属性和方法，所以不必用一大堆的if语句检查每一个属性和方法，只要检查一个就行


### 6.寄生构造函数模式

这种模式的基本思想就是创建一个函数，该函数的作用仅仅是封装创建对象的代码，然后再返回新建的对象

```
function Person(name,job){
    var o=new Object()
    o.name=name;
    o.job=job;
    o.sayName=function(){
        console.log(this.name)
    }
    return o
}

var person1=new Person('Jiang','student');
person1.sayName();
```

这个模式，除了使用new操作符并把使用的包装函数叫做构造函数之外，和工厂模式几乎一样

构造函数如果不返对象，默认也会返回一个新的对象，通过在构造函数的末尾添加一个return语句，可以重写调用构造函数时返回的值

### 7.稳妥构造函数模式

首先明白稳妥对象所指的是没有公共属性，而且其他方法也不引用this。

稳妥对象最适合在一些安全环境中（这些环境会禁止使用this和new),或防止数据被其他应用程序改动时使用

稳妥构造函数模式和寄生模式类似，有两点不同：一是创建对象的实例方法不引用this，二是不使用new操作符调用构造函数

```
function Person(name,job){
    var o=new Object()
    o.name=name;
    o.job=job;
    o.sayName=function(){
        console.log(name)
    }
    return o
}

var person1=Person('Jiang','student');
person1.sayName();
```

和寄生构造函数模式一样，这样创建出来的对象和构造函数之间没有什么关系，instanceof 操作符对于他们没有意义