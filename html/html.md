####  html5新特性

- HTMl5现在已经不是SGML的子集，主要是关于图像，位置，存储，多任务等功能的增加。
- 拖拽释放（Drag and  Drop）API
- 语义化更好的内容标签（header，nav,footer,aside,article,section）
- 音频、视频API（audio，video）
- 画布（Canvas）API
- 地理（GEOlocation）API
- 本地离线存储localstorage长期存储数据，浏览器关闭后数据不丢失；sesseionStorage的数据在浏览器关闭后自动删除
- 表单控件：calendar，data，time，email，URL，search
- 新的技术webworker,websocket,Geoloation 

> 移除的元素

纯表现的元素：basefont,big,center,font,s,strike,tt,u;
对可用性产生负面影响的元素：frame，frameset，noframe；

> 支持HTML5新标签：

  IE8/IE7/IE6支持通过document.createElement方法产生的标签，

```
可以利用这一特性让这些浏览器支持HTML5新标签，
 
当然最好的方式是直接使用成熟的框架、使用最多的是html5shim框架
 
   <!--[if lt IE 9]>
 
   <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
 
   <![endif]-->
 
如何区分： DOCTYPE声明\新增的结构元素\功能元素可以利用这一特性让这些浏览器支持HTML5的新标签，
```

当然最好的方式是直接使用成熟的框架，使用最多的是html5shim框架



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



- #### 行内元素有哪些？块级元素有哪些？空（void）元素有哪些？

> 首先：CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认display值，如div的display默认值是"block",则为”块级“元素；span默认为display属性值为”inline“，是”行内“元素。
>
> 1. 行内元素有：a b span img input select strong
>
> 2. 块级元素有：div ul li ol dl dd p h1
>
> 3. 常见的空元素有：
>
>    ------
>
>    <input><link><meta>鲜为人知的是：
>
>    
>
>    <base><command><embed><keygen><param><source><track>

- #### 页面导入样式时，使用link和@import有什么区别

> 1.link属于XHTML标签，除了加载CSS外，还能用于定义RSS，定义rel链接属性等作用；而@import是CSS提供的，只能用于加载CSS
> 2.页面被加载的时候，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载
> 3.import是css2.1提出的，只有IE5以上才能被识别，而link是XHTML标签，无兼容问题；

- #### 介绍一下你对浏览器内核的理解？

> 主要分为两部分：渲染引擎和js引擎
> 渲染引擎：负责取得网页的内容（HTML、XML、图像等等）、整理讯息（例如加入css等），以计算网页的显示方式，然后会输出至显示器或打印机。浏览器的内核的不同对于网页的语法解释会有不同，所以渲染的效果也不相同。
> js引擎：解释和执行javascript来实现网页的动态效果。
> 最开始渲染引擎和JS引擎并没有区分的很明确，后来JS引擎越来越独立，内核就倾向于只指渲染引擎。

- #### 常见的浏览器内核有哪些？

> Trident内核：IE，MaxThon，TT，The Word，360，搜狗，等
> Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
> Presto内核：Opera7及以上. [Opera内核原为：Presto，现为：Blink;]
> Webkit内核：Safari,Chrome等。 [ Chrome的：Blink（WebKit的分支）]

- #### html5有哪些新特性、移除了那些元素？如何处理HTMl5新标签的浏览器兼容问题？r如何区分HTML和HTML5？

> HTML5现在已经不是SGML的子集，主要是关于图像，位置，存储，多任务等功能的增加

> **新特性**
> 1.绘画canvas；
> 2.用于媒介回放的video和audio元素；
> 3.本地离线存储localStorage长期存储数据。浏览器关闭后数据不丢失；
> 4.sessionStorage的元素在浏览器关闭后自动删除；
> 5.语义化更好的元素内容：比如 article，footer，header，nav，section；
> 6.表单控件，calendar，data，time，email，url，search
> 7.新的技术webworker,websocket,Geolocation;

> **移除的元素**
> 1.纯表现的元素：base,font,big,center,font,s,strike,tt,u;
> 2.对可用性产生负面影响的元素：frame,frameset,noframes;

> **支持HTML5新标签**
> 1.IE8/IE7/IE6支持通过document.createElement方法产生的标签；
> 2.可以利用这一特性让这些浏览器支持HTML5新标签
> 3.浏览器支持新标签后，还需要添加标签默认的样式。
> 4.当然也可以直接用成熟的框架，比如html5shim；

```
 <!--[if lt IE 9]>
        <script> src="http://html5shim.googlecode.com/svn/trunk/html5.js"</script>
     <![endif]--
```

> 如何区分HTMl5
> DOCTYPE声明\新增的结构元素\功能元素

- #### 简述以下你对HTML语义化的理解？

> 1.用正确的标签做正确的事情；
> 2.html语义化让页面的内容结构化，结构更清晰，便于浏览器，搜索引擎解析；
> 3.即使在没有样式css情况下也以一种文档格式显示，并且是容易阅读的；
> 4.搜索引擎的爬虫也依赖于HTML标记俩确定上下文和各个关键字的权重，利于SEO；
> 5.使阅读源代码的人对网站更容易将网站分块，便于阅读和维护理解。

