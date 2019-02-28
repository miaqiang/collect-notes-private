#### 参考 
- [js 数组详细操作方法及解析合集](https://juejin.im/post/5b0903b26fb9a07a9d70c7e0?utm_source=gold_browser_extension)


## 一、创建一个数组：

### 1.ES5创建
```
//字面量方式：
//这个方法也是我们最常用的，在初始化数组的时候，相当方便
var a=[3,11,8];//[3,11,8]
//构造器
//实际上 new Array===Array，加不加new 一点影响都没。
var a=Array();//[]
var a=Array(3);//[,,]
var a=Array(3,11,8);//[3,11,8]
```
### 2.ES6 Array.of()返回由所有参数值组成的数组

定义：返回由所有参数值组成的数组，如果没有参数，就返回一个空数组。

目的：Array.of()出现的目的是为了解决上诉构造器因参数个数不同，导致的行为有差异的问题。

```
var a=Array.of(3,11,8);//[3,11,8]
var a=Array.of(3);//[3]
```
### 3.ES6 Array.from()将两类对象转为真正的数组

定义：用于将两类对象转为真正的数组（不改变原对象，返回新的数组）。

参数：    

第一个参数（必选）:要转化为真正数组的对象。

第二个参数（可选）：类似数组的map方法，对每个元素进行处理，将处理后的值放入返回的数组。

第三个参数（可选）：用来绑定this。

```
//1.对象拥有length属性

var obj={0:"a",1:"b",2:"c",length:3};
var arr=Array.from(obj);
console.log(arr);//[a,b,c]

//2.部署了Iterator接口的数据构造 比如：字符串、set、NodeList对象

var arr=Array.from('hello');
console.log(arr);//['h','e','l','l','o'];
var arr=Array.from(new Set(['a','b','a']));
console.log(arr);//['a','b'];
```

## 二、方法总结
数组原型提供了非常多的方法，这里分为三类来讲，一类会改变原数组的值，一类是不会改变原数组，另一类是数组的边遍历方法
### 1.改变原数组的方法（9个）：
```
var a=[1,2,3];
ES5:
	a.splice() //删除/增加 返回被删除项目
	a.pop()  a.shift() //删除 返回被删除项目
	a.push() a.unshift()//增加 返回新长度
	a.sort() a.reverse()//排序 反转 返回新数组
ES6：
	a.copyWithin() a.fill()// 复制 填充
```
### 2.不改变原数组的方法（8个）：
```
var a=[1,2,3];
ES5:
	a.slice() a.join()
	a.toLocateString() a.toString()// 转字符串
	a.concat //拼接
	a.indexOf a.lastIndexOf //查找 indexOf()不能识别NaN
ES7:
	a.includes()
```
### 3.遍历方法(12个)：

js中遍历数组并不会改变原始数组的方法总共有12个：

```
ES5：
	a.forEach()  a.map() 
	a.every()    a.some()
	a.filter()
	a.reduce()   a.reduceRight()
ES6:
	a.find() a.findIndex()
	a.keys() a.values()  a.entries()
```





### 一、改变原数组的方法（9个）：

对于这些能够改变原数组的方法，要注意避免在循环遍历中改变原数组的选项，比如：改变数组的长度，导致遍历的长度出现问题。

#### splice() 添加/删除数组元素

定义：splice()方法向/从数组中添加/删除项目，返回返回被删除的项目

语法：array.splice(index,howmany,item1,......，itemX)


参数：

1.index：必须。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。

2.howmany：必须。要删除的项目数量。如果设置为0，则不会删除项目。

3.item1，...,itemX:可选，像数组添加的新项目。

返回值：如果有元素被删除，返回包含被删除项目的新数组。

eg1:删除元素

```
var a=[1,2,3,4,5,6,7];
//从数组下标0开始，删除3个元素
var item=a.splice(0,3);
console.log(a);//[4,5,6,7];
console.log(item);//[1,2,3];
//从最后一个元素开始删除3个元素，因为最后一个元素，所以只删除了7

var item=a.splice(-1,3);
cosnole.log(a);//[4,5,6]
console.log(item);//[7]
```

eg2:删除并添加

```
var a=[1,2,3,4,5,6,7];
var item=a.splice(0,3,'添加');//从数组下标0开始，删除3个元素，并添加元素'添加'
console.log(item);//[1,2,3]
console.log(a);//['添加'，4，5，6]

var b=[1,2,3,4,5,6,7];
var item=b.splice(-2,3,"添加1","添加2");//从数组最后第二个元素开始删除3个元素，并添加两个元素"添加1"，"添加2"
console.log(b);//[1,2,3,4,5,"添加1","添加2"]
console.log(item);//[6,7]
```

eg3:不删除只添加：

```
var a=[1,2,3,4,5,6,7];
var item=a.splice(0,0,'添加1','添加2');//[]没有删除元素，返回空数组
console.log(item);//[]
console.log(a);//['添加 ','添加2',1,2,3,4,5,6,7]

var b=[1,2,3,4,5,6,7]
var item=b.splice(-1,0,'添加1','添加2');//[]没有删除元素，返回空数组

console.log(b);//[1,2,3,4,5,6,'添加1','添加2',7]
console.log(item);//[]

```

从上诉三个栗子可以得出：

1. 数组如果元素不够，会删除到最后一个元素为止
2. 操作的元素，包括开始的那个元素
3. 可以添加很多元素
4. 添加是在开始的元素前面添加的



#### pop()删除一个数组中的最后一个元素
定义：pop()方法删除一个数组中的最后的一个元素，并且返回这个元素。
参数：无。
```
var a=[1,2,3];
item =a.pop();
console.log(a);//[1,2]
console.log(item);//3
```
#### shift()删除数组的第一个元素
定义：shift()方法删除数组的第一个元素，并返回这个元素。
参数：无。
```
var a=[1,2,3];
item =a.shift();
console.log(a);//[2,3]
console.log(item);//1
```
#### push()向数组的末尾添加元素
定义：push()方法可向数组的末尾添加一个或多个元素，并返回新的长度。
参数：item1,item2...itemX，要添加到数组末尾的元素。
```
var a=[1,2,3];
var item=a.push('末尾');
console.log(item);//4
console.log(a);//[1,2,3,'末尾']
```
#### unshift()向数组的开头添加一个或更多个元素，并返回新的长度。
参数：item1,item2...itemX，要添加到数组开头的元素
```
var a=[1,2,3];
var item=a.unshift('开头');
console.log(a);//["开头", 1, 2, 3]
console.log(item);//4
```
#### sotr()数组排序

定义：sort()方法对数组元素进行排序，并返回这个数组。

参数可选：规定排序顺序的比较函数。

默认情况下sort()方法没有传比较函数的话，默认按字母升序，如果元素不是字符串的话，会调用toString()方法将元素转化为字符串的Unicode，然后再比较字符。

```
//字符串排列，看起来很正常

var  a=["Banana","Orange","Apple","Mango"];

a.sort();
console.log(a);//["Apple", "Banana", "Mango", "Orange"]

//数字排序的时候，因为转换成Unicode字符串之后，有些数会乱，这显然不是我们想要的

var a=[10,1,3,20,25,8];
console.log(a);//[10, 1, 3, 20, 25, 8]
```

##### 比较函数的两个参数：
sort的比较函数有两个默认参数，要在函数中接收这两个参数，这两个参数是数组中两个要比较的元素，通常我们用a和b接收两个将要比较的元素：

- 若比较函数返回值<0,那么a排到b的前面；
- 若比较函数返回值=0,那么a和b相对位置不变；
- 若比较函数返回值>0,那么b排在a的前面；

对于sort()方法更深层级的内部实现以及处理机制可以看一下这篇文章[深入了解javascript的sort方法](https://juejin.im/entry/59f7f3346fb9a04514635552)

##### sort排序常见用法：

1.数组元素为数字的升序、降序：

```
var array=[10,1,3,4,20,4,25,8];
//升序a-b<0 a将排到b的前面，按照a的大小来排序

array.sort(function(a,b){
    return a-b;
})
console.log(array);//[1, 3, 4, 4, 8, 10, 20, 25]

array.sort(function(a,b){
    return b-a;
})
console.log(array);// [25, 20, 10, 8, 4, 4, 3, 1]
```
2.数组多条件排序

```
var array=[{id:10,age:2},{id:5,age:4},{id:6,age:10},{id:9,age:6},{id:2,age:8},{id:10,age:9},{id:10,age:2}];
array.sort(function(a,b){
	if(a.id===b.id){//如果id的值相等，按照age的值升序
		return a.age-b.age;
	}else{
		return a.id-b.id;
	}
})
console.log(array);// [{"id":2,"age":8},{"id":5,"age":4},{"id":6,"age":10},{"id":9,"age":6},{"id":10,"age":2},{"id":10,"age":9}] 

```
3.自定义比较函数。

类似的：运用好返回值，我们可以写出任意符合自己需求的比较函数

```
var array=[{name:'koro1'},{name:'koro1'},{name:'OB'},{name:'koro1'},{name:'OB'},{name:'OB'}];
array.sort(function(a,b){
	if(a.name==='koro1'){//如果name是‘koro1’返回-1，-1<0,a排在b前面
		return -1;
	}else{//如果不是的话，a排在b的后面
		return 1
	}
})
console.log(array)//[{"name":"Koro1"},{"name":"Koro1"},{"name":"Koro1"},{"name":"OB"},{"name":"OB"},{"name":"OB"}] 
```
#### reverse()颠倒数组中元素的顺序
定义：reverse()用于颠倒数组中元素的顺序。
参数：无。
```
var a=[1,2,3];
a.reverse();
console.log(a);//[3,2,1];
```
#### ES6: copyWithin()指定位置的成员复制到其他位置
定义：在当前数组内部，将指定位置的成员复制到其他位置，并返回这个数组。
语法:
```
	array.copyWithin(target,start=0,end=this.length)
```
参数：
三个参数都是数值，如果不是，会自动转为数组。
1. target(必选)：从该位置开始替换数据。如果为负值，表示倒数。
2. start（可选）：从该位置开始读取数据，默认为0。如果为负值，表示倒数。
3. end（可选）：到该位置前停止读取数据，默认等于数组长度。使用负数可以从数组结尾处规定位置。

浏览器兼容(MDN): chrome 45,Edge 12,Firefox32,Opera 32,Safari 9, IE 不支持

eg：
```
//-2相当于3号位，-1相当于4号位
var x=[1,2,3,4,5].copyWithin(0,-2,-1)
console.log(x);//[4, 2, 3, 4, 5]
var a=[1,2,3,4,5,6,7,8,9,10]
//2位置开始被替换，3位置开始读取要替换的 5位置前面停止替换
var y=a.copyWithin(2,3,4);
console.log(y);//[1, 2, 4, 4, 5, 6, 7, 8, 9, 10]
console.log(a);/[1, 2, 4, 4, 5, 6, 7, 8, 9, 10]
```
从上述栗子：
1. 第一个参数是开始被替换的元素位置
  2.要替换数据的位置范围：从第二个参数是开始读取的元素，在第三个参数前面一个元素停止读取
  3.数组的长度不会改变
  4.读了几个元素就从开始被替换的地方替换几个元素。

#### ES6：fill()填充数组
定义：使用给定值，填充一个数组。
参数：
第一个元素（必须）：要填充数组的值
第二个元素（可选）：填充的开始位置，默认为0
第三个元素（可选）：填充的结束位置，默认是this.length
```
['a','b','c'].fill(7);//[7,7,7]
['a','b','c'].fill(7,1,2);//['a',7,'c']
```

### 不改变原数组的方法（8个）：
```
var a=[1,2,3];
ES5:
 a.slice()/a.join()/a.toLocateString()/a.toString/a.concat/a.indexOf/a.lastIndexOf
ES7:
 a.includes()
```
---
#### slice()浅拷贝数组的元素
定义：方法范湖一个从开始到结束（不包含结束）选择的数组的一部分浅拷贝到一个新数组对象，且原数组不会被修改。

注意：字符串也有一个slice()方法是用来提取字符串的，不要弄混了。

语法：
```
 array.slice(begin,end);
```
参数：
begin(可选):索引数值，接受负值，从该索引处开始提取原数组中的元素，默认值为0。
end（可选）：索引数值（不包括），接受负值，在该索引前结束提取原数组元素，默认值为数组末尾（包括最后最后一个元素）。
```
var a=['hello','world'];
var b=a.slice(0,1);
console.log(b);//['hello']
a[0]='改变原数组';
console.log(a);//["改变原数组", "world"]
console.log(b);//['hello']
b[0]='改变拷贝的数组';
console.log(a);//["改变原数组", "world"]
console.log(b);//["改变拷贝的数组"]
```
如上：新数组是浅拷贝，元素是简单数据类型，改变之后不会互相干扰。
如果是负载类型数据（对象，数组）的话，改变其中一个，另一个也会改变、
```
var a=[{name:'OBKoro1'}];
var b=a.slice();
console.log(b);//[{"name":"OBKoro1"}]
a[0].anme='改变原数组';
console.log(a);//[{"name":"改变原数组"}]
console.log(b);//[{"name":"改变原数组"}]
b[0].name='改变拷贝数组',b[0].koro='改变拷贝数组';
console.log(a);//[{"name":"改变拷贝数组","koro":"改变拷贝数组"}]
console.log(b);//[{"name":"改变拷贝数组","koro":"改变拷贝数组"}]
```
原因在定义上说过了：slice()是浅拷贝，对于复杂的数据类型浅拷贝，拷贝的只是指向原数组的指针，所以无论改变原数组，还是浅拷贝的数组，都是改变原数组的数据。

#### join()数组转字符串
定义：join方法用于把数组中的所有元素通过指定的分隔符进行分隔放入一个字符串，返回生成的字符串。

语法：
```
 array.join(str)
```
参数：

str(可选)：指定要使用的分隔符，默认使用逗号作为分隔符。
```
var a=['hello','world'];
var str=a.join();
console.log(str);//hello,world
var str2=a.join('+');
console.log(str2)//hello+world
var str3=a.join(' ');
console.log(str3)//hello world
```
使用join方法或者下文说到的toString方法时，当数组中的元素也是数组或者是对象时会出现什么情况？
```
var a=[['hello','world'],'!'];
var str1=a.join();
console.log(str1);//hello,world,!
var b=[{name:'hello world',age:'2018','!'}]
var str2=b.join();
console.log(str2);//[object Object],!
//对象转字符串推荐JSON.stringify(obj);
```
所以：join()/toString()方法在数组元素是数组的时候，会将里面的数组也调用join()/toString(),如果是对象的话，对象会被转换为[object Object]字符串。

#### toLocaleString()数组转字符串

定义：返回一个表示数组元素的字符串。该字符串由数组中的每个元素的toLocalString()返回值经调用join()方法连接(由逗号隔开)组成。

语法：
```
	array.toLocalString()
```
参数：无

eg:
```
var a=[{name:'OBKorol'},23,'abcd',new Date()];
var str=a.toLocaleString();
console.log(str);//[object Object],23,abcd,2018/6/4 下午4:43:17
```

如上述栗子：调用数组的toLocaleString方法，数组中的每个元素都会调用自身的toLocalString方法，对象调用对象的toLocaleString，Date调用Date的toLocalString。

#### toString()数组转字符串 不推荐

定义：toString()方法可把数组换换为由逗号连接起来的字符串。

语法：

```
array.toString()
```
参数：无

该方法的效果和join方法一样，都是用于数组转字符串的，但是与join方法相比没有优势，也不能自定义字符串的分隔符，因此不推荐使用。

值得注意的是：当数组和字符串操作的时候，js会调用这个方法将数组自动转换为字符串

```
var b=['toString','演示'].toString();
console.log(b);//toString,演示
var a=['调用toString','连接在我后面']+'啦啦啦啦';
console.log(a);//调用toString,连接在我后面啦啦啦啦
```
#### concat
定义：方法用于合并两个或多个数组，返回一个新数组。

语法：
```
	var newArr=oldArray.concat(array1,array2...arrayn)
```
参数：
array1（可选）：改参数可以是具体的值，也可以是数组对象。可以是任意多个。

eg:
```
var a=[1,2,3];
var b=[4,5,6];
//连接两个数组
var newVal=a.concat(b);
console.log(newVal);//[1, 2, 3, 4, 5, 6]
var c=[7,8,9];
var newVal2=a.concat(b,c);
console.log(newVal2);//[1, 2, 3, 4, 5, 6, 7, 8, 9]
//添加元素
var newVal3=a.concat('添加元素',b,c,'再加一个');
console.log(newVal3);//[1, 2, 3, "添加元素", 4, 5, 6, 7, 8, 9, "再加一个"]
//合并嵌套数组，会浅拷贝嵌套数组
var d=[1,2];
var f=[3,[4]];
var newVal4=d.concat(f);
console.log(newVal4);//[1, 2, 3, [4]]
```

#### ES6扩展运算符...合并数组：

因为ES6的语法更简洁易懂，所以现在合并数组我大部分采用...来处理，...运算符可以实现concat的每个栗子，且更简洁和具有高度自定义数组元素位置的效果。

```
var a=[2,3,4,5];
var b=[4,...a,4,4];
console.log(b);//[4, 2, 3, 4, 5, 4, 4]
console.log(a);//[2, 3, 4, 5]
```

#### indexOf()查找数组是否存在某个元素，返回下标
定义：返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1.

语法：
```
	array.indexOf(searchElement,fromIndex)
```
参数：
searchElement(必须):被查找的元素

fromIndex(可选):开始查找的位置（不能大于等于数组的长度，返回-1），接受负值，默认为0。

严格相等的搜索：

数组的indexOf搜素跟字符串的indexOf不一样，数组的indexOf使用严格相等===搜索元素，即数组元素要完全匹配才能搜索成功。

注意：indexOf()不能识别NaN

eg:
```
var a=['啦啦',2,4,24,NaN];
console.log(a.indexOf('啦'));//-1
console.log(a.indexOf('NaN'));//-1
console.log(a.indexOf('啦啦'));/0
```
使用场景：

1. 数组去重

2. 根据获取的数组下标执行操作，改变数组中的值等。

3. 判断是否存在，执行操作。

#### lastIndexOf()查找指定元素在数组中的最后一个位置
定义：方法放回指定元素在数组中最后一个的索引，如果不存在则返回-1。（从数组后面往前查找）

语法：

```
	arr.lastIndexOf(searchElement,fromIndex)
```
参数：

searchElement（必须）:被查找的元素

fromIndex(可选):逆向查找开始位置，默认值为数组的长度-1，即查找整个数组。

关于fromIndex有三个规则：

1. 正值。如果该值大于或等于数组的长度，则整个数组会被查找。

2. 负值。将其视为从数组末尾向前的偏移。（比如-2，从数组倒数第二个元素开始往前查找）

3. 负值。其绝对值大于数组长度，则方法返回-1，即数组不会被查找。

```
var a=['OB',4,'Koro1',1,2,'Koro1',3,4,5,'Koro1'];
var b=a.lastIndexOf('Koro1',4); // 从下标4开始往前找 返回下标2
console.log(b);//2
var b=a.lastIndexOf('Koro1',100); //  大于或数组的长度 查找整个数组 返回9
console.log(b);//9
var b=a.lastIndexOf('Koro1',-11); // -1 数组不会被查找
console.log(b);//-1
var b=a.lastIndexOf('Koro1',-9); // 从第二个元素4往前查找，没有找到 返回-1
console.log(b);//-1

```

#### ES7 includes()查找数组是否包含某个元素 返回布尔

定义：返回一个布尔值，表示某个元素是否包含给定的值

语法：
```
	array.includes(searchElement,fromIndex=0)
```
参数：

searchElement(必选):被查找的元素

fromIndex(可选):默认值为0，参数表示搜索的起始位置，接受负值。正值超过数组长度，数组不会被搜索，返回false。负值绝对值超过长数组长度，重置从0开始搜索。

includes方法是为了弥补indexOf方法的缺陷而出现的：

1. indexOf方法不能识别NaN

2. indexOf方法检查时候包含某个值不够语义化，需要判断是否不等于-1，表达不够直观。

eg

```
var a=['OB','Koro1',1,NaN];
var b=a.includes(NaN); // true 识别NaN
console.log(b);//true
var b=a.includes('Koro1',100); // false 超过数组长度 不搜索
console.log(b);//false
var b=a.includes('Koro1',-100);  // true 负值绝对值超过数组长度，搜索整个数组
console.log(b);//true

```
### 遍历方法(12个)：

js中遍历数组并不会改变原始数组的方法总共有12个：

```
ES5：
 forEach/every/some/filter/map/reduce/reduceRight
ES6:
 find/findIndex/keys/values/entries
```
关于遍历：

- 关于遍历的效率，可以看一下这篇[详解JS遍历](http://louiszhai.github.io/2015/12/18/traverse/#%E6%B5%8B%E8%AF%95%E5%90%84%E6%96%B9%E6%B3%95%E6%95%88%E7%8E%87)
- 尽量不要在遍历的时候，修改后面要遍历的值
- 尽量不要在遍历的时候修改数组的长度（删除/添加）

#### forEach

定义：按升序为数组中含有有效值的每一项执行一次回调函数。
语法

```
array.forEach(function(currentValue,index,arr){},thisValue)
```

参数：

function(必选):数组中每个元素需要调用的函数。

```
//回调函数的参数
1. curentValue(必须)，数组当前元素的值
2. index(可选)，当前元素的索引值
3. arr(可选),数组对象本身
```
thisValue（可选）:当执行回调函数时this绑定对象的值，默认为undefined

##### 关于forEach()你要知道：

- 无法中途退出循环，只能用return退出本次回到，进行下一次回调。】
- 它总是返回undefined值，即使你return了一个值。

##### 下面类似语法同样适用于这些规则

```
 1. 对于空数组是不会执行回调函数的
 2. 对于已在迭代过程中删除的元素，或者空元素会跳过回调函数
 3. 遍历次数再一次循环前就会确定，再添加到数组中的元素不会被遍历。
 4. 如果已经存在的值被改变，则传递给callback的值是遍历到他们那一刻的值。
```
eg:

```
var a=[1,2,,3];//最后第二个元素是空的，不会遍历(undefined,null会遍历)
var obj={name:'OBKoro1'};
var result=a.forEach(function(value,index,array){
    console.log(array);
	a[3]='改变元素';
	a.push('添加到尾端，不会遍历');
	console.log(value,'forEach传递的第一个参数');//分别打印1,2改变元素
	console.log(this.name);//OBKoro1打印三次this绑定在obj对象上
	//break;//break会报错
	return value;//return只能结束本次回调，会执行下次回调
	console.log('不会执行，因为return会执行下一次循环回调')
},obj);
console.log(result);//即使return了一个值，也还是返回undefined
```
#### every检测数组所有元素是否都符合判断条件

定义：方法用于检测数组所有元素是否都符合函数定义的条件

语法：
```
array.every(function(currentValue,index,arr),thisValue)
```
参数:（则几个方法的参数，语法都类似）

function(必须):数组中每个元素需要调用的函数。
```
	//回调函数的参数
	1.currentValue（必须）,数组当前元素的值
	2.index(可选),当前元素的索引值
	3.arr(可选),数组对象本身
```
thisValue(可选)：当执行回调函数时this绑定对象的值，默认值为undefined

方法返回值规则：

1. 如果数组中检测到与一个元素不满足，则整个表达式返回false，且剩余的元素不会再进行检测。

2.如果所有元素都满足条件，则返回true。    

eg:
```
function isBigEnuough(element,index,array){
	return element>=10;//判断数组中的所有元素是否都大于10
}
var result=[12,5,8,130,44].every(isBigEnough)；//false
console.log(result);//false
var result=[12,54,18,130,44].every(isBigEnough);//true
console.log(result);//true
//接受箭头函数写法
[12,5,8,130,44].every(x=>x>=10);//false
[12,54,18,130,44].every(x=>x>=10);//true

```
#### some数组中是否有满足判断条件的语句

定义：数组中是否有满足条件判断的元素

语法：

```
	array.some(function(currentValue,index,arr),thisValue)
```
参数：（这几个方法的参数，语法都类似）

function（必须）：数组中每个元素需要调用的函数。

```
//回调函数的参数
1. currentValue(必须),数组当前元素的值
2. index(可选)，当前元素的索引值
3. arr(可选)，数组对象本身
```

thisValue（可选）：当执行回调函数时this绑定的值，默认为undefined

方法返回值规则：

1. 如果有一个元素满足条件，则表达式返回true，剩余的元素不会再执行检测。

2. 如果没有满足的条件，则返回false。

eg:
```
function isBigEnough(element,index,arr){
	return (element>=10);//数组中是否有一个元素大于10
}
var result=[2,5,8,1,4].some(isBigEnough);
console.log(result);//false
var result=[12,5,8,1,4].some(isBigEnough);
console.log(result);//true
```

#### filter 过滤原始数组，返回新数组

定义：返回一个新数组，其包含通过所提供函数实现的测试的所有元素。

语法：

```
	var new_array=arr.filter(function(currentValue,index,arr),thisArg)

```
参数:(这几个方法的参数，语法都类似)

function（必须）:数组中每个元素需要调用的函数。

```
	//回调函数的参数
	1. currentValue（必须）,数组当前元素的值
	2. index(可选)，当前元素的索引值
	3. arr(可选)，数组对象本身
```

thisArg(可选)：当执行回调函数this绑定对象的值，默认值为undefined

eg

```
	var a=[32,33,16,40];
	var result=a.filter(function(value,index,arr){
		return value>=18;
	})
	console.log(result);//[32,33,40]
```

#### map 对数组中的每个元素进行梳理，返回新的数组

定义：创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

语法：

```
	var new_array=arr.map(function(currentValue,index,arr),thisArg)
```

参数：（这几个方法的参数，语法都类似）

function(必须)：数组中每个元素需要调用的函数。
```
//回调函数的参数
1. currentValue(必须)，数组当前元素的值
2. index(可选)，当前元素的索引值
3. arr(可选)，数组对象本身
```

thisArg(可选)：当执行回调函数时this绑定对象的值，默认为undefined。

eg
```
var a=['1','2','3','4','5'];
var result=a.map(function(value,index,array){
	return value+'新数组的新元素'
});
console.log(a);//["1", "2", "3", "4", "5"]
console.log(result)["1新数组的新元素", "2新数组的新元素", "3新数组的新元素", "4新数组的新元素", "5新数组的新元素"]
```

#### reduce为数组提供累加器，合并为一个值

定义：reduce()方法对累加器和数组中的每个元素(从左到有，应用一个函数，最终合并为一个值。

语法:

```
arry.reduce(function(total,currentValue,currentIndex,arr),initialvlue)
```
参数：

function(必须)：数组中每个元素需要调用的函数。

```
//回调函数的参数
1. total（必须），初始值，或者上一次调用回调返回的值
2. currentValue（必须），数组当前元素的值
3. index(可选)，当前元素的索引值
4. arr（可选），数组对象本身
```

initialValue(可选)：指定第一次回调的第一个参数

回调第一次执行时：
- 如果initialValue在调用reduce时被提供，那么第一个total将等于initialValue，此时currentValue等于数组中的第一个值。
- 如果initialValue未被提供，那么total等于数组中的第一个值，currentValue等于数组中的第二个值，此时如果数组为空，那么将抛出TypeError。
- 如果数组仅有一个元素，并且，没有提供initialValue,或提供了initialValue但数组为空，那么回调不会被执行，数组的唯一值将被返回。

eg:

```
//数组求和
var sum=[0,1,2,3].reduce(function(a,b){
	return a+b;
},10);
console.log(sum);//16
var flattened=[[0,1],[2,3],[4,5]].reduce((a,b)=>a.concat(b),[])
console.log(flattened);//[0, 1, 2, 3, 4, 5]

```
#### reduceRight 从右至走累加
这个方法除了与reduce执行方向相反外，其他完全与其一致，请参考上述reduce方法介绍。

#### ES6: find()&findIndex()根据条件找到数组成员

find()定义：用于找到第一个符合条件的数组成员，并返回该成员，如果没有符合条件的成员，则返回undefined。

finderIndex()定义：返回第一个符合条件的数组成员的位置，如果所有成员都不符合条件，则返回-1。

语法:
```
 var new_array=arr.find(function(currentValue,index,arr),thisArg)
 var new_array=arr.findIndex(function(currentValue,index,arr),thisArg)
```
参数：（这几个方法的参数，语法都类似）

function(必须)：数组中每个元素需要调用的函数。

```
//回调函数的参数
1. currentValue(必须),数组当前元素的值
2. index(可选)，当前元素的索引值
3. arr(可选)，数组对象本身
```
thisArg(可选)：当执行回调函数时this绑定对象的值，默认为undefined

这两个方法都可以识别NaN，弥补了indexOf的不足。

eg:
```
//find
var a=[1,2,-5,10].find((n)=>n<0);
console.log(a);//-5
var b=[1,4,-5,10,NaN].find((n)=>Object.is(NaN,n));
console.log(b);//NaN

//findIndex
var a=[1,4,-5,10].findIndex((n)=>n<0);
console.log(a);//2
var b=[1,4,-5,10,NaN].findIndex((n)=>Object.is(NaN,n));
console.log(b)//4
```
浏览器兼容(MDN):Chrome 45,Firefox 25,Opera 32, Safari 8, Edge yes,

#### ES6 keys()&values()&entries()遍历键名、遍历键值、遍历键名+键值

定义：三个方法都返回一个新的Array Iterator对象，对象根据方法不同包含不同的值、

语法:
```
	array.keys();
	array.values();
	array.entries();
```
参数：无。

eg：
```
for( var index of ['a','b'].keys()){
	console.log(index);//0  1
}

for( var elem of ['a','b'].values()){
	console.log(elem);//a  b
}
for( var [index,elem] of ['a','b'].entries()){
	console.log(index, elem);// 0 "a" 1 "b"
}

```
在for...of中如果遍历中途要退出，可以使用break退出循环。

如果不使用for...of玄幻，可以是手动调用遍历器对象的next方法，进行遍历：
```
var letter=['a','b','c'];
var entries=letter.entries();
console.log(entries.next().value);//[0, 'a']
console.log(entries.next().value);//[1, 'b']
console.log(entries.next().value);//[2, 'c']
```
entries()浏览器兼容性(MDN):Chrome 38, Firefox 28,Opera 25,Safari 7.1
keys()浏览器兼容性(MDN):Chrome 38, Firefox 28,Opera 25,Safari 8,
注意:目前只有Safari 9支持,，其他浏览器未实现，babel转码器也还未实现