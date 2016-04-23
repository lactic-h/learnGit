learnGit_git配置

# learnGit----git配置

标签（空格分隔）： git

---


###一、git配置
1. 配置文件
每个仓库的Git配置文件都放在.git/config文件中：
当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中
2. 配置命令参数
配置Git的时候，加上--global是针对当前用户起作用的，
如果不加，那只针对当前的仓库起作用。

###二、 .gitignore
有些情况，必须把某些文件放到Git工作目录中，但又不能或者不想提交它们，比如.class文件等，每次git status都会显示Untracked files ...

可以通过配置.gitignore文件可以让git忽略这部分文件。

在Git工作区的根目录下创建一个特殊的.gitignore文件，
然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。
所有配置文件可以直接在线浏览：[https://github.com/github/gitignore][1]

###三、配置命令别名
命令太长容易敲错，可以通过配置命令别名来简化命令。

```
git config --global alias.st status
    用st代替status
git st
    等同于git status命令
    
git config --global alias.co checkout
git config --global alias.ci commit
git config --global alias.br branch
    用co表示checkout，ci表示commit，br表示branch


git config --global alias.last 'log -1'
    配置一个git last，让其显示最后一次提交信息：
git last
    显示最近一次的提交


    甚至还有人丧心病狂地把lg配置成了：
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

git lg
    很爽

```



  [1]: https://github.com/github/gitignore