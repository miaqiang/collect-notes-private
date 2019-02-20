## hTTP2.0

HTTP/2引入了“服务端推（server push）”的概念，它允许服务端在客户需要数据之前就主动将数据发送到客户缓存中，从而提高性能

HTTP/2提供更多的加密支持

HTTP/2使用多路技术，允许多个消息在一个连接上同时交差。

它增加了头压缩（head compression），因此即使非常小的请求，其请求和响应的header都只会占很小比例的贷款。



## HTTP 状态码

100 continue 继续，一般在发送post请求时，已发送了http header之后服务端将返回此信息，表示确认，之后发送具体参数信息

200 ok 正常返回信息

201 created 请求成功并且服务器创建了新的资源

202 accepted 服务器已经接受请求，但尚未处理

301 moved permanently 请求的网页已永久移动到新位置

302 found 临时重定向

303 see other 临时性重定向，且总是使用get请求新的URL

304 not modefied 自从上次请求后，请求的网页未修改过。

400 bad request 服务器无法理解请求的格式，客户端不应当尝试再次使用相同的内容发送请求。

401 unauthorized 请求未授权

403 forbidden 禁止访问。

404 not found 找不到如何与URL相匹配的资源

500 internal server error 最常见的服务器端错误

503 service unavailable 服务器端暂时无法处理请求（可能过载或维护）