同一个标识符，先后用var和function声明它，最后是什么呢？
```

var a;//声明一个变量，标识符为a
function a(){//声明一个函数，标识符也为a

}
console.log(typeof a);//function
```
显示的是“function”,即function的优先级高于var。
有人觉得这是代码顺序执行的原因，即a被后执行的function覆盖了。好，将它们调换下。
```
function a(){//声明一个函数，标识符也为a

}
var a;//声明一个变量，标识符为a

console.log(typeof a);//function
```
结果仍然显示的是“function”而非“undefined”。即函数声明优先于变量声明。
我们把代码稍作修改，声明a同时赋值。
```
function a(){//声明一个函数，标识符也为a

}
var a=2;//声明一个变量，标识符为a

console.log(typeof a);//number
```
这时显示的是“number”却不是function了，这相当于
```
function a(){//声明一个函数，标识符也为a

}
var a;
a=2;//声明一个变量，标识符为a

console.log(typeof a);//number
```
即把“var a=1”拆分为两步，a被重新赋值了，自然是最后的那个值。