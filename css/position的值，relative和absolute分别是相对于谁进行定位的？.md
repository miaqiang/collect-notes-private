### position 有六个值：static、relative、absolute、fixed、inherit，sticky


#### absolute：生成绝对定位的元素，相对于最近一级的定位不是static的元素进行定位。
> 脱离了布局流，此时可以使用top，right，bottom，left但这些属性不再是相对于static时的位置，而是相对于content-box，相对其边框内边缘的，而不是其padding内边缘


#### fixed：（老IE不支持）生成绝对定位的元素，通常相对于浏览器窗口或frame进行定位。
> 它的模式与absolute相同，不过无论怎么拖动滚动条，它始终固定在屏幕的指定位置。在IE6中不支持这个属性；在IE7中支持这个属性，但需要指明DOCTYPE；top，right，bottom，left属性指相对于视口的。

#### relative：生成相对定位的元素，相对于其在普通流中的位置进行定位。
> 没有脱离布局流，此时可以使用top，right，bottom，left属性
 ```
 top和bottom共存时，使用top值，忽略bottom值；
 left和right共存时，使用left值，忽略right值；
 ```
> release是相对位置，指相对于元素的positionw位static时的位置：
```
- top相对于static下移多少像素（若top是负值，则上移）。
- right相对于static左移多少像素（若right是负值，则右移）。
- bottom相对于static上移多少像素（若bottom是负值，则下移）。
- left 相对于static右移多少像素（若left是负值，则左移）

```
> 使用relative之后
```
- 原来的空间不会被其他元素挤占
- 元素在最终位置时也不会挤占其他元素的空间，它浮动到其他元素的上方。
```

#### static：默认值。没有定位，元素出现在正常的流中，

   > 就是按正常的布局流从上到下从左到右布局，平常我们做网页时，没有指定position，也就表示使用static


#### sticky：生成粘性定位的元素，容器的位置根据正常文档流计算得出。
- inherit：继承父元素的position值

参考网址：[position 的 static、relative、absolute、fixed、inherit](http://blog.csdn.net/qq546937127/article/details/5989601)