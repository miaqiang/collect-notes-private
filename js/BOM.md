浏览器对象模型（brower object model）是用于和浏览器窗口进行交互的对象，也可用于窗口与窗口之间的通信。它的核心对象是window，在window对象当中也提供了很多其他对象属性用于操作和管理浏览器的各个部分。常用的window对象属性有：

location对象：表示该窗口中当前显示的文档的URL。     
history独享：用于将窗口的历史浏览记录用文档和文档状态列表的形式表示。        
navidator:该对象包含了浏览器厂商和版本信息。        
Screen对象：它提供了有关窗口显示大小和可用的颜色数量信息      

常用的对话框也属于挂在在window对象上的方法：alert();confirm();prompt();