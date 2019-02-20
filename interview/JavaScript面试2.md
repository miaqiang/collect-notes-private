#### 1.类型转换为字符串类型有哪些形式，请写出具体代码。

答：`var num=123; num.toString()；String(num)；`

#### 2.请写出代码中console.log将会打印什么？
```javascript
var scope="global";
function log(){
    var args=Array.prototype.join.call(arguments,",");
    //console.log(this);
    console.log(this.scope+":"+args);
}
var dog={
    scope:"dog",
    yelp:function(){
        var scope="dog.yelp";
        log('wow');

    }
};
dog.yelp(); 
dog.yelp.call(dog); 
log.apply(dog,['created'])
```
答:   
`global:wow`  
`global:wow (this只跟执行环境的上下文有关，这道题，log原本的作用于是全局)`  
`dog:cretated  (call的作用域问题，log的作用域被修改为dog。)`

#### 3.写一个通用的正则表达式，并从变量text中匹配所有的数字
答：var test="123lkj/.,k2";test.match(/\d+/ig)

#### 4.如何判断一个变量是字符串？如何判断一个对象是数组
```javascript
答：   
var name="123";
var arr=[1,2,3];
console.log(typeof name);
console.log(arr instanceof Array)
```
#### 5.请用promise改写下列代码
```javascript
$(document).ready(funtion(){
  $.get('/get/user/info',funtion(result){
    $.get('/get/city?city='+result.user.city,funtion(city){
      //show city info
    })
  })
})
```
答：   
```javascript

```
#### 6.有一div容器A，宽300px，高200px。另有一个list数据B：{'cn':20,'us':26,'au':98,'en':56};
#### 现在需要把这串数据可视化在A容器中：    要求：  
1.以横向条形图（div）展现。   
2.最大值需顶足整个容器宽度。   
3.垂直方向需均匀分布。   
问：   
1.cn,us和au的条形（div）的width和垂直定位分别是多少？   
2.条形（div）和容器A（div）的css样式分别是怎么样的。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script type="text/javascript" src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
</head>
<style>
    .parent{
        width: 300px;
        height: 200px;
        border: 1px solid #ff0000;
    }
    .parent div{
        width: 100%;
        text-align: center;
        height: 50px;
        line-height: 50px;

    }
</style>
<script>
    $(function(){
        var obj={'cn':20,'us':26,'au':98,'en':56};
        var html="";

        for(var x in obj){
            html+='<div>'+x+':'+obj[x]+'</div>';
        }
        $('div').html(html);
    })
</script>
<body>
<div class="parent">
</div>
</body>
</html>
```
答：   
1.width:100% ，25px,75px,125px      
2.如代码所示