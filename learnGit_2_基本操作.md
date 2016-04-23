learnGit_基本操作

# learnGit----基本操作

标签（空格分隔）： git

---

![git_basic][1]

##基本操作
####**1. 创建一个版本库**
```
cd learnGit
    进入目标目录
git init
    在目标目录下执行 git init命令
```	
执行git init命令后，目标目录会多一个".git/"目录。
这个目录是Git用来跟踪管理版本库的，保存了当前版本库的配置信息和版本信息。

####**2. 向版本库中添加文件**
```
git add filename
    将工作区修改保存到暂存区
git commit -m "infoMsg"
    将暂存区内容提交到分支并生成一个新版本
```    
####**3. 查看仓库状态**
```
git status
    查看仓库当前的状态，获知是否有文件被修改过
    
git diff
git diff HEAD -- filename
    用于查看工作区发生的修改的内容
```
####**4. 版本回退**
```
git log
git log --pretty=oneline
    查看提交日志
    
git reset commitID
    回退到commitID对应的版本
git reset --hard commitID
    --hard参数有特别的意义

git reflog
    显示commit相关的所有记录(所有版本变化信息，包括回退)
```

####**5. 撤销修改**
```
git checkout -- filename
    撤销工作区发生的修改
git reset HEAD filename
    unstage暂存区的内容
```
撤销修改有两种情况
**第一种是撤销工作区发生的修改**
`git checkout -- filename`命令是把目标文件在工作区的修改全部撤销。

    这里有两种情况：
    一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态。
	一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。
	
**第二种是将保持到stage的修改撤销回工作区修改状态**
`git reset HEAD filename`可以把保存到暂存区的修改撤销掉（unstage），重新放回工作区


####**6. 删除文件**
```
git rm filename
    物理删除文件后，取消git对该文件的追踪(版本控制)
    实际相当于把工作区的修改(删除某个文件)保存到stage
git commit -m "infoMsg"
    将stage的内容(删除某个文件)提交到分支

git checkout -- filename
    把误删的文件恢复到最新版本
    实际上是撤销工作区的修改(删除某个文件)
```
当我们手动删除一个已经被git追踪修改的文件时，**本质上是在工作区对这个文件做了某些修改操作(就是删除该文件)**，git追踪到你在工作区删掉了这个文件。这个删除操作发生在工作区，所以此时工作区和版本库就不一致了，而且git status会显示哪些文件被删除了。

当在工作区删除一个文件后，有两种情况
**一种情况是确实要从版本库中删除该文件**，那就将该文件从git中删掉，并且git commit提交该操作
```
git rm test.txt
    实际上把工作区的修改保存到stage
git commit -m "remove test.txt"
```
**一种情况是删错了**，但是版本库里还有之前提交的版本，所以可以很轻松地把误删的文件恢复到最新版本
```
git checkout -- test.txt
    相当于是撤销工作区的修改
```


##二、命令详解

  [1]: https://raw.githubusercontent.com/lactic-h/learnGit/master/pictures/git_basic.png