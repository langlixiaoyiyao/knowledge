# npm模块说明
## npm install
npm install 命令用来安装依赖到node_modules目录。   
当执行这条命令的时候npm会先去查看当前node_modules里面是否已经有这个包的，如果没有才会进行安装。
```
npm install <package name>
``
如果你希望node_modules无论什么情况下都要安装，那么你可以安装的时候加上一个-f的参数
```
npm install <package name> -f
```
如果你想更新已安装的某个包的版本，你可以用如下命令   
```
npm update <package name>
```
   
## npm的发展过程
早期的时候，npm安装依赖的时候是完全按照层级关系去嵌套安装的。这回导致回调地狱的产生。
