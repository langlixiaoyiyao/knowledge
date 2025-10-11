# js的变量&函数的提升
## 结论
var定义的变量，**创建**过程和**初始化为undefined**过程都会被提升。   
let定义的变量，**创建**过程会被提升，但是**初始化为undefined**不会被提升。   
函数定义，**创建**、**初始化**、**赋值**都会被提升。  
## 代码论证
```js
var name = 'abc';
let age = 18;
function sayHi() {
  console.log(name); // undefined
  console.log(age); // 报错。let如果不存在变量提升，应该输出18而不是报错。
  var name = "Lydia";
  let age = 21;
}

sayHi();
```
