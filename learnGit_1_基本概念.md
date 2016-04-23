learnGit_基本概念

# learnGit----基本概念

标签（空格分隔）： git

---



##概念

####repository，版本库
>	版本库又名仓库，英文名repository，可以简单理解为一个目录。
这个目录里面的所有文件都可以被Git管理起来，Git能跟踪该目录下每个文件的修改、删除，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。


####工作区    暂存区    版本库
* working directory，工作区
    &emsp; 不包括.git/目录的整个目标目录就是工作区。工作区的正常状态是clean，如果有文件修改或者新增文件，而没有add到stage，工作区的状态就不是clean。可通过`git status`命令查看工作区状态。
* stage，暂存区
	&emsp; 暂存区的概念就是用来暂存。我们可以把多个修改(或者新增)文件add到stage，然后一次性commit到版本库。这样做的好处是可以减少版本库中commit的数量，以免显得混乱。
	&emsp; stage的实际作用是实现对文件进行跟踪。如果一个文件从未被add到stage，无论在工作区对该文件做多少次修改，git都不会跟踪这些修改。只会在`git status`中显示`untracked files`。而一个文件被add到stage后，git就将跟踪该文件的修改。
	&emsp; 如果一个add到stage的文件，在工作区发生修改后，可通过`git status`命令查看是否有修改。而且可通过`git diff`命令查看修改的内容
> stage实际上是git实现版本控制的一部分
	&emsp;目标目录下的.git/目录包括两部分，
	&emsp;&emsp; 一部分是成为stage的暂存区
	&emsp;&emsp; 一部分是版本控制的各个分支
* 版本库（实际上repository包括stage和branch）
	+ 将文件添加到一个git版本库包括两步
	&emsp;	第一步通过`git add`命令将文件(修改)添加到stage
	&emsp;	第二步通过`git commit`命令将stage的所有内容一次性提交到当前分支。
	+ 所以git commit命令实际是将stage的内容提交到当前分支，并生成一个新版本(包括一个commit id)


####版本概念，commitID
+ 每次git commit命令将在分支上生成一个新的版本，同时会生成一个commitID。
+ commit id是一个SHA1计算出来的一个非常大的数字，用十六进制表示，类似3628164...882e1e0这样的一大串数字

####分支概念
&emsp;见分支操作
####现场概念
&emsp;见保存现场







