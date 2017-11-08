# 目的
由于相对于SVN来说，git创建一个新的branch的耗费小的惊人，在实际应用中branch是git的一个很强大的功能。随之而来的影响就是如何将多个branch中的内容合并到你的主branch。

## 主要命令
Git merge 和 git rebase 是当仁不让的两大命令。两者区别是什么呢？

## git merge
假设在新的branch创建后，
1. 当前branch上没有任何的改动(如果有改动，git merge不被允许执行)，执行了git merge newbranch命令后，git简单的将当前branch的指针指向newbranch指针指向的最新的commit. 
2. 当前branch如果有改动，这是再做git merge,git会自动寻找两个branch共同的上一次提交，然后在当前branch中会进行一次新的提交，这个提交包括了两个branch在共同的上一次提交后修改的内容。
3. 如果当前branch有改动，且两个branch修改了相同的文件，这时就需要手工的merge。 可以使用git mergetool

## git rebase
与merge不同的是，rebase指的是将一个branch的修改的内容，再被merge的branch上再重复做一遍
+ git checkout -b newbranch
+ update file
+ git commit -a -m updates from newbranch
+ git checkout oldbranch
+ update file
+ git commit -a -m update from oldbranch
现在两个branch的内容均有变动
+ git checkout new branch
+ git rebase oldbranch
![git rebase的图形表现](./branch_introduction_rebase.png)
现在newbranch的指针指向了最新的版本，但是oldbranch的指针还是指向原来的版本
+ git checkout oldbranch
+ git merge
+ git branch -d new branch

