### display:none和visibility：hidden的区别？

> dispaly：none 隐藏对应的元素，在文档不居中不再给它分配空间，它各边的元素会合拢，就当他从来不存在。    
> visibility:hidden 隐藏对应的元素，但是在文档布局中仍保留原来的空间。

#### css中link和@import的区别是？

> 1.link属于html标签，而@import是css提供的；  
> 2 页面被加载时，link会同时被加载，而@import被引入的css会等到引用它的css文件被加载完后再加载；    
> 3 import只在IE5以上才能识别，而link是HTML标签，无兼容问题；  
> 4 link方式的样式的权重，高于@import的权重

### position：absolute和float属性的异同

- 共同点：对内联元素设置float和absolute属性，可以让元素脱离文档流，并且可以设置其宽高。
- 不同点：float仍会占据位置，absolute会覆盖文档流中的其他元素。


### 介绍一下box-sizing属性？
box-sizing属性主要用来控制元素的盒模型的解析模式。默认值是content-box。
- content-box：让元素维持W3C的标准盒模型。元素的宽度/高度由border+padding+content的宽度/高度决定，设置width/height属性指的是content部分的宽/高
- border-box：让元素维持IE传统盒模型（IE6以下版本和IE6-7的怪异模式）。设置width/height属性指的是border+padding+content

标准浏览器下，按照W3C规范对盒模型解析，一旦修改了元素的边框或内距，就会影响元素的盒子尺寸，就不得不重新计算元素的盒子尺寸，从而影响这个页面的布局。

### CSS选择符有哪些？哪些属性能继承？优先级算法如何计算？CSS3新增伪类有哪些？

1. id选择器（#myid）
2. 类选择器（.myclassname）
3. 标签选择器（div，h1,p）
4. 相邻选择器（h1+p）
5. 子选择器（ul>li）
6. 后代选择器（li a）
7. 通配符选择器（*）
8. 属性选择器（a[rel="external"]）
9. 伪类选择器（a:hover,li:nth-child）


优先级为：
！important>id>class>tag

important比内联优先级高，但内联比id要高

### css3新增伪类举例？

1. p:first-of-type 选择属于父元素的首个<p>元素的每个<p>元素。
2. p:last-of-type 选择属于其父元素的最后<p>元素的每个<p>元素。
3. p:only-of-type 选择属于父元素唯一的<p>元素的每个<p>元素。
4. p:only-child 选择属于父元素的唯一子元素的每个<p>元素。
5. p:nth-child(2) 选择属于父元素的第二个子元素的每个<p>元素
6. :enabled ：disabled控制表单控件的禁用状态。
7. :checked 单选框或复选框被选中。


### css3有哪些新特性？

1. css3实现圆角（border-radius）,阴影（box-shadow）,
2. 对文字加特效（text-shadow）,线性渐变（gradient），旋转(transform)
3. transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);//旋转,缩放,定位,倾斜
4. 增加了更多的css选择器，多背景 rgba
5. 在css3中唯一引入的伪元素是::selection
6. 媒体查询，多栏布局
7. border-image

css3中新增了一种盒模型计算方式：box-siziing。盒模型默认的值是content-box，新增的值是padding-box和border-box,几种盒模型计算元素宽高的区别如下：

content-box（默认）

布局所占宽度Width：

     Width=width+padding-left+padding-right+border-left+border-right

布局所占高度Height：

    Height=height+padding-top+padding-bottom+border-top+border-bottom

 padding-box:

 布局所占宽度Width：

     Width=width（包含padding-left+padding-right）+border-left+border-right

 布局所占高度Height:

    Height=height(包含padding-top+padding-bottom)+border-top+border-bottom

border-box

布局所占宽度Width:
    
    Width=width(包含padding-left+padding-right+border-left+border-right)

布局所占高度Height：
    
    Height=height（包含padding-top+padding-bottom+border-top+border-bottom）

#### 对BFC规范的理解？

BFC，块级格式化上下文，一个创建了新的BFC的盒子是独立布局的，盒子里面的子元素的样式不会影响到外面的元素。在同一个BFC的两个毗邻的块级盒在垂直方向（和布局方向有关系）的margin会发生折叠。
W3c CSS 2.1规范中的一个概念，它决定了元素如何对其内容进行布局，以及其他元素的关系和相互作用。
    
    