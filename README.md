# github学习历程
1. 首先我们要知道github是干什么的，github是一个版本控制工具，可以记录你每次提交的code的变化的情况，嗯，大概就是这样。
2. 一下是github几个常用的命令：
- git init 新建一个空的仓库
- git status 查看仓库的状态
- git add + file 向仓库中添加文件
- git commit -m '说明' 先仓库中添加文件后的备注说明,养成写commit的习惯非常有帮助，因为当你修改的次数多了之后，你不一定能记住哦~
- git push -u origin master 将本地的仓库推送到远程的仓库
- git log 查看变更日志
- git reset -hard 版本号前六位 回归指定的版本
- git branch 查看分支
- git branch newname 创建一个名叫newname的分支
- git checkout branch_name 切换到名叫branch_namde的分支上
- git merge branch_name 将名叫branch_namde的分支合并到当前的分支上
- git pull origin master 将master分支的内容拉到本地
- git diff file_name 可以查看文件的变化
3. 关于变更版本的操作
[关于版本链接变更的几个命令的介绍](https://www.jianshu.com/p/09dbd8dc7345)
- 当我们想回退到某个版本的时候，应该怎么操作，在Git中，head表示当i当前的版本，或者回到以前的版本又想回到现在的版本怎么办

- 首先我们可以使用`git log`命令查看变更日志，执行该条命令之后我们可以看到整个仓库的变更的历史,同时我们可以看到一个`commit id(版本号)`这个是你每次提交系统自动生成的，同时还可以看到你每次修改增加的备注，通过这些备注的说明你就可以决定自己要退回到哪个版本了，是不是有点像操作系统实验时有的同学用到的快照 \斜眼笑，同时我们还应该知道在Git中，`HEAD`表示当前版本，上一个版本是`HEAD^`，上上一个版本是`HEAD^^`，所以易得上一百个版本是`HEAD`+100个`^`，当然没这么蠢，可以写成`HEAD~100`

    ![git log后的输出](F:\git\learngit\Snipaste_2020-02-18_19-39-08.png)

- `git reset --hard commit_id的前六位`可以回退到指定的版本,注意那个`--hard`参数的意义，通过查阅网上的资料可以看出，这里可选的参数一共有三个，分别是`hard,soft,mixed`,分别代表不同的意义

    * hard 将最近一次提交节点的提交记录全部清除

    * soft 将最近一次提交节点的提交记录回退到暂存区

    * mixed 将最近一次提交节点的提交记录回退到工作区
      下面放一张关于github三个分区的说明图

      ![git的三个区](F:\git\learngit\git的三个区.png)这个要好好理解一下，就可以很好的理解git中大多数命令的含义，这里再贴一个链接
      [关于git中区的介绍](https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576)

- 如果回到以前的版本之后还想回到原来的版本怎么办呢，有下面两种情况
    1.  如果你现在的命令窗口还没关的话，你可以直接`git reset  --hard commit_id前六位`，意思就是如果你能直接在当前的命令行窗口里面找到你要回退的版本的`commit_id`的话就可以直接回退回去了
    2.  当然如果你找不到的话，可以使用`git reflog`查看你的变更记录，在这个log里面你可以找到你的回退记录。同样使用如上命令进行回退。
    反正核心就是知道`commit_id`就可以回退到相应的版本
- 我看网上教程还有一种使用`HEAD`的命令，但是自己试验并没有成功，这里还是介绍一下`git reset --hard HEAD^`，这个`HEAD^`就是上面介绍的含义

到这我们就学会了如何使用github来进程版本控制了，下面介绍一些新内容
再记录一下关于git中区的介绍:
 - git add是将工作区的文件保存再暂存区
 - git commit是将暂存区中的文件放到版本库中
 - git push可以将版本库中的文件存在远程服务仓库中
 - git pull可以从远程仓库中下载相应的文件
 - git diff可以查看工作区和暂存区文件的差异
 - git status可以查看工作区文件的情况