### 一 、练习
#### 1.通过下标删除数据
```
var array=[1,2,3,4,5,6];
var del=[3,5];// 通过下标删除数据
for(var i=0,len=del.length;i<len;i++){
    var index=del[i];
    if(i!=0){
        index-=i;//删除了几个,下标减几，数组长度改变了
    }
    array.splice(index,1)
}
console.log(array)//[1,2,3,5] //原数组改变
```

#### 2.数组的深拷贝
> 基本烈性就是浅拷贝，引用类型就是深拷贝，如果要深拷贝一个数组和对象，可以用array.concat和array.slice函数


在使用JavaScript对数组进行操作的时候，我们经常需要将数组进行备份，事实证明如果只是简单的将它赋予其他变量，那么我们只要更改其中任何一个，然后其他的也会跟着改变，这就导致了问题的发生
```javascript
var arr = ["One","Two","Three"];
var arrto = arr;
arrto[1] = "test";
document.writeln("数组的原始值：" + arr + "<br />");//Export:数组的原始值：One,test,Three
document.writeln("数组的新值：" + arrto + "<br />");//Export:数组的新值：One,test,Three
```
方法一：array的slice方法
``` javascript
对于array对象的slice函数，
返回一个数组的一段。（仍为数组）
arrayObj.slice(start, [end])
参数
arrayObj
必选项。一个 Array 对象。
start
必选项。arrayObj 中所指定的部分的开始元素是从零开始计算的下标。
end
可选项。arrayObj 中所指定的部分的结束元素是从零开始计算的下标。
说明
slice 方法返回一个 Array 对象，其中包含了 arrayObj 的指定部分。
slice 方法一直复制到 end 所指定的元素，但是不包括该元素。如果 start 为负，将它作为 length + start处理，此处 length 为数组的长度。如果 end 为负，就将它作为 length + end 处理，此处 length 为数组的长度。如果省略 end ，那么 slice 方法将一直复制到 arrayObj 的结尾。如果 end 出现在 start 之前，不复制任何元素到新数组中。
```

``` javascript
var arr = ["One","Two","Three"];
var arrtoo = arr.slice(0);
arrtoo[1] = "set Map";
console.log("数组的原始值：" + arr);//数组的原始值：One,Two,Three
console.log("数组的新值：" + arrtoo);//数组的新值：One,set Map,Three
```
方法二：array的concat方法
``` javascript
concat() 方法用于连接两个或多个数组。
该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。
语法
arrayObject.concat(arrayX,arrayX,......,arrayX)
说明
返回一个新的数组。该数组是通过把所有 arrayX 参数添加到 arrayObject 中生成的。如果要进行 concat() 操作的参数是数组，那么添加的是数组中的元素，而不是数组。
```

``` javascript
var arr = ["One","Two","Three"];
var arrtooo = arr.concat();
arrtooo[1] = "set Map To";
console.log("数组的原始值：" + arr );//数组的原始值：One,Two,Three
console.log("数组的新值：" + arrtooo);//数组的新值：One,set Map To,Three
```