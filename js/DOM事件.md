# DMO 事件

##  一、问题

1. 基本概念：DOM事件的级别
2. DOM事件模型（冒泡补货）
3. DOM事件流（页面中接受事件的顺序）
4. 描述DOM事件捕获的具体流程
5. Event对象的常见应用
6. Dom操作方法
7. 什么是事件代理
8. attribute和property的区别是什么？
9. document.write()的用法
   

##  二、回答

###  1.基本概念：DOM事件的级别

    DOM事件事件类
    DOM1标准指定的时候没有涉及任何和事件相关的东西；
    
    事件级别
    DOM0 element.onclick=function(){};
    
    //ture,false指定是冒泡还是捕获,默认为false，为冒泡
    //IE attachEvent
    DOM2 element.addEventListener('click',function(){},false);
    //事件类型增加了很多；
    DOM3 element.addEventListener('keyup',function(){},false);

###  2.DOM事件模型

    捕获（从上往下）
    冒泡（从目标元素往上）

###  3.DOM事件流（页面中接受事件的顺序）

> 浏览器在为当前页面与用户做交互的过程中，比如点击了鼠标左键，这个左键是怎么传动到你的页面上，又怎么响应的。

    1.捕获阶段
    2.目标阶段   事件通过捕获到达目标元素
    3.冒泡阶段   从目标元素上传到Window对象

###  4.描述DOM事件捕获的具体流程

    第一个接受事件的对象是window；
    取得body标签：document.body;
    表示html节点：document.documentElement；
    
    捕获流程：window-->document-->html标签-->body-->父级元素-->子级元素...-->目标元素。
    冒泡流程；从目标元素一层一层最后到window完成一次冒泡的流程；

### 5.Event对象的常见应用

####  1.event.preventDefault();阻止默认行为

    a标签绑定了click事件，在响应函数中设置了preventDefault，就阻止了链接默认跳转的行为。

#### 2.event.stopPropagation();阻止冒泡

    父级元素、子元素都绑定有事件，单击子元素做一件事，单击父元素在做一件事；如果不阻止冒泡，单击子元素的范围的时候，根据冒泡的原理，父级元素也会被响应；

#### 3.event.stopImmediatePropagation();事件响应优先级

    一个按钮绑定了两个click事件1和2，想通过优先级的方式，第一个响应函数是a。第二个响应函数是b，依次注册了a，b两个事件。想让执行a之后完不再执行b了；a响应函数中加上上面代码，就能成功阻止b执行。

#### 4.event.currentTarget(currentTarget当前绑定事件的对象,指向添加监听事件的对象)

    把子元素的事件代理都转移到父元素中，只绑定一次事件就可以了。做响应的时候就要区分是哪个元素被触发。

#### 5.event.target(target是当前被点击的元素,指向触发事件监听的对象。) 

#### 6.自定义事件或者模拟事件（重要）

    eg：有一个按钮，增加一个事件，在别的地方触发这个事件，而不是用回调的方式处理；
    
    1.var eve=new Event('custom');
    //通过new Event声明了一个自定义事件，把eve这个事件当做普通事件对象，只不过这个事件是你定义的
    
    2.ev.addEventListener('custom',function(){
        console.log('hello custom');
    });//ev是一个dom节点，通过dom2这种事件注册的方式绑定这个事件名称；
    
    3. ev.dispatchEvent(eve);//最后触发就是用的这个dom节点，dispatchEvent这个api触发eve这个对象。

## 总结：

	Event的不足只能指定事件名，如果想要给这个事件加些数据，Event是做不到的；用customEvent;
	
	customEvent自定义事件的是一个方法；除了可以指定事件名，后边还可以跟一个object来做指定参数。这个参数是自定义的，所以用法是一样的。

### 6. Dom操作方法

> 文档对象模型(document object model)是用来表示和操作HTML和XML文档内容的基础API。Document类型代表了一个HTML或XML文档，document对象则是用来保存整个web页面的dom结构，在页面上所有的元素最终都会映射为一个dom对象。对页面节点的操作也是通过document对象中的方法来实现的。

- **document对象中常用的Dom操作方法有**

  ```
  getElementById();  
  getElementsByClassName()        
  querySlector();     
  getAttribute()
  ```

  

- 创建新节点

  ```
  createDocumentFragment()//创建一个DOM片段
  createElement()//创建
  createTextNode()//创建一个文本节点
  
  ```

- 添加、移除、替换、插入

  ```
  appendChild()
  removeChild()
  replaceChild()
  insertBefore()//并没有insertAfter
  ```

- 查找

  ```
  getElementsByTagName()//通过标签名称
  getElementsByName()//通过元素的Name属性的值（IE容错能力较强，会得到一个数组，其中包括id等于name的值）
  getElementById()//通过元素Id,唯一性
  ```

  

### 7. 什么是事件代理

> 事件代理（EVent Delegation）又称之为事件委托。是JavaScript中常用绑定事件的技巧。顾名思义，“事件代理”即是把原本需要绑定的事件委托给父元素。让父元素担当事件监听的职务。事件代理的原理是DOM元素的事件冒泡。使用事件代理的好处是可以提高性能。

### 8. attribute和property的区别是什么？

> property就是dom元素在js中作为对象拥有的属性。
>
> 所以
>
> 对于html的标准属性来说，attribute和property是同步的，是会自动更新的。
>
> 但是对于自定义的属性来说，他们是不同步的。



### 9. document.write()的用法

> document.write()方法可以用在两个方面：页面载入过程中用实时脚本创建页面内容，以及用延时脚本创建窗口或新窗口的内容。
>
> document.write只能重绘整个页面，innerHTMl可以只重绘页面的一部分。