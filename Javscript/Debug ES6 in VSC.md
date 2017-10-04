# ES6 支持
nodejs 和当前的大多数浏览器均不支持，但是es6提供了很多方便的方法，且更适合面向对象的编程思想，例如对Class的支持，Object下面的多种方法（Assign）等，以及Lamba表达式，和Export/Import等命令， 所以在实际的开发过程中，开发人员会偏向于es6的写法。这就是Babel应运而生的原因。Babel可以帮助将es6转换成es5及其他浏览器和nodejs支持的javascript。

# IDE
免费的，由微软发行，使用Typescript编写的，拥有大量插件，使用极其方便的编译器 Visual Studio Code。可以集成Git等大量其他插件工具

# 目的
使用VSC来开发ES6的代码时，绕不过的一个问题就是调试，本文就是一篇关于调试的文章

# 调试
## VSC的调式
VSC支持调试JS代码，快捷键F5或者菜单栏调试-》开始就可以进入调出调式菜单并进入调试页面，同时VSC提供了一个Launch.json来配置具体的调试策略。具体的参数可以参考VSC的官方文档，这里简单提一下，当前使用的版本（1.15.1） 支持直接启动调试， 支持attach到运行中的进程，支持通过npm启动，等等

## Babel的调式
1. Babel可以被看作一个编译软件，用于转换当前的ES6 JS。 Babel分成了很多个模块，包括Babel CLI, Babel Regist. 其中Babel-node, Babel-node-debug,Babel都是Babel-cli的一部分。需要调试ES6的代码 ，首先需要使用Babel编译，生成对应的Preset的js。 命令如下代码1所示

2. 下载babel cli 
```xml
npm install babel-cli
```
3. 下载对应的Babel preset 例如Preset-2015
```xml
npm install babel-preset-2015
```

- 编译代码至dist目录，并随时监视lib目录下所有文件的变化，动态编译
- inline表示不生成.map文件，在新生成的js文件中添加链接
- 代码1 

```xml 
babel lib --out-dir dist --watch --source-maps inline
```
## VSC中的配置
在vsc中配置launch.json文件如下
```js
{
    "type": "node",
    "request": "launch",
    "name": "Launch Program",
    "program": "${workspaceRoot}/lib/pbxt.js",  // 程序中的启动文件
    "runtimeExecutable": "${workspaceRoot}/node_modules/.bin/babel-node",  //执行命令s
    "cwd": "${workspaceRoot}",
    "sourceMaps": true,  
    "outFiles": [
        "${workspaceRoot}/dist/**/*.js"   // 对应babel编译生成的代码的目录 -out-dir
    ]
}
```
