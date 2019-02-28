参考网址：    
- [js String对象中常用方法小结(字符串操作)](http://www.jb51.net/article/29547.htm)   
- [样式](http://www.w3school.com.cn/tiy/t.asp?f=jseg_str_style)
- [JavaScript String 对象参考手册](http://www.jb51.net/w3school/js/jsref_obj_string.htm)

### 一、基础
#### 1.String 对象属性
var name1="hello world"
| 属性        | 描述                         | 输出                                |
| ----------- | ---------------------------- | ----------------------------------- |
| constructor | 对创建该对象的函数的引用     | function String() { [native code] } |
| length      | 字符串的长度                 | 3                                   |
| prototype   | 允许您向对象添加属性和方法。 | undefined                           |

#### 1.charCodeAt方法返回一个整数，代表指定位置字符的Unicode编码。
> strObj.charCodeAt(index)  

**说明:**      
index将被处理字符的从零开始计数的编号。有效值为0到字符串长度减1的数字。如果指定位置没有字符，将返回NaN。

例如：
```
var str="ABC";
var re=str.charCodeAt(0);
var re2=str.charCodeAt(3);
console.log(re);// 65
console.log(re2);// NaN
console.log(str);//原字符串不改变
```
#### 2.fromCharCode方法从一些Unicode字符串中返回一个字符串。
> String.fromCharCode(code1,code2...,codeN)   

**说明:**          
code1,code2....是要转换为字符串的Unicode字符串序列。如果没有参数，结果为空字符串。

例如:
```
var re=String.fromCharCode(65,66,112);
console.log(re);// ABp
```
#### 3.charAt方法返回指定索引位置处的字符。如果超出有效范围的索引值返回空字符串。
> strObj.charAt(index)    

**说明：**     
index 从0到strObj.length-1,如果超过下标，结果为空字符串  
例如：
```
var str="ABC";
var re=str.charAt(1);
var re2=str.charAt(3);
console.log(re);//B
console.log(re2);// 空
console.log(str);//ABC 原字符串不改变
```
#### 4.slice方法返回字符串的片段。Array也有该方法
> strObj.slice(start[,end]) 左闭右开    

**说明:**         
start下标从0开始的strObj指定部分开始索引。如果start为负，将它作为length+start处理，此处length为字符串的长度。 
end小标从0开始的strObj指定部分结束索引。如果end为负，将它作为length+end处理，此处length为字符串的长度。
对不符合条件的返回空。

例如：
```
var str="ABCDEF";//leng=6
var re=str.slice(2,4);
var re2=str.slice(2,-1);//str.slice(2,5)
var re3=str.slice(-1,-1);//str.slice(5,5)
var re4=str.slice(-2,-3);//str.slice(4,3)
console.log(re);//CD
console.log(re2);//CDE
console.log(re3);//空
console.log(re4);//空
console.log(str);//ABCDEF 原字符串不改变

```
#### 5.substring方法返回位于String对象中指定位置的子字符串。
> strObj.substring(start,end)   

**说明：**     
start指明子字符串的起始位置，该索引从0开始起算。 
end指明子字符串的结束位置，该索引从0开起算。
subString 方法使用start和end两者中的较小值作为子字符串的起始点。如果start或end为NaN或者为负数，那么将起替换为0。

例如：
```
var str="ABCDEF";
var re=str.substring(2,4);
var re2=str.substring(4,2);
var re3=str.substring(2,-1);//str.substring(2,0)=str.substring(0,2);
console.log(re);//CD
console.log(re2);//CD
console.log(re3);//AB
console.log(str);//ABCDEF 原字符串不改变
```
#### 6.substr方法返回一个指定位置开始的指定长度的子字符串
> strObj.substr(start[,length]) 

**说明：**  
start所需的子字符串的起始位置。字符串的第一个字符的索引为0。   

例如：
```
var str="ABCDEF";
var re=str.substr(1,3);
var re2=str.substr(1,6);//长度超过字符串长度，按照最大的长度截取
var re3=str.substr(-1,6);//如果为负，该值为当前值加上字符串长度
var re4=str.substr(-1,-1);//如果长度为负数，不满足条件，返回空
console.log(re);//BCD
console.log(re2);//BCDEF
console.log(re3);//F
console.log(re4);//kong
console.log(str);//ABCDEF 原字符串不改变
```
#### 7.indexOf方法返回String对象第一次出现的字符串位置。如果没有找到子字符串，则返回-1。
> strObj.indexOf(substr[,startIndex])   

**说明：**
substr要在String对象中查找的子字符串。    
startIndex该整数值指出在String对象内开始查找的索引。如果省略，则从字符串的开始出查找。

例如:
```
var str="ABCDEF";
var re=str.indexOf('B',1);
var re2=str.indexOf('b',1);
console.log(re);//1
console.log(re2);//-1
console.log(str);//ABCDEF 
```
#### 8.lastIndexOf方法返回String对象中字符串最后出现的位置。如果没有匹配到子字符串，则返回-1。
> strObj.lastIndexOf(substr[,startindex])    

**说明：**  
substr要在String对象内查找的子字符串。  
startindex该整数值指出在String对象内进行查找的开始索引位置。如果省略，则查找从字符串的末尾开始。

例如：
```
var str="ABCDBEFB";
var re=str.lastIndexOf('B');//从字符串的末尾开始找
var re2=str.lastIndexOf('B',5);//从5位置从右向左查找 5,4,3,2,1
var re3=str.indexOf('BE');
var re4=str.indexOf('BE',-1);//如果为0或者负数，都从字符串的末尾开始找
console.log(re);//7
console.log(re2);//4
console.log(re3);//4
console.log(re4);//4
console.log(str);//ABCDBEFB 
```
#### 9.search方法返回与正则表达式查找内容匹配的第一个字符串的位置。
> strObj.search(reExp)  

**说明：**  
reExp包含正则表达式模式和可用标志的正则表达式对象。  
例如：
```
var str="ABCDEFCD";
var re=str.search('CD');
console.log(re);//2
console.log(str);
```
#### 10.match 方法可在字符串内检索指定的值，或找到一个或多个正则表达式的匹配。该方法类似indexOf和lastIndexOf,但是它返回指定的值，而不是字符串的位置。
> stringObject.match(searchvalue)     
> stringObject.match(regexp)

例如：
```
var str = "Hello world"; 
var re=str.match("HE")
var re2=str.match("He")
console.log(re);// null
console.log(re2);//["He", index: 0, input: "Hello world"]
console.log(str);//Hello world
```

#### 11.replace 方法用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子串。
> stringObject.replace(regexp/substr,replacement)  

**说明：**   
字符串 stringObject 的 replace() 方法执行的是查找并替换的操作。它将在 stringObject 中查找与 regexp 相匹配的子字符串，然后用 replacement 来替换这些子串。如果 regexp 具有全局标志 g，那么 replace() 方法将替换所有匹配的子串。否则，它只替换第一个匹配子串。
replacement 可以是字符串，也可以是函数。如果它是字符串，那么每个匹配都将由字符串替换。但是 replacement 中的 $ 字符具有特定的含义。如下表所示，它说明从模式匹配得到的字符串将用于替换。

例如
```
var str = "ABCabc"; 
var re=str.replace(/c/ig,'D')//方法用于把字符串转换为小写();
console.log(re);//ABDabD
console.log(str);//ABCabc
```

#### 12.concat 方法返回字符串值，该值包含了两个或多个提供的字符串连接。Array 也有该方法
> str.concat(string1,string2...stringn)  

说明：  
string1，string2要和所有其他指定的字符串进行连接的String对象或文字。

例如：
```
var str="ABCDEFCD";
var re=str.concat(' Hello ',"World")
console.log(re);//ABCDEFCD Hello World
console.log(str);//ABCDEFCD 原字符串不改变
```
#### 13.split将一个字符串分隔为子字符串，然后将结果作为字符串数组返回。
>strObj.split(separator[,limit])  

**说明：**    
separator字符串或正则表达式对象，它标识了分隔字符串时使用的是一个还是多个字符串。如果忽略该选项，则返回包含整个字符串的单一元素数组。

例如：
```
var str="AA BB CC DD EE FF";
var re=str.split(" ",3);
var re2=str.split(" ");
console.log(re);//["AA", "BB", "CC"]
console.log(re2);//["AA", "BB", "CC","DD","FF]
console.log(str);//AA BB CC DD EE FF
```
#### 14.toLowerCase方法返回一个字符串，该字符串的字母被转换成小写。
> strObj.toLowerCase()

例如：  
```
var str = "ABCabc"; 
var re=str.toLowerCase();
console.log(re);//abcabc
console.log(str);//ABCabc
```
#### 15.toUpperCase方法返回一个字符串，该字符串的字母都被转换为大写字母。
> strObj.toUpperCase()

例如：
```
var str = "ABCabc"; 
var re=str.toUpperCase();
console.log(re);//ABCABC
console.log(str);//ABCabc
```
#### 16.toLocaleLowerCase方法用于把字符串转换为小写
> strObj.toLocaleLowerCase();   

**说明：**   
与 toLowerCase() 不同的是，toLocaleLowerCase() 方法按照本地方式把字符串转换为小写。只有几种语言（如土耳其语）具有地方特有的大小写映射，所有该方法的返回值通常与 toLowerCase() 一样。
例如：  
```
var str = "ABCabc"; 
var re=str.toLowerCase();
console.log(re);//abcabc
console.log(str);//ABCabc
```
#### 17.toLocaleUpperCase方法用于把字符串转换为小写
> strObj.toLocaleUpperCase()    

**说明：**   
与 toUpperCase() 不同的是，toLocaleUpperCase 方法按照本地方式把字符串转换为小写。只有几种语言（如土耳其语）具有地方特有的大小写映射，所有该方法的返回值通常与 toLowerCase() 一样。
例如：  
```
var str = "ABCabc"; 
var re=str.toLocaleUpperCase()//方法用于把字符串转换为大写();
console.log(re);//ABCABC
console.log(str);//ABCabc
```
#### 18.toSource()代表对象的源代码
#### 19.toString()返回字符串。
#### 20.valueOf()返回某个字符串对象的原始值。
#### 21.localeCompare()用本地特定的顺序来比较两个字符串。


### 样式相关
```

var txt="Hello World!"
document.write(txt.anchor("myanchor")) <a name="myanchor">Hello world!</a>

document.write("<p>Big: " + txt.big() + "</p>")
document.write("<p>Small: " + txt.small() + "</p>")

document.write("<p>Bold: " + txt.bold() + "</p>")
document.write("<p>Italic: " + txt.italics() + "</p>")

document.write("<p>Blink: " + txt.blink() + " (does not work in IE)</p>")
document.write("<p>Fixed: " + txt.fixed() + "</p>")
document.write("<p>Strike: " + txt.strike() + "</p>")

document.write("<p>Fontcolor: " + txt.fontcolor("Red") + "</p>")
document.write("<p>Fontsize: " + txt.fontsize(16) + "</p>")

document.write("<p>Lowercase: " + txt.toLowerCase() + "</p>")
document.write("<p>Uppercase: " + txt.toUpperCase() + "</p>")

document.write("<p>Subscript: " + txt.sub() + "</p>")
document.write("<p>Superscript: " + txt.sup() + "</p>")

document.write("<p>Link: " + txt.link("http://www.w3school.com.cn") + "</p>")
```