

##  参考

- [ 从输入 URL 到页面加载完成的过程中都发生了什么事情？](https://www.jianshu.com/p/71cf7f69eca8)
- [从输入 URL 到页面加载完成发生了什么事](https://segmentfault.com/a/1190000002611809)
- [浏览器渲染原理及流程](https://www.cnblogs.com/slly/p/6640761.html)
- [TCP三次握手及四次挥手详解及常见面试题](https://blog.csdn.net/ZWE7616175/article/details/80432486)
- [http全过程](https://segmentfault.com/a/1190000007033157#articleHeader1)
- [基础概念](https://www.jianshu.com/p/408425a489dd)





分为4个步骤：

1. 当发送一个URL请求时，不管这个URL是Web页面还是web页面上每个资源的URL，浏览器都会开启一个线程来处理这个请求，同时在远程DNS服务器上启动一个DNS查询。这能使浏览器获得请求对应的IP地址
2. 浏览器与远程'web'服务器通过TCP三次握手协商来建立一个TCP/IP连接，该握手包括一个同步报文，一个同步应答报文和一个应答报文，这三个报文在浏览器和服务器之间传递，该握手首先由客户端尝试建立通信，而后服务器应答并接受客户端的请求，最后有客户端发出该请求已经被接受的报文
3. 一旦TCP/IP连接建立，浏览器会通过该连接向远程服务器发送“http”的get请求。远程服务器找到资源并使用HTTP相应返回该资源，值为200的HTTP相应状态表示一个正确的响应。
4. 此时，“web”服务器提供资源服务，客户端开始下载资源。

请求返回后，便进入了我们关注的前端模块    
简单来说，浏览器会解析HTML生成DOM Tree，其次会根据CSS生成css Rule Tree而JavaScript又可以根据DOM API操作DOM

