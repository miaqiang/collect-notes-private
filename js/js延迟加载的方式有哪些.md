1. defer和async
2. 动态创建DOM方式（创建sript,插入到DOM中，加载完毕后callBack）
3. 按需异步载入js


    1.异步加载的方案： 动态插入script标签
    2.通过ajax去获取js代码，然后通过eval执行
    
    3.script标签上添加defer或者async属性
    
    4.创建并插入iframe，让它异步执行js
    
    5.延迟加载：有些 js 代码并不是页面初始化的时候就立刻需要的，而稍后的某些情况才需要的。
> defer并行加载js文件，会按照页面上script标签的顺序执行
> async并行加载js文件，下载完成立即执行，不会按照页面上script标签的顺序执行

