# 目的
关于Git中对Branch的处理

## Git Branch的一些基本知识
**git branch branchname**  用来新建一个branch ,在本地/远程（push之后) 会产生一个新的指针指向最新的commit,
**git checkout branchname** 切换branch，在git中有一个特殊的指针**header** ，默认情况下指向master branch(git命令的默认生成的branch)，切换后，header指针指向新的branch。

在checkout不同的branch之后，再进行commit, git会生成不同的文件版本。见图1
![](1.png)



## Git remote
Git是一个分布式的版本控制系统，所有的内容在服务器上和本地均有备份，假设从服务器上git clone之后，就会将内容均拷贝到本地，并且
1. 在本地会有一个master的指针指向最新的版本  - 这个是local的
2. 在本地会有一个Origin/master的指针指向最新的版本  这个是代码server
当本地有任何更改之后并COMMIT之后，本地的master指针会随之移动并指向最新版本。

如果是多人操作的情况，服务器的master版本由其他人更改后，可以使用**git fetch**命令，该命令会将服务器上的所有内容全部拿下，并写入本地数据库，同时更新**origin/master**指针。

##  git push
当本地新建了一个Branch，并想要推送到服务端的时候可以使用 git push origin localbranch,（或者可以使用git push origin localbranch:serverbranch 来指定server端的Branch的名字）然后你的合作者可以使用上面提到的git fetch origin localbranch 从服务端获取这个Branch, 但是需要注意地是
1. 从server端获取到新的Branch之后，并没有在本地新建了本地指针，而是只有Origin/localbranch指针，可以使用**git merge origin/localbranch** 来获取代码，
2. 或者新建本地的指向localbranch的指针，git checkout -b mylocalbranch origin/localbranch

##  Tracking Branch
使用checkout -b 从remote端新建一个Branch之后，git会自动创建一个tracking branch(upstream branch),意思为本地的Branch和Remote的Branch有一个直接的连接，只要你在本地切换到Tracking的branch，然后运行git pull，git会知道从那个remote，获取哪个branch。 
1. git checkout --track origin/remotebranch    同名
2. git checkout -b localbranch origin/remotebranch   换名字
3. 如果本地已经有对应的Branch了，可以通过git checkout -b localbranch , git branch -u origin/remotebranch  或者 git branch ----set-upstream-to=origin/remotebranch. 
4. 同时可以使用git branch -vv 来查看所有的Tracking Branch

##  git pull
其实就是**git fetch** 和 **git merge**的合体

##  删除remote branch
git push origin --delete remotebranch
注意：这个设置并不是直接删除了，git server只是在server上把对应这个branch的指针删除，真实的数据依然在server上，只有等到GC运行时，才会真正删除。即如果不小心删除了Branch，也是很快可以恢复的