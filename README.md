### 把一个目录变成git可以管理的仓库
进入一个目录使用`git init`把这个目录变成git可以管理的仓库。

### 把文件添加到版本库：
1. `git add readme.txt`
2. `git commit -m "wrote a readme file"` (-m是本次提交的说明)

---
## 时光穿梭机
`git status`可以查看当前仓库的状态。

`git diff readme.txt`可以查看这个文件做了什么修改。

__每次`git commit`之前用`git status`查看一下仓库状态__

### 版本回退
- 使用`git log`查看提交的日志

- 使用`git log --pretty=oneline`可以查看精简版

- 利用上面两条命令，可以看到每次提交的 **commit id**(版本号)

- Git回退的时候必须知道当前版本是哪个版本，在Git中，用 **HEAD** 表示当前版本，上一个版本就是 **HEAD^**，上上一个版本就是 **HEAD^^**，现在，回退到上一个版本：

    `git reset --hard HEAD^`

- 或者使用**commit id**来回退：

    `git reset --hard 325644`

- 要查看未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本
---
### 工作区和暂存区
#### 工作区
就是电脑里能看到的目录
#### 版本库
- 工作区有一个隐藏目录 **.git** ，这个不算工作区，而是Git的版本库
- Git的版本库里存了很多东西，其中最重要的称为**stage**的**暂存区**，还有Git为我们自动创建的第一个分支**master**，以及指向**master**的一个指针叫**HEAD**

    ![image](http://www.liaoxuefeng.com/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)
    
---
`git diff HEAD -- readme.txt`命令可以查看工作区和版本库里面最新版本的区别

---
#### 撤销修改
`git checkout -- readme.txt`可以丢弃工作区的修改，这有两种情况：
1. readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态
2. readme.txt已经添加到暂存区后，又做了修改，现在，撤销修改就回到添加到暂存区后的状态

总之，就是让这个文件回到最近一次`git add`或`git commit`时的状态

如果不但工作区修改了，而且add到了暂存区，在commit之前你发现了这个问题，可以使用`git reset HEAD readme.txt`把暂存区的修改撤销掉，重新放回工作区。

---
#### 删除文件
1. 确定要从版本库中删除该文件：`git rm test.txt` --> `git commit -m "remove test.txt"`
2. 删错了，因为版本库中还有，所以可以把误删文件恢复到最新版本：`git checkout -- test.txt`
---
#### 关联远程仓库
- 在github上创建了一个远程仓库，使用`git remote origin git@https://github.com/JJkenny/Java`，添加后，远程库的名字就是origin。
- `git push -u origin master` 使用`git push` 把当前分支master推送到远程，由于远程库是空的，第一次推送master分支时，加上-u参数，Git不但会把本地的master分支内容推送到远程新的master分支，还会把本地的master分支和远程的master分支关联起来，再以后推送或者拉取时就可以简化命令。
- 以后提交，只需要`git push origin master`就好了
---
#### 从远程库克隆
`git clone git@https://github.com/JJkenny/Java`

---
### 分支管理
#### 创建与合并分支
- 创建dev分支，然后切换到dev分支:`git checkout -b dev`，相当于`git branch dev` --> `git checkout dev`
- `git branch`命令会列出所有的分支，当前分支会标一个 `*` 号
- `git checkout master`切换回master分支
- 现在把dev分支的成果合并到master分支上，`git merge dev`，这个命令用于合并指定分支到当前分支上。
- 删除dev分支，`git branch -d dev`
---
#### 解决冲突
用`git log --graph`命令查看分支合并图
