# 目的
Git的基础知识

## 本地Git中的文件状态
1. Tracked -  包括有Unmodified, modified, 和committed
2. Untracket - 所有的其他文件 （如新文件，从Tracked中删除的)
##　状态的变化
UnTracket -> Tracked
New　 ->　Tracked gitadd(staged)
Unmodified -> modified (staged)
当git add命令运行后，git会立刻将一个文件放入到Stage状态。 如果之后对文件再进行修改，运行git status之后会在stage和unstage下同时发现这个文件

## git status 和 git diff
git status 只列出文件名
git diff会列出详细信息

1. **git diff** 会列出文件没有staged的部分，比较对象为当前文件和在stage状态下的文件
2. **git diff --staged** 比较对象为stage状态下的文件和上次commit的文件。 或者使用**git diff -cached**

## git commit
1. git commit 默认将staged 状态下的文件提交,然后输入提交信息
2. git commit -m message  - 内置提交信息至命令中
3. git commit -a file  - 跳过stage状态，提交文件不需要运行git add。

## git remove
1. 在git 中删除一个文件，需要使用git rm ，该命令不仅删除文件本身，同时也将git中对该文件的追踪也删除
2. 如果要删除的文件已经被git add了，在staged状态。 要删除该文件则需要加-f ，目的是为了加强安全性。还没有提交且在stage状态的文件是无法恢复的。
3. 如果需要删除一个文件，但仅局限于在git中删除，仍需保留物理版本，这个功能会特别有用，如果你忘记在.gitignore中添加这个文件了，则使用--cached标签。 git rm --cached file

## git 中的文件改名
git本身没有专门的文件改名的命令，但是可以通过两种方法做到
1. git mv filefrom fileto
2. mv filefrom fileto , git rm filefrom ,git add fileto
然后git commit.
