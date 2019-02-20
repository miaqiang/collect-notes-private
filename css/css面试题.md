#### 1.清除浮动的方式有那些？那种方式你觉得最好
| 操作 | 对父级设置适合CSS高度                                        | 结尾处加空div标签 clear:both                                 | 父级div定义 伪类:after 和 zoom                               | 父级div定义 overflow:hidden                                  |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 原理 | 父级div手动定义height，就解决了父级div无法自动获取到高度的问题。 | 添加一个空div，利用css提高的clear:both清除浮动，让父级div能自动获取到高度 | IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题 | 因为overflow:hidden属性相当于是让父级紧贴内容，这样即可紧贴其对象内内容（包括使用float的div盒子），从而实现了清除浮动。【注意：必须定义width或zoom:1，同时不能定义height】 |
| 优点 | 简单，代码少，容易掌握                                       | 简单，代码少，浏览器支持好                                   | 简单，代码少，浏览器支持好，不容易出现怪问题                 | 浏览器支持好，不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等） |
| 缺点 | 只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题 | 不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不爽 | 代码多，不少初学者不理解原理，要两句代码结合使用，才能让主流浏览器都支持。 | 不能和position配合使用，因为超出的尺寸的会被隐藏。           |
| 建议 | 不推荐使用，只建议高度固定的布局时使用                       | 不推荐使用，但此方法是以前主要使用的一种清除浮动方法         | 推荐使用，建议定义公共类，以减少CSS代码。                    | 推荐没有使用position或对overflow:hidden理解比较深的情况使用  |
| 评分 | 2颗星                                                        | 3颗星                                                        | 4颗星                                                        | 3颗星                                                        |

* #### 介绍下一标准的CSS的盒子模型？低版本IE和盒子模型有什么不同？
>1.有两种，IE盒子模型，W3C盒子模型；   
>2.盒子模型：内容（content）、填充（padding）、边界（margin）、边框（border）；    
>3.区别：IE的content部分把border和padding计算了进去；

* #### CSS选择符有哪些？有哪些属性可以继承？
> 1.id选择器（#myid）   
> 2.类选择器（.myClassName）   
> 3.标签选择器（div，h1，p）    
> 4.相邻选择器（h1+p）   
> 5.子选择器（ul>li）   
> 6.后代选择器（li a）   
> 7.通配符选择器（*）   
> 8.属性选择器（a[rel="external"]）   
> 9.伪类选择器（a:hover,li:nth-child）

>**可继承的样式**：font-size 、font-family、color、ul li

>**不可继承样式**：border padding margin width height

* #### CSS优先级算法如何计算
>优先级就近原则，同权重情况下样式定义最近者为准；   
>载入样式以最后载入的定位为准；

>优先级为：!important>id>class>tag   
>important比内联优先级高

* #### CSS3新增伪类有哪些？
>**举例**:   
>p：first-of-type 选择属于其父类的首个<p>元素的每个<p>元素    
>p：last-of-type  选择属于其父类的最后<p>元素的每个<p>元素；

>p：only-of-type 选择属于其父类的唯一<p>元素的每个<p>元素                  
>p：only-child 选择属于其父类的唯一子元素的每个<p>元素                
>p：nth-child(2) 选择属于其父类的第二个子元素的每个<p>元素

>:after 在元素之前添加内容，也可以用来做清除浮动    :before 在元素之后添加内容     
>:enabled      
>:disabled 控制表单控件的禁用状态     
>:checked 单选框或复选框被选中

* #### 如何居中div？如何居中一个浮动元素？如何让绝对定位的div居中？
>给div设置一个宽度，然后添加margin：0 auto属性
```css
div{
    width:200px;
    margin:0 auto
 }
```
>居中一个浮动元素
>确定容器的宽高 宽500 高300的层    
>设置层的外边距
```css
div{
    width:500px;
    height:300px;//高度可以不设          
    margin:-150px 0 0 250px;        
    position:relative;//相对定位
    background-color：pink;//方便看效果
    left:50%;
    top：50%;
}
```
>让绝对定位的div居中
```css
div{
    position:absolute;
    width:1200px;
    background:pink;
    margin:0 auto;
    top:0;
    left:0;
    bottom:0;
    right:0;
}
```
* #### display有哪些值？说明他们的作用

>block 像块类型元素一样显示。    
>none 不显示    
>inline 像行内元素一样显示，   
>inline-block 像行内元素一样显示，但其内容像块类型元素一样显示。    
>list-item 像块类型元素一样显示，并添加样式列表标记   
>table 此元素会作为块级表格来显示   
>inherit 规定应该从父元素继承display属性的值

* #### position的值relative和absolute定位原点是？    
>**absolute** 生成绝对定位的元素，相对于值不为static的第一个父元素进行定位。