- #### HTML5的离线存储怎么使用，工作原理能不能解释一下？

> 在用户没有与因特网链接时，可以正常访问站点或应用，在用户与因特网链接时，更新用户机器上的缓存文件

> **原理**:HTML5的离线存储是基于一个新建的.appcache文件的缓存机制（不是存储技术），通过这个文件上的解析清单离线存储资源，这些资源就会向cookie一样被存储了下来。之后当网络处于离线状态时，浏览器会通过离线存储的数据进行页面展示。

> 如何使用： 1、页面头部像下面一样加入一个manifest的属性；
> 2、在cache.manifest文件的编写离线存储的资源； CACHE MANIFEST #v0.11 CACHE: js/app.js css/style.css NETWORK: resourse/logo.png FALLBACK: / /offline.html 3、在离线状态时，操作window.applicationCache进行需求实现。

- #### 浏览器是怎么对HTMl5的离线存储资源进行管理和加载的呢？

> **在线的情况下**：浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相关的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会从新下载文件中的资源并进行离线存储。 **离线的情况下**:浏览器就直接使用离线存储的资源。

- #### 请描述一下cookies，sessionStorage和localStorage的区别？

> cookie是网站为了表示用户身份而存储在用户本地终端（client side）上的数据(通常经过加密)。
> cookie数据始终在同源的http请求中携带（即使不需要），在浏览器和服务器间来回传递。
> sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。

> 存储大小：
> cookie数据大小不能超过4K.
> sessionStorage和localStorage虽然也有存储大小限制，但比cookie大很多，可以达到5M或更大。

> 有效时间：
> localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
> sessionStorage 数据在当前浏览器窗口关闭后自动删除。
> cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭

- #### iframe有哪些缺点？

> 1.iframe会阻塞主页面的onload事件
> 2.搜索引擎的检索程序无法解读这种页面，不利于SEO；
> 3.iframe和主页面共享连接池，而浏览器对相同域的连接有限制，所以会影响页面的并行加载
> 4.使用iframe之前需要考虑这两个缺点，如果需要使用iframe，最好是通过javascript动态给iframe添加src属性值，这样可以绕开以上两个问题

- #### label的作用是什么？是怎么用的？

> label标签来定义表单控制间的关系，当用户选择该标签时，浏览器会自动将焦点转到和标签相关的表单控件上。

```
<label for="Name">Number:</label>
<input type=“text“name="Name" id="Name"/>

<label>Date:<input type="text" name="B"/></label>
```

- #### HTML5的form如何关闭自动完成功能？

> 给不想要提示的form或者某个input设置为autocomplete=off。

- #### 如何实现浏览器内多个标签页的通信？

> WebSocket、ShareWorker；
> 也可以调用localStorage、cookie等本地存储方式；

> localsStorage另一个浏览上下文被添加、修改或删除时，它都会触发一个事件，我们通过监听事件，控制它的值来进行页面信息通信；
> 注意quirks:Safari在无痕模式下设置localStorage值时会抛出QuotaExceededError的异常

- #### webSocket如何兼容低浏览器

```
Adobe Flash Socket 、
ActiveX HTMLFile (IE) 、
基于 multipart 编码发送 XHR 、
基于长轮询的 XHR
```

- #### 页面可见性（Page Visibility API） 可以有哪些用途？

```
通过 visibilityState 的值检测页面当前是否可见，以及打开网页的时间等;
在页面被切换到其他后台进程的时候，自动暂停音乐或视频的播放；
```

- #### 如何在页面上实现一个原型的可点击区域？

> 1、map+area或者svg 2、border-radius 3、纯js实现 需要求一个点在不在圆上简单算法、获取鼠标坐标等等

- #### 实现不使用border画出1px高的线，在不同浏览器的标准模式与怪异模式下都能保持一致的效果

```
<div style="height:1px;overflow:hidden;background:red"></div>
```

- #### 网页验证码是干嘛的，是为了解决什么安全问题。

```
区分用户是计算机还是人的公共全自动程序。可以防止恶意破解密码、刷票、论坛灌水      
有效防止黑客堆某一特定注册用户用特定程序暴力破解方式进行不断的登录尝试
```

- #### title与h1的区别、b与strong的区别、i与em的区别？

```
title属性没有明确意义只表示是个标题，h1则表示层次明确的标题，对页面信息的抓取也有很大的影响；      
strong是标明重点内容，有语气加强的含义，使用阅读设备阅读网络时，<strong>会重度，而<B>是展示强调内容     
i内容展示为斜体，em表示强调的文本；

Physical Style Elements -- 自然样式标签
b, i, u, s, pre
Semantic Style Elements -- 语义样式标签
strong, em, ins, del, code
应该准确使用语义样式标签, 但不能滥用, 如果不能确定时首选使用自然样式标签
```