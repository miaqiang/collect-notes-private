参考链接：

[深入理解JavaScript系列（1）：编写高质量JavaScript代码的基本要点](http://www.cnblogs.com/TomXu/archive/2011/12/28/2286877.html)
### 1.忘记var的副作用
隐式全局变量和明确定义的全局变量间有些小的差异，就是通过delete操作符让变量未定义的能力。
- 通过var 创建的全局变量（任何函数之外的程序中创建）是不能被删除的。
- 无var创建的隐式全局变量（无视是否在函数中创建）是能被删除的。
  这表明，在技术上，隐式全局变量并不是真正的全局变量，但它们是全局对象的属性。属性是可以通过delete操作符删除的，而变量是不能的：
```javascript
// 定义三个全局变量
var global_var = 1;
global_novar = 2; // 反面教材
(function () {
   global_fromfunc = 3; // 反面教材
}());

// 试图删除
delete global_var; // false
delete global_novar; // true
delete global_fromfunc; // true

// 测试该删除
typeof global_var; // "number"
typeof global_novar; // "undefined"
typeof global_fromfunc; // "undefined
```