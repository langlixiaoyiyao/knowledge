# js的模块化
## es6的模块化
### 导入导出语法
```js
// es6的导入语法
import "" from "";

// es6的导出语法
export const a = 3;
export default b = 2;
```
### 特点
1、其模块的依赖关系是在运行前就已经确定好了的。   
2、不能用动态语句去import "" from ""。   
3、可以直接在浏览器中运行。   
## commonJs的模块化
commonjs是nodeJs的模块化方案，在nodeJs中，一个文件就是一个模块。   
### 导入导出语法
```js
// 导入语法
const { a, b } = require("a-b");
const xixi = require("xixi");
// 导出语法 exports = module.exports = {}
exports.name = 'q';
module.exports = {
  a: 1,
  b: 2,
}

```
