## npm 基本命令
npm install 命令用来安装依赖到node_modules目录。   
当执行这条命令的时候npm会先去查看当前node_modules里面是否已经有这个包的，如果没有才会进行安装。
```
npm install <package name>
```
如果你希望node_modules无论什么情况下都要安装，那么你可以安装的时候加上一个-f的参数
```
npm install <package name> -f
```
如果你想更新已安装的某个包的版本，你可以用如下命令   
```
npm update <package name>
```

## npm的发展过程
### npm2--嵌套地狱
早期的时候，npm安装依赖的时候是完全按照层级关系去嵌套安装的。这会导致嵌套地狱的产生。   
比如：A@1.0.0的依赖是：B@1.0.0，C@1.0.0的依赖是：B@1.0.0、D@1.0.0。那么npm安装之后结构就是下面这种情况。
```
node_modules
├── A@1.0.0
│   └── node_modules
│       └── B@1.0.0
└── C@1.0.0
    └── node_modules
        └── B@1.0.0
        └── D@1.0.0
```
这种嵌套方式虽然结构清晰明了，但是多个依赖如果都依赖同个包的话，这个包会被下载多次，会导致node_modules的体积过于庞大。
### npm3--扁平化嵌套、不确定性、幽灵依赖、依赖分身
针对npm2嵌套地狱的问题，npm3作出了解决方案，就是采用扁平化嵌套方式。   
比如：项目依赖了A、C、D，A依赖B@v1，C依赖B@v2，D依赖E@v1。那么npm安装之后结构就是下面这种情况
```
node_modules
├── A
├── B@v1
├── C
    └── node_modules
        └── B@v2
└── D
    └── node_modules
        └── E@v1
```
这种嵌套方案可以避免同个包被安装多次，也可以避免嵌套层级太深

参考文章：   
[npm 模块安装机制简介](https://www.ruanyifeng.com/blog/2016/01/npm-install.html)。   
[彻底了解npm——架构、进化史及原理解析](https://juejin.cn/post/7245201923506094140?searchId=20250909172905F773A6C04577F1DC38A5#heading-25)   
[聊聊依赖管理](https://juejin.cn/post/7196635893971877948?from=bytetech)
