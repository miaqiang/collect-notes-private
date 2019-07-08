# JS页面性能类

## 一、问题

题目：

1.提升页面性能的方法有哪些？

2.和缓存相关的http头有哪些？能写出来几个？

## 二、  回答

## 1.提升页面性能的方法有哪些？

> 1)资源压缩合并，减少HTTP请求（资源传输的过程变小）
>
> 2)非核心的代码异步加载
>
> 3)利用浏览器缓存
>
> 4)使用CDN
>
> 5)预解析DNS



###  1). 资源压缩合并，减少HTTP请求（资源传输的过程变小）；



### 2).非核心的代码异步加载—异步加载的方式—异步加载的区别；

#### - 异步加载的方式：

- 1.动态脚本加载 

 js动态创建一个标签，把标签最后加到body或者head上去（追加到文档中实现加载）

```
 var loadScript=document.createElement('script');
 loadScript.setAttribute("type","text/javascript");
 loadScript.setAttribute('src',loadUrl);
 console.log(loadUrl)
 document.getElementsByTagName("head")[0].appendChild(loadScript);
```

- 2.defer 

	 <script src="./defer1.js" charset="utf-8" defer></script>

- 3.async

	 <script src="./defer1.js" charset="utf-8" async></script>



#### - 异步加载的区别

1.defer是在HTML解析完之后才会执行，如果是多个，按照加载顺序依次执行；

2.async是在加载完成之后立即执行，如果是多个，执行顺序和加载顺序无关；



####  - 异步加载原理：任何一个时刻都只能做一件事

1.defer:新加载的，在HTML解析完之前，是不会执行的，defer能保证按你的加载顺序依次执行；

2.async：哪个先回来，哪个先执行，和加载顺序无关；



### 3).利用浏览器缓存-缓存的分类-缓存的原理；

#### 1.缓存的分类 （强缓存与协商缓存）

> 缓存：对应文件在浏览器中存在的备份，把请求的东西缓存到本地了（本地磁盘中），浏览器下次请求相当于从本地磁盘读取文件，不需要去服务端获取。

-  1.强缓存

```
http协议头：
Expires       Expires:Thu,21 Jan 2017 23:39:02 GMT
Cache-Control      Cahe-Control : Max-age=3600

```

强缓存：在强缓存的时间范围内，不与服务端进行通信，直接获取本地资源渲染。Expires为绝对时间，为服务端的时间，传到客户端来，可能导致两边时间不一致，Cache-Control为相对时间，从取到资源的那一秒开始计算，在多少秒内不再去服务端请求资源。



```
HTTP协议头：
 在请求一个文件的时候，http头上（响应头上）会带两个东西（有可能是2个，也有可能是1个，根据服务器配置）；

 响应头中会有key，value 
 Expires  过期时间； value值表示的是绝对时间（服务器的绝对时间，这个时间是服务器下发的）
判断客户端当前的时候是不是这个时间，比较的时候是按浏览器本地的时间做比较，下发的是服务器端的时间，会有偏差；
 缺点：有可能客户端和服务器的时间不一致。

Cache-Control   value值   Max-age=3600（相对时间）
不管客户端和服务器时间是否一致，它最后是以客户端相对时间为止，时间单位是秒（拿到资源之后再3600s之内不会再去请求服务器，在这个时间之内直接去浏览器拿缓存）

*如果服务器两个时间都下发了，依哪个时间为准呢？
以后者相对时间为准（这个规定）

```

-  2.协商缓存

```
Last-Modified If-Modified-Since   Last-Modified:Wed,26 Jan 2017 00:35:11 GMT
Etag   If-None-Match    
```

协商缓存：浏览器发现本地有这个副本，但是又不确定用不用他，去服务端问一下这个文件是否可用（浏览器与服务端协商）

**Last-Modified:**

```
Last-Modified(服务器下发的上次修改的时间)

    在拿到这个文件的时候，浏览器会给这个资源文件的http响应头中加一个Last-Modified，value值就是时间；
  If-Modified-Since:(请求中给服务器带的，服务器要对比，所以一来一回，两个东西)
    当强缓存失效（过期了），浏览器在这个时间之外又开始请求了，不确定这个东西有没有变化，要携带上次给的时间是哪一个，请求的时候会以携带这个字段的时间。（拿到新资源文件，会通过Last-Modified下发一个时间，当下次请求问服务器这个资源有没有发生变化，是用http请求
     头中加If-Modified-Since（key值），他们两个值是一个）
*缺点：虽然hash值变了，内容并没有变化，完全可以从副本拿，Etag就是解决这个问题的。

```

**Etag:**

```
 Etag（哈希值）：
    服务器给你这个资源的时候会给一个Etag值，当过了强缓存的时间，浏览器在问服务器请求问它这个资源可不可以在用的时候，
    会通过这个http中加一个key值（If-None-Math）一个value，那么value就是发的那个Etag值。
If-None-Match

```



### 4)使用CDN（网络优化，CDN加载资源非常快）;

CDN可以让客户以最快的时间把资源请求过来；（让网络库快速到达服务器端把文件下载下来;）

当页面第一次打开的时候，浏览器缓存是起不了作用的，使用CDN效果是非常明显的



### 5)预解析DNS

页面中所有的a标签，在一些高级浏览器中默认打开了DNS预解析的（不加这句话，a标签也是可以做到DNS预解析的，这是浏览器的一个功能）；但是如果你的页面https协议头的，很多浏览器默认关闭DNS预解析的。这句话是强制打开a标签的DNS预解析。

````
<meta http-equiv=“x-dns-prefetch-control” content=“on”>
````

- 怎么使用预解析DNS呢

```
<link rel=“dns-prefetch” href=“//host_name_to_prefetch.com”>
```

- 从浏览器输入一个url到页面真正的渲染中间发生了哪些环节/

  [ 从输入 URL 到页面加载完成的过程中都发生了什么事情？](https://www.jianshu.com/p/71cf7f69eca8)



##  2.和缓存相关的http头有哪些？能写出来几个？

>  Expires 		
>  Cache-Control		
>  Last-Modified	
>  Etag		
>  If-None-Match	



## 参考

无

## 其他

无