# vite
## 安装
```
npm i -D vite
```
## 基本的目录结构

1、在根目录下面创建一个vite.config.js文件
```
export default {
}
```
2、在根目录下面创建一个正常的html模版文件
```
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
dev构建命令：vite
prod生产环境构建命令：vite build
