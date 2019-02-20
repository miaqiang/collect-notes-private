参考网址：

### 参考网址
1. [js数组依据下标删除元素](http://blog.sina.com.cn/s/blog_60e74b5d01017og5.html)
2. [Array对象(javascript——MADN)](https://msdn.microsoft.com/zh-cn/library/jj155291(v=vs.94).aspx)
3. [MDN->Web 技术文档->JavaScript->JavaScript 指南->Indexed collections](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#Array_object)


判断是不是数组

> Array.isArray(value)
### 一、基础
#### 1.Array 对象属性
var name1=[1,2,3]
| 属性        | 描述                             | 输出                               |
| ----------- | -------------------------------- | ---------------------------------- |
| constructor | 返回对创建此对象的数组函数的引用 | function Array() { [native code] } |
| length      | 设置或返回数组中元素的数目       | 3                                  |
| prototype   | 使您有能力向对象添加属性和方法。 | undefined                          |
#### 1. 创建数组

``` 
var array=[item1,item2...itemN];
var array=new Array();
var array=new Array(size);//指定数组的长度
var array=new Array(item1,item2....itemN);//创建数组并赋值

```

#### 2.取值、赋值

``` javascript
var item=array[index];// 获取指定元素的值
array[index]=value;// 为指定元素赋值
[0, 0, 0].fill(7, 1);//[0,7,7]
```

#### 3.添加新元素
```
array.push(item1,item2...itemN);//将一个或多个元素加入数组，返回新数组的长度
eg:
var xx=[1,2,3];
var xx2=xx.push(4);
console.log(xx2);// 4 返回新数组的长度
console.log(xx);// [1,2,3,4] 原数组将改变

array.unshift(item1,item2...itemN);//将一个或多个元素加入到数组的开始位置，原有元素位置自定后移，返回新数组的长度
eg:
var xx=[1,2,3];
var xx2=xx.unshift(4,5);
console.log(xx2);// 5 返回新数组的长度
console.log(xx);// [4,5,1,2,3] 原数组将改变

array.splice(start,deCount,item1,item2...itemN);//从start的位置开始向后删除delCount个元素，然后从start的位置开始插入一个或多个新元素
eg:
var xx=[1,2,3,4,5];
var xx2=xx.splice(1,2);
console.log(xx2);// [2,3] 返回删除的数据，数组格式
console.log(xx);// [1,4,5] 原数组将改变

```
#### 4.删除元素
``` javascript
array.pop()//删除最后一个元素，并返回该元素
eg:
var xx=[1,2,3,4,5];
var xx2=xx.pop();
console.log(xx2);// 5 返回删除的数据
console.log(xx);// [1,2,3,4] 原数组将改变

array.shift()//删除第一个元素，数组元素位置自动前移，返回被删除的元素
eg:
var xx=[1,2,3,4,5];
var xx2=xx.shift();
console.log(xx2);// 1 返回删除的数据
console.log(xx);// [2,3,4,5] 原数组将改变

array.splice(start,delCount);//从start的位置开始向后删除delCount个元素
eg:
var xx=[1,2,3,4,5];
var xx2=xx.splice(2,2);
console.log(xx2);// [3,4] 返回删除的数据
console.log(xx);// [1,2,5] 原数组将改变
```

#### 5.数据的合并，截取

``` javascript
array.slice(start,end);//以数组的形式返回数组的一部分，注意不包括end对应的元素，如果省略end将复制start之后的所有元素(左闭又开，注意和splice的区别，splice第二个参数是长度，slice的第二个参数是结束位置)
eg:
var xx=[1,2,3,4,5];
var xx2=xx.slice(2,4);
console.log(xx2);// [3,4] 返回新数组的长度
console.log(xx);// [1,2,3,4,5] 原数组不改变

array.concat(array1,array2);//将多个数组拼接成一个数组
eg:
var xx1=[1,2,3],xx2=[4,5],xx3=[6,7];
var xx4=xx.concat(xx1,xx2,xx3);
console.log(xx1);// [1,2,3] 原数组不改变
console.log(xx2);// [4,5] 原数组不改变
console.log(xx3);// [6,7] 原数组不改变
console.log(xx4);// [1,2,3,4,5,6,7] 
```

#### 6.数组的排序
```javascript
array.reverse();//数组反转
eg:
var xx=[1,10,2,3,4,5];
var xx2=xx.reverse();
console.log(xx2);// [5,4,3,2,10,1] 返回翻转后的数组
console.log(xx);// [5,4,3,2,10,1] 原数组将改变

array.sort();//数组排序，返回数组地址
eg:
var xx=[1,2,3,10,5,4];
var xx2=xx.sort();
console.log(xx2);// [1,10,2,3,4,5] 返回排序后的数组
console.log(xx);// [1,10,2,3,4,5] 原数组将改变

注意：这里默认是按照字符串来排序的，所以10在2的前面，如果需要按数组排序，需要填代码
eg:
var xx=[1,2,3,10,5,4];
function sortNumber(a,b){
return a - b
}

var xx2=xx.sort(sortNumber);
console.log(xx2);// [1,10,2,3,4,5] 返回排序后的数组
console.log(xx);// [1,10,2,3,4,5] 原数组将改变

```
#### 7.数组转字符串
``` javascript
array.join(separator);//将数组用separator分隔符链接起来
eg:
var xx=[1,2,3,10,5,4];
var xx2=xx.join();// 分隔符默认为“，”
var xx3=xx.join("|"); //分隔符为
console.log(xx2);// 1,2,3,10,5,4 转换后的字符串
console.log(xx3);// 1|2|3|10|5|4 转换后的字符串
console.log(xx);// [1,2,3,10,5,4] 原数组不改变

```
#### 8.字符串转数组
```javascript
string.split(separator);//将字符串通过用separator分隔符分隔开来
eg:
var xx="1,2,3,10,5,4";
var xx2=xx.split(',');// 分隔符默认为“，”
console.log(xx2);// 1,2,3,10,5,4 转换后的字符串
console.log(xx);// [1,2,3,10,5,4] 原数组不改变
```
### 二 、进阶 对数组进行处理

#### 1. every方法(Array)
确定数组的所有成员是否满足指定的测试(全部满足则返回true，否则返回false)

**语法：** array1.every(callbackfn[, thisArg])

**参数：** 
参数

| 参数       | 定义                                                         |
| ---------- | ------------------------------------------------------------ |
| array1     | 必需。一个数组对象。                                         |
| callbackfn | 必需。一个接受最多三个参数的函数。 every 方法会为 array1 中的每个元素调用 callbackfn 函数，直到 callbackfn 返回 false，或直到到达数组的结尾 |
| thisArg    | 可选。可在 callbackfn 函数中为其引用 this 关键字的对象。如果省略 thisArg，则 undefined 将用作 this 值 |

**返回值：** 如果 callbackfn 函数为所有数组元素返回 true，则为 true；否则为 false。如果数组没有元素，则 every 方法将返回 true

**回调函数语法：** function callbackfn(value, index, array1)

| 回调参数 | 定义                 |
| -------- | -------------------- |
| value    | 数组元素的值         |
| index    | 数组元素的数字索引   |
| array1   | 包含该元素的数组对象 |


```
var checkNumericRange=function(value){
    if(typeof value!='number'){
        return false;
    }else{
        return value>=this.minimum&&value<=this.maximum;
    }
}
var numbers=[10,15,19];
var obj={minimum:10,maximum:20}
if(numbers.every(checkNumericRange,obj)){
    console.log('all are within range');//output
}else{
    console.log('some are not within range');
}

```
#### 2. some方法(Array)
确定指定的回调函数是否为数组中的任何元素均返回 true  (既有一个满足即返回true)

**语法：** array1.some(callbackfn[, thisArg])

**参数：** 
参数

| 参数       | 定义                                                         |
| ---------- | ------------------------------------------------------------ |
| array1     | 必需。一个数组对象。                                         |
| callbackfn | 必需。一个接受最多三个参数的函数。 some 方法会为 array1 中的每个元素调用 callbackfn 函数，直到 callbackfn 返回 true，或直到到达数组的结尾 |
| thisArg    | 可选。可在 callbackfn 函数中为其引用 this 关键字的对象。如果省略 thisArg，则 undefined 将用作 this 值。 |

**返回值：** 如果 callbackfn 函数为任何数组元素均返回 true，则为 true；否则为 false。
```
var checkNumericRange=function(value){
    if(typeof value!='number'){
        return false;
    }else{
        return value>=this.minimum&&value<=this.maximum;
    }
}
var numbers=[6,12,16,22,-13];
var obj={minimum:10,maximum:20}
if(numbers.some(checkNumericRange,obj)){
    console.log('true');
}else{
    console.log('false');
```

#### 3. filter方法(Array)
返回数组中的满足回调函数中指定的条件的元素。

**语法：** array1.filter(callbackfn[, thisArg])

**参数：** 
参数

| 参数       | 定义                                                         |
| ---------- | ------------------------------------------------------------ |
| array1     | 必需。一个数组对象。                                         |
| callbackfn | 必需。一个接受最多三个参数的函数。对于数组中的每个元素，filter 方法都会调用 callbackfn 函数一次。 |
| thisArg    | 可选。可在 callbackfn 函数中为其引用 this 关键字的对象。如果省略 thisArg，则 undefined 将用作 this 值 |

**返回值：** 一个包含回调函数为其返回 true 的所有值的新数组。如果回调函数为 array1 的所有元素返回 false，则新数组的长度为 0。
```
function checkIfPrime(value,index,ar){
    high=Math.floor(Math.sqrt(value))+1;
    for(var div=2;div<=high;div++){
        if(value%div==0){
            return false;
        }
    }
    return true;
}
var numbers=[31,33,35,37,39,41,43,45,47,49,51,53];
var primes=numbers.filter(checkIfPrime);
console.log(primes);//[31, 37, 41, 43, 47, 53]
```

#### 4. forEach方法(Array)
为数组中的每个元素执行指定操作。

**语法：** array1.forEach(callbackfn[, thisArg])

**参数：** 
参数

| 参数       | 定义                                                         |
| ---------- | ------------------------------------------------------------ |
| array1     | 必需。一个数组对象。                                         |
| callbackfn | 必选。最多可以接受三个参数的函数。对于数组中的每个元素，forEach 都会调用 callbackfn 函数一次。 |
| thisArg    | 可选。 callbackfn 函数中的 this 关键字可引用的对象。如果省略 thisArg，则 undefined 将用作 this 值。 |

**返回值：** 没有返回值，或者说返回值为Undefined

```
function showResults(value,index,ar){
    console.log('value: '+value);
}
var letters=['ab','cd','ef'];
var result=letters.forEach(showResults);
console.log(result);
//value: ab
//value: cd
//value: ef
//undefined
```

#### 5. map(Array)
对数组的每个元素调用定义的回调函数并返回包含结果的数组。

**语法：** array1.map(callbackfn[, thisArg])

**参数：** 
参数

| 参数       | 定义                                                         |
| ---------- | ------------------------------------------------------------ |
| array1     | 必需。一个数组对象。                                         |
| callbackfn | 必选。  最多可以接受三个参数的函数。  对于数组中的每个元素，map 方法都会调用 callbackfn 函数一次。。 |
| thisArg    | 可选。   callbackfn 函数中的 this 关键字可引用的对象。  如果省略 thisArg，则 undefined 将用作 this 值。 |

**返回值：** 一个新数组，其中的每个元素均为关联的原始数组元素的回调函数返回值。
```
function areaOfCircle(radius){
    var area=Math.PI*(radius*radius);
    return area.toFixed(0);
}
var radii=[10,20,30];
var areas=radii.map(areaOfCircle);
console.log(areas);//["314", "1257", "2827"]
```
#### 6. reduce方法(Array)
对数组中的所有元素调用指定的回调函数。该回调函数的返回值为累积结果，并且此返回值在下一次调用该回调函数时作为参数提供。。

**语法：** array1.reduce(callbackfn[, initialValue])

**参数：** 
参数

| 参数         | 定义                                                         |
| ------------ | ------------------------------------------------------------ |
| array1       | 必需。一个数组对象。                                         |
| callbackfn   | 必需。一个接受最多四个参数的函数。对于数组中的每个元素，reduce 方法都会调用 callbackfn 函数一次。 |
| initialValue | 可选。如果指定 initialValue，则它将用作初始值来启动累积。第一次调用 callbackfn 函数会将此值作为参数而非数组值提供。 |

**回调函数语法：** function callbackfn(previousValue, currentValue, currentIndex, array1)

| 回调参数      | 定义                                                         |
| ------------- | ------------------------------------------------------------ |
| previousValue | 通过上一次调用回调函数获得的值。如果向 reduce 方法提供 initialValue，则在首次调用函数时，previousValue 为 initialValue。 |
| currentIndex  | 当前数组元素的数字索引。                                     |
| array1        | 包含该元素的数组对象。                                       |

**返回值：** 通过最后一次调用回调函数获得的累积结果
```
function addRounded(previousValue,currentValue){
    return previousValue+Math.round(currentValue);
}
var numbers=[10.9,15.4,0.5];
var result=numbers.reduce(addRounded,0);
console.log(result);//27


```

#### 6. reduceRight 方法 (Array) 上面方法的倒叙