# vite
## 安装
```
npm i -D vite
```
## 基本的目录结构
dist是执行了vite build之后生成的目录。   
public下面的文件，当执行vite命令跑起来之后，该目录下面的文件均可直接访问。   
index.html是模版文件。   
```js
dist
├── assets
└── index.html
public
src
└── index.ts
index.html
package-lock.json
package.json
vite.config.js
```
```
// vite.config.js
export default {
}
```
```html
// index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <script type="module" src="/src/index.ts"></script> <!-- 引入入口文件：vite build的时候会自动识别并替换成编译成功之后的路径 -->
</body>
</html>
```
## vite的基本命令
dev构建命令：vite。   
prod生产环境构建命令：vite build。   
## vite.config.js
```js
export default {
  build: {
    rollupOptions: {
      output: {
        manualChunks: id => {
          // id /Users/huangxiaohong/MyDir/demo/my-test/index.html
          // id /Users/huangxiaohong/MyDir/demo/my-test/src/index.ts
          // id /Users/huangxiaohong/MyDir/demo/my-test/node_modules/react/index.js
          console.log("id", id);
          // 将 node_modules 中的代码单独打包成一个 JS 文件,假如我的src/index.ts里面导入了react和lodash的包，并且都使用到了，那么这个配置就会把这两个node_modules里面的包集合打包成vendor-[hash].js
          if(id.includes('node_modules')) {
            return 'vendor'
          }
        }
      }
    }
  }
}
```
## vite的特性
### treeshaking
treeshaking也被称为摇树优化，简单来讲就是在保持代码运行不变的情况下，去除无用代码，只打包你所用到的api。要使用这个特性无需额外配置。但有个条件就是这个模块必须得是ES6 module才行，如果不是es6 module则默认全量打包。
