# git学习

感谢[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)

## git 基本操作

### 基本命令

初始化仓库，`git init`

添加文件到Git仓库，分两步：

使用命令`git add<file>`  注意，可反复多次使用，添加多个文件

使用命令`git commit - m <message>`   

使用`git status`  来掌握工作区的状态

如果`git status` 告诉你有文件修改过，则`Git diff`来查看修改内容。

### 版本回退

`head`指向的版本 就是当前版本，因此，git允许我们在版本的历史之间穿梭，使用命令`git reset --hard head^`来退回上一个版本或者`head^^`或`commit_id`或者`head~100`

穿梭前，用`git log` 来查看

提交历史，以便确定来回退到那个版本。

要重返未来，用`git reflog`查看命令历史，以便确定回到未来的哪个版本。

场景一：当你改乱了工作区某个文件的内容，想直接丢弃 工作区的修改时，用命令`git checkout -- file` 

场景二：当你不但改了工作区的某个文件的内容，还添加了暂存区，第一步`git reset HEAD file  `第二步：`git checkout -- file` 

场景三：不但添加了，还`commit` 了，`git reset --hard HEAD^`前提是没有提交的远程库orin

### 删除文件

命令`git rm `用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用 担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次你修改的内容**。



## 远程仓库

 ### 添加远程仓库

- 要关联一个远程库，使用命令`git remote add oringin git @server-name:path/repo-name.git`
  + 如果出现`fatal: remote origin already exists.`  说明origin已经是关联了别的仓库
  + 先  `git remote rm origin                                                          ` ，在执行上述命令

- 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

- 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master` 推送最新修改

- 分布式版本系统的最大好处是在本地工作完全不用考虑远程库的存在，也就是有没有联网都可以正常工作，有网络的时候，再把本地提交退诉讼 一下就完成了推送。

### 从远程仓库克隆

- 要克隆一个仓库，首先要知道仓库的地址，然后使用`git clone`命令克隆

- git 支持多种协议，包括`https`，但通过`ssh`支持的原生git协议最快

- git支持大量使用分支

## 分支管理


### 基本命令

- 查看分支:`git branch`

- 创建分支:`git branch <name>`

- 切换分支:`git checkout`

- 创建加切换分支:`git checkout -b <name>`

- 合并某分支到当前分支:`git merge <name>`

- 删除分支 :`git branch -d <name>`

### 解决冲突

- 当git无法自动合并分支时，就必须首先解决冲突，再提交，合并完成。

- 解决冲突就是手动吧文件改为我们想要的内容，在提交。

### 分支管理策略

- 用`git log --graph`命令可以看到分支合并图。

- Git分支非常强大，再团队开发中应该充分利用

- 合并 分支时，加上`--no--ff`参数就可以一个普通模式合并，合并后的分支有历史，能看出

- 来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

### bug 分支

- 修复bug时，我们会通过创建新的bug分支来进行修复，然后合并，最后删除。

- 当手头工作没有完成时，先把工作现场`git stash`,然后去修复bug，修复后，在`git stash pop`，再回到工作现场。

### feature分支

- 开发一个新功能，最好新建一个分支

- 如果要丢弃一个没有合并的分支，可以通过`git branch -D <name>`强行删除。

### 多人协作

多人协作的工作模式：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的代码

2. 如果推送失败，则因为远程分支比你的本地更新，需要用`git pull` `github pull`试图合并

3. 如果合并有冲突，则解决冲突。并在本地提交

4. 没有冲突或解决掉冲突后,用`git push origin <branch-name>推送就能成功

5. 如果`git pull `提示`no tracking information`,则说明本地分支和远程分支的连接关系没有建立，使用命令`git branch --set-upstream-to <brach-name> origin/branch-name`


查看远程库信息使用``git remote -v`;

本地新建的分支如果不推送到远程，对其他人就是不可见的

从本地推送分支,`git push origin <branch-name>`，如果推送失败，先用`git pull`

抓取远程的新提交

在本地创建和远程对应的分支，使用·git checkout -b branch-name origin/brnach-name

名字最好一致

建立本地分支 远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`

从远程抓取分支，使用`git pull`,如果有冲突，先解决冲突。

### Rebase

rebase操作可以把本地未push的分叉整理成直线；

rebase的目的是使我们在查看历史提交的变化是更容易，因为分叉的提交需要三方对比。

## 标签管理

命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`, 也可以指定一个commit

命令`git tag -a <tagname>  -m "blablabla"`可以指定标签信息

命令`git tag`可以查看所有标签。

命令`git push origin <tagname>`可以推送一个本地标签；

命令`git push origin --tags`可以推送全部未推送过的本地标签

命令`git tag -d <tagname>`可以删除本地标签

命令`git push origin:refs/tags/<tagname>`可以删除一个远程标签

忽略某些文件时，需要编写`.gitignore`

`.gitignore`文件本身需要放到版本库里，并且可以`gitignore`做版本管理





