文档对象模型(document object model)是用来表示和操作HTML和XML文档内容的基础API。Document类型代表了一个HTML或XML文档，document对象则是用来保存整个web页面的dom结构，在页面上所有的元素最终都会映射为一个dom对象。对页面节点的操作也是通过document对象中的方法来实现的。

document对象中常用的Dom操作方法有：  
getElementById();  
getElementsByClassName()        
querySlector();     
getAttribute()等

1. 创建新节点

       createDocumentFragment()//创建一个DOM片段
       createElement()//创建
       createTextNode()//创建一个文本节点

2. 添加、移除、替换、插入


    appendChild()
    removeChild()
    replaceChild()
    insertBefore()//并没有insertAfter

3.查找

    getElementsByTagName()//通过标签名称
    getElementsByName()//通过元素的Name属性的值（IE容错能力较强，会得到一个数组，其中包括id等于name的值）
    getElementById()//通过元素Id,唯一性


##  请解释什么是事件代理

事件代理（EVent Delegation）又称之为事件委托。是JavaScript中常用绑定事件的技巧。顾名思义，“事件代理”即是把原本需要绑定的事件委托给父元素。让父元素担当事件监听的职务。事件代理的原理是DOM元素的事件冒泡。使用事件代理的好处是可以提高性能。



## attribute和property的区别是什么？

property就是dom元素在js中作为对象拥有的属性。

所以

对于html的标准属性来说，attribute和property是同步的，是会自动更新的。

但是对于自定义的属性来说，他们是不同步的。

## document.write()的用法

document.write()方法可以用在两个方面：页面载入过程中用实时脚本创建页面内容，以及用延时脚本创建窗口或新窗口的内容。

document.write只能重绘整个页面，innerHTMl可以只重绘页面的一部分。