leanGit_分支操作

# learnGit----分支操作

标签（空格分隔）： git

---


###一、概念解析

![此处输入图片的描述][1]

####1. 分支概念
+ 分支的本质是指针，一个指向提交的指针。
+ 当我们初始化一个git仓库后，git默认生成一个master分支。
+ HEAD也是一个指针，用来表示当前分支。
&emsp;&emsp;可以将HEAD理解为一个指针变量，用来存放当前分支的指针。
+ 当只有一个master分支时，master就是当前分支，所以HEAD指向master。

> 图一:&emsp; 只有master一个分支，当前分支HEAD为master分支

####2. 新建分支
当我们在当前分支新建一个分支时，实际是新建一个指针，一个指向当前分支的指针。

> 图二:&emsp; 在master分支上新建一个dev分支

####3. 切换分支
+  当我们切换分支时，就是改变HEAD这个指针的指向。
+ 将HEAD理解为一个指针变量，用来存放当前分支的指针。每当我们切换分支时，实际是切换的HEAD这个指针变量的值。

> 图三:&emsp; 从master分支切换到dev分支

####4. 新分支上commit
在新分支上执行一个提交操作对其他分支没有影响。

> 图四:&emsp; 在dev分支上做一次commit操作

---

###二、合并分支
![此处输入图片的描述][2]

> 分支的合并操作有两种，**fast-forward模式的合并** 和 **no-FF模式的合并**。


####1. fast-forward模式的合并实际是将当前分支的指针指向被合并分支最近的提交。
+ 比如当前分支为master，在master分支上合并dev分支就是当前分支master指向dev的最近的提交。
+ 但这种模式下，删除分支后，会丢掉分支信息。

####2. no-FF模式的合并会在分支上新生成一个commit，并将该分支指针指向这个commit

> 如果可能，git会用Fast-forward模式，因为快啊。

####3. 冲突情况下的合并
&emsp;&emsp;在下图所示的情况下，合并会发生冲突，在这种情况下不能通过快速模式合并，只能通过no-ff模式执行合并操作。
&emsp;&emsp;执行merge命令会提示conflict，需要先解决conflict然后通过no-FF模式完成merge操作。
![此处输入图片的描述][3]



###三、具体命令
1. 查看分支情况
    ```	
	git branch 
	    查看本地分支
	git branch -r
	    查看远程分支
	git branch -a
	    查看所有分支=本地分支+远程分支
    ```

2. 新建分支
    ```
    git branch dev
        创建dev分支
    git checkout dev
        从当前分支切换到dev分支
    git checkout -b dev
	    创建并切换到dev分支
    ```
3. 删除分支
    ```
    git branch -d dev
    	删除dev分支
    git branch -D dev
    	强制删除，在不合并dev的情况下强行删除dev分支
	    如果删除一个未被合并的分支时，git会通过报错提出警告
    ```

4. 合并分支
    ```
    git merge dev
    	将dev分支合并到当前分支，
    	如果为fast-forward模式的合并，实际是将当前分支master指向dev的最近的提交
    ```




  [1]: https://raw.githubusercontent.com/lactic-h/learnGit/master/pictures/branch_basic.png
  [2]: https://raw.githubusercontent.com/lactic-h/learnGit/master/pictures/branch_merge.png
  [3]: https://raw.githubusercontent.com/lactic-h/learnGit/master/pictures/branch_conflict.png