>**fixed**（老IE不支持）生成绝对定位的元素，相对于浏览器窗口进行定位。

>**relative** 生成相对定位的元素，相对于其正常位置进行定位 

>**static**默认值。没有定位，元素出现在正常的流中（忽略top,bottom,left,right,z-index）

>**inherit**规定从父元素继承position属性的值。

* #### CSS3有哪些新特性？
>新增各种CSS选择器 （：not（.input）：所有class不是input的节点）   
>圆角 （border-radius）    
>多列布局 （multi-column layout）    
>阴影和反射 (shadow\reflect)    
>文字特效 （text-shadow）   
>文字渲染（text-decoration）    
>线性渐变 （gradient）   
>旋转（transform）   
>增加了旋转，缩放，定位，倾斜，动画，多背景 transform:\scale(0.85,0.90)\ translate(0px,-30px)\ skew(-9deg,0deg)\Animation:

* #### 用纯CSS创建一个三角形的原理是什么？
>把上、左右、三条边隐藏掉（颜色为transparent）   
```css
div{
    width:0;
    height:0;
    border-width:20px;
    border-style:solid;
    border-color:transparent transparent red transparent；
}
```

* #### 一个满屏 品 字布局如何设计
>简单方式
>上面的div宽100%    
>下面的两个div分别宽50%    
>然后用float或者inline使其不换行即可

* #### 经常遇到的浏览器的兼容行有哪些？原因，解决方法是什么，常用hack的技巧？
>1.png24位的图片在IE6上出现背景，解决方法是做成png8    
>2.浏览器默认的margin和padding不同，解决方案是加一个全局的*{margin:0,padding 0}来统一    
>3.IE6双边距bug：块属性标签float后，又有横行的margin情况下，在IE6显示margin比设置大，浮动IE产生的双倍距离，解决方案是在float的标签样式控制中加入-_display：inline，将其转换为行内属性(_这个符号渐进识别的方法，从总体中逐渐排除局部)
> 首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。
>  接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。
>  css
>      .bb{
>          background-color:#f1ee18;/*所有识别*/
>          .background-color:#00deff\9; /*IE6、7、8识别*/
>          +background-color:#a200ff;/*IE6、7识别*/
>          _background-color:#1e0bd1;/*IE6识别*/
>      }     
>4.在IE下，可以使用获取常规属性的方法来获取自定义属性，也可以使用getAttribute（）获取自定义属性，FF中，只能通过getAttribute（）获取自定义属性。解决方法：统一用getAttribute（）获取自定义属性。    
>5.IE下，event对象有x,y属性，但是没有pageX,pageY属性；FF中，刚好相反      
>6.chrome中文界面下默认会将小于12px的文本强制按照12px显示，可以通过加入CSS属性-webkit-text-size-adjust：none解决。    
>7.超链接访问过后hover样式就不出现了，被点击访问过的超链接样式不存在hover和active了解决方法是改变css属性的排列顺序L-V-H-A :  a:link {} a:visited {} a:hover {} a:active {}

* #### li和li之间看不见的空白间隔是什么原因引起的？有什么解决方法？
>行框的排列会受到中间空白（回车\空格）等的影响，因为空格也属于字符，这些空白也会应用样式，占据空间，所以会有间隔，把字符大小设为0，就没有空格了。

* #### 为什么要初始化CSS样式
>因为浏览器的兼容性问题，不同浏览器对所有标签的默认值是不同的，如果没对CSS初始化往往会出现浏览器之间的页面显示差异。   
* #### absolute的containing block（容器块）计算方式和正常流有什么不同？
>无论属于那种，都要找到其祖先元素中最近的position值不为static的元素，然后再判断

>若此元素为inline元素，则containing block为能够包含这个元素生成的第一个和最后一个inline box的padding box（除margin，border外的区域）的最小矩形；     
>否则，则由这个祖先元素的paddingbox构成。     
>如果都找不到，则为initial containing block。

>补充      
>1.static(默认)/relative:简单来说就是它的父元素的内容框（即去掉padding的部分）      
>2.absolute:向上找最近的定位为absolute/relative的元素     
>3.fixed：她的containing block 一律为根元素（html/body），根元素也是initial containing block

* #### 什么是css预处理器/后处理器
>预处理器例如 LESS Sass Stylus用来预编译Sass或less，增强css代码的复用性。     
>还有层级、mixin、变量、循环、函数等，具有很方便的UI组件模块化开发能力，极大的提高工作效率     

>后处理器：PostCSS,通常被视为在完成的样式中根据css规范处理css，让其更有效，目前最常做的的是给CSS属性添加浏览器私有前缀，实现跨浏览器兼容性的问题。