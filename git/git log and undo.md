# 目的
还是一些关于git的基本知识，git log主要用于显示git commit的历史记录，还有一个比较重要的概念，如果commit错误，如何从git中恢复数据。git的优点就是如果你的文件已经提交到git，则有很大的可能性，轻易就能恢复。如果你的修改没有提交，那就无法恢复了。因为这时windows的锅。

## git log
1. 为什么要使用log? 查记录，做code review等等。git log的功能比较强大，有很多的参数，具体的信息需要参考[git官方文档](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History).这里记录几个常用的参数

+ 直接使用**git log** ,显示的信息比较简单，就是编号，作者，提交日期
+ 加-p参数，会显示具体的修改信息(同前一个版本比较)，p参数后面可以加 -数字，例如**git log -p -2** ，显示最近的2条commits信息，并显示修改的具体内容，其实就是git diff
+ 鉴于**-p**的输出内容较多，所以又提供了**--pretty**参数来格式化输出内容，例如**git log --pretty="%an %h"**
+ 可以给**git log** 加各种过滤，例如指定搜索某字符串 **git log -S funciton_name**,或者 最近两个星期的 **git log --since=2.weeks**
或者指定搜索路径或文件 **git log -- filename(directory)**

## git commit --amend  更改已提交的内容
如果错误的提交了或者修改了文件，想要反悔。就到了看这段的时候
1. **git commit --amend** 覆盖上一次的提交，例如 
```shell
git commit -m 'first commit'
git add anotherfile
git commit --amend
```
或者
```shell
git commit -m 'first commit'
git commit -m 'update commit message'
```
更改commit 的消息。  看上面的命令，执行了两次的commit,但是使用git status你会发现只有一个commit，第二次的commit直接覆盖了第一次的commit

2. git reset head <file>  如果误操作将一个不需要的文件add了，进入stage状态
3. git checkout -- <file>, 如果误修改了一个文件，使用该命令可以将文件恢复到上一次commit的版本


