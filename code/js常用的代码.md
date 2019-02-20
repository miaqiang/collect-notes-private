js常用代码

### 解析cookie
```
util.getcookie=function(objname){//获取指定名称的cookie的值
	var arrstr = document.cookie.split("; ");
	for(var i = 0;i < arrstr.length;i ++){
		var temp = arrstr[i].split("=");
		if(temp[0] == objname) return unescape(temp[1]);
	}
}
```

#### json转Obj,Obj转json
> JSON字符串转换为JSON对象 
```
var obj = str.parseJSON(); //由JSON字符串转换为JSON对象

var obj = JSON.parse(str); //由JSON字符串转换为JSON对象
```
> 可以使用toJSONString()或者全局方法JSON.stringify()将JSON对象转化为JSON字符串。
```
var last=obj.toJSONString(); //将JSON对象转化为JSON字符
var last=JSON.stringify(obj);   //将JSON对象转化为JSON字符
 
```
### 如果要通过json字符串传输
```
$.ajax({
	type: "PUT",
	url: PATH + "/p/api/v1/leapid/" + id,
	data: para,
	dataType: "json",//重点
	contentType: "application/json;//重点 charset=utf-8",
	success: function (data) {
	
	}.bind(this),
	error: function (error) {

	}
})
```
#### 获取cookie
```
util.getcookie=function(objname){//获取指定名称的cookie的值
	var arrstr = document.cookie.split("; ");
	for(var i = 0;i < arrstr.length;i ++){
		var temp = arrstr[i].split("=");
		if(temp[0] == objname) return unescape(temp[1]);
	}
}
```
### 去掉字符的前后空格
```
String.prototype.trim=function() {

	return this.replace(/(^\s*)|(\s*$)/g,'');
}
```
### bits转换为B,k,M,G
```
util.parseUsage=function (number) {
	var number=parseInt(number);
	if(number<1024){
		return number+"B";
	}
	var usage_k=number/1024;
	if(usage_k<1024){
		return parseFloat(usage_k).toFixed(2)+"K";
	}else{
		var usage_m=usage_k/1024;
		if(usage_m<1024){
			return parseFloat(usage_m).toFixed(2)+"M";
		}else{
			var	usage_g=usage_m/1024;
			return parseFloat(usage_g).toFixed(2)+"G";
		}
	}
	
}
```
### 正则
```
//email
util.emailExp=/[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/ig;
//phone
util.phoneExp=/^1[3|4|5|7|8][0-9]\d{8}$/ig;
```

### 冒泡排序

```
var examplearr=[3,2,1,3,5,6,7,38,77,5,34,2,99];
function sortArray(arr){
    for(var i=0;i<arr.length;i++){
        for (var j=0;j<arr.length-1-i;j++){
            if(arr[j]>arr[j+1]){
                var max=arr[j1];
                arr[j]=arr[j+1];
                arr[j+1]=max
            }
        }
    }
}
```

### promise

```
var url = 'https://hq.tigerbrokers.com/fundamental/finance_calendar/getType/2017-02-26/2017-06-10';

function getJSON(url){
    return new Promise(function(resolved,reject){
        var XHR= new XMLHttpRequest()
        XHR.open('GET',url,true);
        XHR.send();

        XHR.onreadystatechange=function(){
            if(XHR.readyState==4){
                if(XHR.status==200){
                    try{
                        var response=JSON.parse(XHR.responseText);
                        resolved(response);

                    }catch(e){
                        reject(e);
                    }
                }else{
                    reject(new Error(XHR.statusText));
                }

            }
        }

    })

}

var url = 'https://hq.tigerbrokers.com/fundamental/finance_calendar/getType/2017-02-26/2017-06-10';
var url1 = 'https://hq.tigerbrokers.com/fundamental/finance_calendar/getType/2017-03-26/2017-06-10';

function renderRace() {
    return Promise.race([getJSON(url), getJSON(url1)]);
}

renderRace().then(function(value) {
    console.log(value);
})


```

### 获取cookie

```
function getcookie(objname){//获取指定名称的cookie的值
	var arrstr = document.cookie.split("; ");
	for(var i = 0;i < arrstr.length;i ++){
		var temp = arrstr[i].split("=");
		if(temp[0] == objname) return unescape(temp[1]);
	}
}
```

### 对象深拷贝

```
function cloneObj (obj) {
	var objType = Object.prototype.toString.call(obj);
	if(objType === '[object Array]' || objType === '[object Object]') {
		var temp = (objType === '[object Array]') ? [] : {} ;
		for(var k in obj) {
			temp[k] = cloneObj(obj[k]);
		}
		return temp;
	}
	return obj;
}
```

### 利用filter,去重数组

```
var
    r,
    arr = ['apple', 'strawberry', 'banana', 'pear', 'apple', 'orange', 'orange', 'strawberry'];
r = arr.filter(function (element, index, self) {
    return self.indexOf(element) === index;
});
```