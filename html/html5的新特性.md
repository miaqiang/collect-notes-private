1. HTMl5现在已经不是SGML的子集，主要是关于图像，位置，存储，多任务等功能的增加。
2. 拖拽释放（Drag and  Drop）API
3. 语义化更好的内容标签（header，nav,footer,aside,article,section）
4. 音频、视频API（audio，video）
5. 画布（Canvas）API
6. 地理（GEOlocation）API
7. 本地离线存储localstorage长期存储数据，浏览器关闭后数据不丢失；sesseionStorage的数据在浏览器关闭后自动删除
8. 表单控件：calendar，data，time，email，URL，search
9. 新的技术webworker,websocket,Geoloation 


>移除的元素

纯表现的元素：basefont,big,center,font,s,strike,tt,u;
对可用性产生负面影响的元素：frame，frameset，noframe；

> 支持HTML5新标签：

  IE8/IE7/IE6支持通过document.createElement方法产生的标签，

    可以利用这一特性让这些浏览器支持HTML5新标签，
     
    当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架
     
       <!--[if lt IE 9]>
     
       <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
     
       <![endif]-->
     
    如何区分： DOCTYPE声明\新增的结构元素\功能元素可以利用这一特性让这些浏览器支持HTML5的新标签，
当然最好的方式是直接使用成熟的框架，使用最多的是html5shim框架