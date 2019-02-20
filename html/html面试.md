#### 1.  怎么区分html和html5？html5有哪些新特性？兼容性怎么样？如何处理兼容
(Q1)
HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
1. 绘画 canvas;
2. 用于媒介回放的 video 和 audio 元素;
3. 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失;
4. sessionStorage 的数据在浏览器关闭后自动删除;
5. 语意化更好的内容元素，比如 article、footer、header、nav、section;
6. 表单控件，calendar、date、time、email、url、search;
7. 新的技术webworker, websocket, Geolocation;

(Q2)
1. IE8/IE7/IE6支持通过document.createElement方法产生的标签，
2. 可以利用这一特性让这些浏览器支持HTML5新标签，
3. 浏览器支持新标签后，还需要添加标签默认的样式。
4. 当然也可以直接使用成熟的框架、比如html5shim，
  <!--[if lt IE 9]>
  <![endif]-->



#### 1.行内元素和 块级元素的区别？行内块元素兼容性怎么处理

| 比较                | 块级元素                                         | 行内元素                                                     |
| ------------------- | ------------------------------------------------ | ------------------------------------------------------------ |
| 常见元素            | div、p、form、ul、ol、li                         | span、strong、em                                             |
| 特性                | 独占一行，默认情况下，其宽度自动填满其父元素宽度 | 宽度不会独占一行，相邻行内元素会排列在同一行里，直到一行排不下，才会换行，其宽度随元素的内容而变化 |
| width height属性    | 可以设置，设置了宽度还是独占一行                 | 设置无效                                                     |
| margin和padding属性 | 可以设置                                         | 水平方向的margin 和padding都产生边距效果，竖直方的margin和padding向却不会产生效果 |
| 对应的display属性   | block                                            | inline                                                       |
| 切换                | display：inline  display：inline-block行内块元素 | dispaly：block display：inline-block 行内块元素              |
| 去掉内间距          | margin：0;padding 0;                             |                                                              |

