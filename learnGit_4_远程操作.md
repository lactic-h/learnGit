learnGit_远程操作

# learnGit----远程操作

标签（空格分隔）： git

---

注释
    remoteName指代远程仓库
    remoteBranch指代远程分支
    localBranch指代本地分支


##**一、git remote**

####1.查看远程库信息
```
git remote
git remote -v   //查看与本地库相关联的远程库信息
git remote show remoteName  //查看指定远程库信息
```

####2.添加远程库
```
git remote add remoteName URL
git remote add git@github.com:lactic-h/learnGit.git
```
* URL格式为 git@server-name:path/repo-name.git
* remoteName是URL代表的远程库在本地的一个别名，可以任意选取(默认将远程库命名为origin）
* 将当前本地仓库和URL代表的远程仓库相关联
>**注意！是将仓库相关联，而不是将仓库的分支相关联。**

####3.删除远程库
```
git remote rm remoteName
```
删除远程仓库，实际上是解除本地库与远程库的关联。

####4.重命名远程库
```
git remote rename remoteName newName
git remote rename origin testName
```

####5.分支间关联关系操作
```
git branch --set-upstream dev origin/dev
//设置本地dev分支与origin的dev分支相关联
git branch --set-upstream-to dev origin/dev
git branch --unset-upstream
//解除关联分支
```
+ 关联关系的正式名称为**track,追踪关系**
+ 分支间的关联关系在fetch/pull/push操作中有重要意义！

####6.PS
* origin这个仓库里也可以有多个分支master,dev,feature等。
* 具体的内容推送或者拉取是在两个仓库的具体分支之间进行，而不是在仓库间进行。


##**二、git clone**
####1. 将URL代表的远程库clone到本地。
```
git clone URL
git clone git@github.com:lactic-h/learnGit.git
```
+ clone远程库时，默认将远程库命名为origin。
+ 从远程库clone时，默认只clone origin/master分支。
####2. clone时指定远程库名称
```
git clone -o remoteName URL
//-o 参数可以指定远程库名称。
```
####3. clone远程库指定分支
```
git checkout -b dev origin/dev
在本地创建dev分支，并将远程仓库origin的dev分支克隆本地的dev分支
```


##**三、git fetch以及本地远程库概念** 
一旦远程主机的版本库有了更新，需要将这些更新取回本地。
```
git fetch remoteName //将指定远程库的更新取回本地。
```
默认情况下，git fetch取回所有分支(branch)的更新。
```
git fetch remoteName branchName //取回特定分支的更新。
git fetch origin master //取回origin仓库的master分支
```


**在这里有一个特别的概念，需要区分。叫做本地远程库。**

对于一个git仓库，如果其与某一远程库相关联，逻辑上有三个仓库的存在。
>**`本地库` `本地远程库` `远程库`**
本地远程库是远程库在本地的一个镜像。

1. 当我们执行完`git fetch`操作后，我们实际上是把远程库的内容拉取到本地，并保存在本地远程库中(并不是直接放在本地库中！！！)。
> 当我们执行完`git fetch`操作后，本地库并没有什么变化。
2. 对于git fetch存放在本地远程库中的内容，可以通过在本地主机上以”远程主机名/分支名”的形式读取。
>	比如origin主机的master，就要用origin/master读取。

3. 我们可以通过git branch命令的-r选项查看远程分支，-a选项查看所有分支。
```
git branch      //查看本地分支
git branch -r   //查看远程分支
git branch -a	//查看所有分支=本地分支+远程分支
```
4.对于本地远程库中的远程分支的内容，我们可以通过merge操作将其合并到本地分支上。
```
git checkout dev        //切换到目标分支(此处为dev)
git merge origin/dev
    //将origin的dev分支合并到当前分支(也就是本地的dev分支)
```

##**四、git pull**
git pull的作用是取回远程主机某个分支的更新，再与本地的指定分支合并。
>**相当于git fetch和git merge两个操作。**

####1. 完整命令格式
```
git pull remoteName remoteBranch:localBranch
```
表示将remoteName/remoteBranch分支和localBranch分支合并

####2. 省略本地分支名，表示与当前分支合并
```
git pull remoteName remoteBranch    //将远程分支与当前分支更新并合并
```
####3. 完全省略分支名，关联分支间合并
```
git pull remoteName
		//将远程库的所有分支与当前库的所有分支更新并合并
		//前提是当前库分支和远程库分支建立关联关系。
```

##**五、git push**

####1. 完整命令格式
```
git push remoteName localBranch:remoteBranch
//注意跟pull的命令格式区别，branch顺序不同
```
推送本地localBranch分支到remoteName/remoteBranch分支
####2. 省略远程分支名
```
git push remoteName localBranch
```
+ 将本地仓库的`localBranch`分支的内容推送到remoteName远程库中与该本地分支存在”追踪关系”的远程分支(通常两者同名)
+ 即使本地仓库的`localBranch`分支未与`remote/sameNameBranch`分支关联，推送操作也会发生。
+ 但推送操作只发生一次，不会将`localBranch`分支与`remote/sameNameBranch`分支建立关联。所以下次通过"git push"推送时并不会更新`remote/sameNameBranch`分支。
+ 如果`remoteName`不存在`sameNameBranch`分支，则将在`remoteName`上新建该分支。

```
git push -u origin master
```

+ -u这个参数，是为了推送时将本地仓库的master分支和origin的master分支关联起来。
+ 一旦本地仓库的某一分支与远程库的某一分支关联后，再次推送时可以简化命令为`git push`
####3. 省略本地分支名
```
git push remoteName :remoteBranch
```

####4. 看命令

```
git push remoteName
```
+ 将与remoteName这个远程库的某一分支已经建立关联的本地库分支的内容推送到remoteName远程库的分支。
+ 如果本地库与remoteName没有任何分支相关联，默认推送master分支。
+ 但并不会将本地库master与remoteName/master建立关联。

####5. 再看命令
```
git push
```
+ 将与任一远程库的某一分支已经建立关联的本地库分支的内容推送到所有相关联的远程库分支。
+ 能够推送的前提是本地库的分支与远程库的分支已经关联。



##**五、push冲突问题与解决方法**

多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin branch-name`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
+ 或者用`fetech+merge`替代`pull`
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！
5. 如果git pull提示`“no tracking information”`，则说明本地分支和远程分支的链接关系没有创建，
用命令`git branch --set-upstream branch-name origin/branch-name`将本地分支和远程分支链接。


