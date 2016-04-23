learnGit_保存现场

# learnGit----保存现场

标签（空格分隔）： git

---
![git_stash][1]

###现场概念

`现场`的概念要和`工作区`，`暂存区`，`提交`三部分结合起来理解。

比如在当前分支(比如dev)完成一次commit后，又在工作区进行了一些文件修改工作，而且这部分工作只进行到一半，还没法提交。
但是现在必须切换到另外一个分支(fixBug)处理一些紧急工作(改bug什么的)。


如果在不提交工作区修改的内容就直接从当前分支切换到新的分支，切换到新的分支后，新分支的工作区不是clean状态，也就是说在原来分支上工作区修改的内容会跟随到新的分支里。
实质是因为一个git仓库只有一个工作区，并不是仓库里每个分支都各自对应自己的工作区，所以切换分支时，并不会改变工作区的修改。

> 这个工作区修改的内容就称为工作现场stash。

Git提供stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。
也就是说在当前分支保存现场，保存现场后工作区就变为clean状态，然后切换到目标分支处理紧急工作，完成紧急工作后，回到原分支，并恢复现场，也就是恢复工作区。

###具体命令

1. 操作流程
    ```
    git stash
    	保存现场，把当前工作现场“储藏”起来，等以后恢复现场后继续工作：
    git status
    	当前工作区是clean状态
    do something other, like:
    	git checkout master
    	git checkout -b bug101
    		modify some files
    	git add files
    	git commit -m "fix bug 101"
    	git checkout master
    	git merge --no-ff -m "merge bug101" bug101
    	git branch -d bug101
    git checkout dev
    	回到原开发分支，
    git status
        工作区依然是clean的
    
    git stash apply
    	恢复现场，但stash的内容依然存在，并未被删除
    ```
2. 删除stash
通过`git stash apply`恢复现场后，之前保存的现场数据仍然存在，并未被删除。需要通过其他命令手动删除。
    ```
    git stash drop
        删除stash的内容
    git stash pop
    	恢复现场的同时删除stash
    ```

3. 多次保存现场
    可以通过多次stash多次保存现场
    ```
    git stash list
    	可以查看工作现场列表，实际上是一个stash栈
    git stash apply stash@{id}
    	恢复指定的stash
    ```
    


  [1]: https://raw.githubusercontent.com/lactic-h/learnGit/master/pictures/git_stash.png