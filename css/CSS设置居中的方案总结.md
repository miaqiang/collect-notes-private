### 总结

### 参考：

- [16种方法实现水平居中垂直居中](https://juejin.im/post/58f818bbb123db006233ab2a)
- [CSS设置居中的方案总结-超全](https://juejin.im/post/5a7a9a545188257a892998ef)

##### 水平居中
1. text-align：center;
2. margin:0 auto;
3. with:fit-content;
4. flex
5. 盒模型
6. transform
7. 8两种不同的绝对定位方法

##### 垂直居中

1. 行内元素（单行文字垂直居中）:设置 line-height = height
2. 块级元素:绝对定位+margin:-(高度的一半)
3. 块级元素：绝对定位+transform
4. 块级元素：绝对定位+margin:auto
5. 块级元素：padding
6. 块级元素：dispaly:table-cell
7. 块级元素：display:felx
8. 块级元素:伪元素
9. 块级元素：calc()
10. 块级元素：inlie-block


我们发现，flex，盒模型，transform，绝对定位，这几种同时适用于水平居中和垂直居中


> 块级元素居中html代码部分
```
<div class="parent">
    <div class="child">child</div>
</div>
```

> 行内元素居中html代码部分

```
<div class="parent">
    <span class="child"></span>
</div>
```

### 水平居中

#### 1 行内元素 text-align:center;

```
.parent{
    text-align:center;
}
```

#### 2 块级元素width:xx; margin：0 auto;

```
.child{
    width:100px;
    margin:0 auto;
}
```
或者设置父元素 text-aligm:center;

```
.parent{
    text-align:center
}
```
#### 3 若子元素包含float:left属性，为了让子元素水平居中，则可让父元素宽度设置fit-content,并且配合margin,作如下设置：

```
.parent{
    width: -moz-fit-content;
    width: -webkit-fit-content;
    width:fit-content;
    margin:0 auto;
}
.child{
    float:left;
}
```
>  fit-content是css3中给width属性新加的一个属性值，它配合margin可以轻松实现水平居中，目前只支持Chrome和Firefox浏览器。

#### 4 使用flex布局，可以轻松的实现水平居中，子元素设置如下：
```
.child{
    display:flex;
    justify-content:center;
}
```

#### 5  使用flex 2009年版本, 父元素display: box;box-pack: center;如下设置:
```
.parent{
    display: -webkit-box;
    -webkit-box-orient: horizontal;
    -webkit-box-pack: center;
    display: -moz-box;
    -moz-box-orient: horizontal;
    -moz-box-pack: center;
    display: -o-box;
    -o-box-orient: horizontal;
    -o-box-pack: center;
    display: -ms-box;
    -ms-box-orient: horizontal;
    -ms-box-pack: center;
    display: box;
    box-orient: horizontal;
    box-pack: center;
}
```
#### 6 使用css3中新增的transform属性，设置如下

```
.parent{
    position:relative;
}
.child{
    position:absolute;
    left:50%;
    transform:translate(-50%,0);
}
```

> absolute生成绝对定位的元素，相对于static定位以外的第一个父元素进行定位。

#### 7 使用绝对定位方式，以及负值的margin-lfet，设置如下:
```
.parent{
    position:relative;
}
.child{
    position:absolute;
    width:固定;
    left：50%;
    margin-left:-0.5宽度;
}
```

#### 8 使用绝对定位方式，以及left:0;right:0;margin:0 auto;设置如下：

```
.child{
    position:absolute;
    width:固定;
    left:0;
    right:0;
    margin: 0 auto;
}
```

### 垂直居中

#### 1 行内元素（单行文字垂直居中） 

```
.parent{
    height:200px;
    line-height:200px;
    border:1px solid pink;
}
```

#### 2 块级元素：绝对定位（需要提前知道尺寸）
> 优点：兼容性不错    
> 缺点:需要提前知道尺寸，margin-top:-（高度的一半）；margin-left:-(宽度的一般);父元素空间不够时, 子元素可能不可见(当浏览器窗口缩小时,滚动条不出现时).如果子元素设置了overflow:auto, 则高度不够时, 会出现滚动条


```
.parnet{
    position:relative;
    height:200px;
    border:1px solid pink;
}
.child{
    width:80px;
    height:40px;
    position:absolute;
    left:50%;
    top:50%;
    margin-top:-20px;
    margin-left:-40px;
    border:1px solid blue;
}
```

#### 3 块级元素：绝对定位+transform

> 优点：不需要提前知道尺寸,代码量少    
> 缺点：兼容性不好，IE8不支持, 属性需要追加浏览器厂商前缀, 可能干扰其他 transform 效果, 某些情形下会出现文本或元素边界渲染模糊的现象.

```
.parent{
    postion:relative;
    height:200px;
    border:1px solid pink;
}
.child{
    position:absolute;
    left:50%;
    top:50%;
    transform:translate(-50%,-50%);
    border:1px solid blue
    
}
```

#### 4 块级元素：绝对定位+margin：auto;
> 优点：兼容性好    
> 缺点：需要知道尺寸，或者不设置尺寸（需要是图片这种自身包含尺寸的元素），都是居中显示的。没有足够空间时, 子元素会被截断, 但不会有滚动条.

```
.parent{
    postion:relative;
    height:200px;
    border:1px solid pink;
}
.child{
    position:absolute;
    left:0;
    top:0;
    right:0;
    bottom:0;
    margin:auto;
    border:1px solid blue
    
}
```

#### 5 块级元素：padiing
> 缺点:如果高度固定，需要提前计算尺寸

```
.parent{
    padding:5% 0;
}
.child{
    padding:10% 0;
}
```

#### 6 块级元素:display:table-cell

```
.parent{
    width:600px;
    height:200px;
    border:1px  solid pink;
    display:table;
}
.child{
    display: table-cell;
    vertical-align: middle;
    text-align: center;
}
```
或
```
.parent{
    height: 300px;
    width: 600px;
    border: 1px solid red;
    display: table-cell;
    vertical-align: middle;
    text-align: center;
    }
```

> 同样适用于多行文字居中

```
.parent {
    width: 400px;
    height: 300px;
    display: table-cell;        
    vertical-align: middle;
    border: 1px solid red;
}
.child {
    display: inline-block;
    vertical-align: middle;
    background: blue;
}


```

#### 7 块级元素:display:flex

> 优点:     
> 1.内容块的宽高任意, 优雅的溢出.    
> 2.可用于更复杂高级的布局技术中. 缺点：兼容性不好

```
.parent{
    width: 600px;
    height: 200px;
    border: 1px solid red;
    display: flex;
    align-items: center;
    justify-content: center;  /*水平居中*/
}

```

#### 8 块级元素：伪元素

```
.parent {
    width: 300px;
    height: 300px;
    border: 1px solid red;
    text-align: center;
}
.child {
    background: blue;
    width: 100px;
    height: 40px;
    display: inline-block;
    vertical-align: middle;
}
.parent::before {
    content: '';
    height: 100%;
    display: inline-block;
    vertical-align: middle;            
}


```



#### 9 块级元素：calc()



```
.parent {
    width: 300px;
    height: 300px;
    border: 1px solid red;
    position: relative;
}
.child {
    width: 100px;
    height: 100px;
    background: blue;
    padding: -webkit-calc((100% - 100px) / 2);
    padding: -moz-calc((100% - 100px) / 2);
    padding: -ms-calc((100% - 100px) / 2);
    padding: calc((100% - 100px) / 2);
    background-clip: content-box;
}

```



#### 10 块级元素:inline-block



html代码:
```
<div class="parent">
    <div class="child">child</div>
    <div class="brother">brother</div>
</div>
```
css代码：

```
.parent {
    width: 400px;
    height: 400px;
    border: 1px solid red;
    position: relative;
}
.child, .brother {
    display: inline-block;
    vertical-align: middle;
}
.child {
    background: blue;
    font-size: 12px;
}
.brother {
    height: 400px;
    font-size: 0;
}


```