git 使用
====


[参考这里](http://rogerdudler.github.com/git-guide/index.zh.html)

***

**安装**

[*git osx 版本*](http://code.google.com/p/git-osx-installer/downloads/list?can=3)

[git windows 版本](http://code.google.com/p/msysgit/downloads/list?can=3)

[git linux版本](http://book.git-scm.com/2_installing_git.html)

***

**创建新仓库**

    1.创建新文件夹
    2.进入执行 git init

***

**复制仓库**

>* 复制本地仓库

>>      git clone /path/to/repository
>>  /path/to/repository 是本地的仓库地址

>* 复制网络上的仓库

>>      git clone username@host:/path/to/repository
>>  username@host:/path/to/repository 在github上面  是https://github.com/xiyoulaoyuanjia/AboutWeb.git 表示其走http协议 如果是git@github.com:xiyoulaoyuanjia/AboutWeb.git 表示走 ssh协议  git://github.com/xiyoulaoyuanjia/AboutWeb.git  则表示走的时git协议

***

**工作流**

git在本地维护着3棵树 。分别是工作目录(实际的文件)、缓冲区(保存最近的更改)、最后是HEAD(指向最近提交的内容)

![](http://rogerdudler.github.com/git-guide/img/trees.png)

*****

**添加与提交**

把修改的东西添加到缓冲区
    
    git add file

实际提交使用如下命令提交到 HEAD 处
    
    git commit -m "代码提交信息"
  
但是这样没有提交到远程服务器中

*****

**推送改动**

将本地的改动推送到远程的仓库上的命令

    git push origin master

master 表示远程的分支(主分支与其它的分支)

如果没有克隆远程的仓库。只是向将现有的仓库增加到远程的仓库里可以使用如下命令

    git remote add origin server(例如git@github.com:xiyoulaoyuanjia/AboutWeb.git)

****

**分支**

分支是用来将特性开发绝缘的。新建仓库的时候 master是默认的主仓库、可以在其它仓库上面开发、待开发完成之后再将它们合并到主分区上面去。

![](http://rogerdudler.github.com/git-guide/img/branches.png)

创建分支可以使用 git checkout 命令  例如 创建一个feature_x分支并切换过去

    git checkout -b feature_x
    
切换回主分区

    git checkout master
    
删除新建的分支

    git branch -d feature_x
    
**更新与合并**   

>更新本地仓库

>> 1.更新远程仓库到本地仓库

>>      git pull

>> 2.更新其它分支到主分支(例如master)
    
>>      git merge <branch>
    
>合并冲突

> 这个对于复杂的问题需要手动合并冲去。当然 少不了一些常用的工具 git diff A B

**标签**

在软件发布的时候创建标签是被推荐的。。

    git tag 1.0.0 1b2e1d63ff

1b2e1d63ff 是commit的提交ID 当然可以少 只要是唯一的就行。。 查看ID 使用

    git log

**替换本地改动**

回到之前的改动。。
    
    git checkout -- <filename>

此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。已添加到缓存区的改动，以及新文件，都不受影响

另外如果想修改本地的所有改动。去服务器下载最新版本 然后把本地主分区指向它就行 相应的命令为
    
    git fetch origin
    git reset --hard origin/master

**有用的东西**

内建的图形化 git

    gitk















    
    
    




















