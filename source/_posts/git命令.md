title: git命令
date: 2015-09-07 15:52:24
tags:
---
#将本地项目上传到github上
一、初始化为git目录
git init：进入到要初始化的目录下，执行该命令。git init执行后，表示当前目录已经成为一个git目录，会在当前目录下创建一个.git文件夹，该文件夹下存放的是版本历史记录文件。
git init bare：这个命令和git init类似，但不会在当前目录下生成.git文件夹，而是直接将版本历史记录文件放到了当前目录下，这就使得当前目录成为了一个裸仓库，不允许进行远端仓库的任何git操作。这样做的好处是避免这种冲突：用户A在远端仓库master分支下执行git操作，而同时用户B将本地版本提交到远端仓库的master分支，这时候就产生了冲突。

二、添加本地文件至git目录下
git add myFloder：其中myFloder是我想放入到git项目中的文件夹名称，首先将myFloder拷贝到上述初始化的git目录下，执行add命令后会将myFloder及其子文件夹和文件都添加为一个git项目，会看到所有的文件夹和文件都打上了加号的图标。
git add myTest.java：添加单个文件则在后边直接跟文件名
git add *.java：支持文件名模糊匹配
git add .：表示将当前目录下的所有文件都添加进去。

三、连接远程仓库
git remote add origin git@github.com:myGitHub/myReposity.git: 其中myGitHub为git的用户名，myReposity是项目名称

四、添加项目到远程仓库上
git push -u origin master

#其他
一、移除初始化
进入到初始化的目录，删除.git文件夹，或者执行命令rm -rf .git

二、从已有的Git仓库克隆出一个新的镜像仓库
git clone git://github.com/myGitHub/myReposity.git mylocalRepository：该条命令表示将已有的github上的一个项目下载到本地，命名为mylocalRepository。

三、提交代码到仓库中
git add .
git commit -m  '提交注释' 


