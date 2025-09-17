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
## npm包的发布
### npm包版本后缀
```
Alpha 代表内部测试版本
Beta 代表公开的广泛测试版本
RC 代表修复问题和缺陷的候选版本
Release 代表最终的可靠版本
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
#### 扁平化嵌套
针对npm2嵌套地狱的问题，npm3作出了解决方案，就是采用扁平化嵌套方式。   
无论是直接依赖还是子依赖的依赖，优先安装到node_modules的根目录下。当安装到相同模块的时候，会判断已安装模块是否符合新模块的版本范围，如何符合则跳过安装，不符合则安装在当前模块的node_modules下面。   
比如：项目依赖了A、C、D，A依赖B@v1，C依赖B@v2，D依赖E@v1。那么npm安装之后结构就是下面这种情况
```
node_modules
├── A
├── B@v1
├── C
   └── node_modules
        └── B@v2
├── D
└──E@v1
```
这种嵌套方案可以避免同个包被安装多次，也可以避免嵌套层级太深。但是它又会产生新的问题：幽灵依赖、不确定性。
#### 幽灵依赖
比如：项目依赖了A、C、D，A依赖B@v1，C依赖B@v2，D依赖E@v1。那么npm安装之后结构就是下面这种情况
```
node_modules
├── A
├── B@v1
├── C
   └── node_modules
        └── B@v2
├── D
└──E@v1
```
有些时候，我们的项目根本没有直接依赖B@v1，但是因为扁平化，导致了间接依赖B@v1被提升到了顶级，我们在项目中就可以直接导入B@v1进行使用。但是如果后面我们删除了A包，那么node_modules结构就会变成下面这种结构，那我们之前导入B@v1的那段代码就会报错。
```
node_modules
├── C
├──B@v2
├── D
└──E@v1
```
#### node_modules结构的不确定性
因为存在依赖提升，所以node_modules的结构根据安装包的顺序不同，可能会发生变化，举例如下：   
假如我目前在准备项目的一些前置依赖，然后我的安装顺序如下：   
A -> C(依赖lodash@3) -> B(依赖lodash@2)，那么我的node_modules的结构如下
```
node_modules
├── A
├──lodash@3
├── B
   └── node_modules
        └── lodash@2
└── C

```
但是package.json是按照字典排序将这些包添加在依赖字段中的。下一个开发者如果按照pakcage.json去安装，那么他的安装顺序和node_modules结构如下：   
A ->  B(依赖lodash@2) -> C(依赖lodash@3)
```
node_modules
├── A
├──lodash@2
├── B
└── C
    └── node_modules
        └── lodash@3
```
从上面就可以看出两者node_modules结构的不确定性

参考文章：   
[npm 模块安装机制简介](https://www.ruanyifeng.com/blog/2016/01/npm-install.html)。   
[彻底了解npm——架构、进化史及原理解析](https://juejin.cn/post/7245201923506094140?searchId=20250909172905F773A6C04577F1DC38A5#heading-25)   
[聊聊依赖管理](https://juejin.cn/post/7196635893971877948?from=bytetech)   
[前端工程化 - 剖析npm的包管理机制](https://juejin.cn/post/6844904022080667661#heading-51)
