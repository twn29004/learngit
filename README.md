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
- 我看网上教程还有一种使用`HEAD`的命令，但是自己试验并没有成功，这里还是介绍一下`git reset --hard HEAD^`，这个`HEAD^`就是上面介绍的含义。*补充：在官方文档看到了关于`HEAD`这个东西的一种使用方法，`git reset HEAD <file_name>`,可以取消暂存,至于前面那个命令，俺也⑧知道咋回事*

到这我们就学会了如何使用github来进程版本控制了，下面介绍一些新内容
再记录一下关于git中区的介绍:
 - `git add`是将工作区的文件保存再暂存区
 - `git commit`是将暂存区中的文件放到版本库中，**养成好好写commit的习惯，非常重要，同时commit才是提交到版本库的最终操作**
 - `git push`可以将版本库中的文件存在远程服务仓库中
 - `git pull`可以从远程仓库中下载相应的文件
 - `git diff`可以查看工作区和暂存区文件的差异
 - `git status`可以查看工作区文件的情况
 - `git diff HEAD -- README.md`可以查看当前工作区与版本库中最新版本的区别

 4. 关于撤销操作的命令

 - 如果我们提交之后发现漏掉了几个文件没有添加，或者提交信息写错了，可以使用`git commit --amend`重新提交,如果是漏掉了文件，可以这样操作
    ```
      git commit -m 'initial commit'
      git add forgttoen_file
      git commit --amend
    ```
  - `git chechout -- file_name`可以将工作区的文件撤回到最近一次`git add`或者`git commit`的状态，回顾一下前面的三大分区的内容，`git add`表示的是暂存区的内容，`git commit`表示版本库的内容。`--`表示的是分支，这个之后再介绍。看到官方文档的一句话:**你需要清楚的知道该命令是一个危险的命令，你对文件做的任何修改都会消失，你只是拷贝了一个文件来覆盖他**,听说新版的已经将`checkout替换为resotre`,
  - `git reset HEAD file_name`其作用是撤销暂存。如果在调用的时候加上`--hard`将让`git reset`成为一个危险的命令，**可能导致当前工作目录所有当前进度丢失**，不加选项的调`git reset`并不危险，他只会**修改暂存区域，不会修改工作区**。emmm,如果这里不懂的的话，可以自己这样操作一下，先add一个文件，使用`git status`查看当前仓库的状态。可以看到文件已经被暂存了，然后在使用这条命令，再执行`git status`可以看到文件变为未暂存了。emmm,我试了一下，就是虽然取消了暂存，但是不会将工作区的内容撤回到上一次`git add`的内容，只是将状态改变为`unstage`
  - 一般我们删除文件都是直接在文件管理器中删除，这时使用`git status`,这是Git将会告诉你有文件被删除了，因为工作区与版本库不一致了，这时你有两种选择，一个是确实要从版本库中删除，这时可以使用`git rm`删除这个文件，并且要`commit`,如果这是误删,可以使用`git checkout file_name`,从版本库中恢复。如果一个文件已经提交到版本库了，永远不担心误删，但是**只能恢复到文件的最新版本**，你会丢失**最近一次提交后你修改的内容。**，那么误删了之后怎么恢复呢。`git checkout -- README.md`就ok了。听说在新版本的Git中`git checkout`被`git restore`替代了。
  - **记住在Git中，你提交的所有东西几乎都是可以恢复的，但是未提交的就不一定能找回来了**
  - 补充:执行`git status`时，会顺带输出一些恢复操作的命令,eg`git restore <file>` to discard changes in working directory.`git restore --staged <file>` to unstaged
  - 这里分享一个看到的问题，就是先`git add`一个文件，修改之后再`git add`，中间没有`git commit`,然后再`git commit`，此时版本库中是最近一次的文件。原因是`git add`是将文件加入跟踪列表，而每一次跟踪是以commit为准的。

5. 连接远程仓库
    1. 到目前为止，我们的代码都还是保存在本地的那么怎么推送给远程仓库呢，首先我们应该让github的服务器知道我是我，这就需要我们生成一个密钥了。使用如下命令`ssh-keygem -t rsa -C youremail@email.com`后面就是你注册github的邮箱，然后就可以一路回车了，然后你就可以在用户的目录下发现一个.ssh文件夹，里面有两个文件，一个是公共密钥，一个是私有密钥，公共密钥可以放心的告诉别人，但是应该保存好私有密钥。
    2. 生成好密钥之后，我们可以登录github网站，点击头像下方发Setting,找打ssh and GPGkeys，new sshkey，将生成的公共密钥粘贴到里面(随便起一个title,eg:家里电脑的ssh),以上我们便连接上了github的服务器。
    3. 然后在github上创建一个仓库(repository)。这里我将该仓库命名为learngit
    4. 使用`git remote add origin git@github.com:twn29004/git_name.git`解释一下这个命令，增加名叫`origin`的远程仓库，同时与在github上创建的名为`git_name`的仓库关联起来，其他的都是固定的貌似(暂时的理解是这样) 
    6. `git push -u origin master`将本地文件上传至远程仓库,由于第一次推送`master`分支，加上`-u`参数，Git不但会把本地的`master`分支内容推送到远程仓库的新的`master`分支，还会把本地的`master`分支与远程的`master`分支关联起来，以后的推送就可以只用`git push origin master`

6. 将远程仓库克隆到本地。`git clone git@github.com:user_name/git_name.git`,也可以使用git提供的连接进行Clone.`git clone url`,这里github提供了多种协议，git协议和https协议。如果想使用git协议可以在CloneorDownloag那点击use ssh连接就会变为git协议。听说git协议更快一点.补充(windos中查看文件目录下所有文件的名字的命令为`dir ./b`),需要特别注意的是，**这里的是用户名，不是你注册的邮箱，是你注册的用户名**

7. 下面是除了仓库外，github中的另一个东西------Branch(分支)，分支的功能相当于一个岔路，嗯，可以这么说，举个例子，你现在已经有了一个完整的项目，项目是可以正常运作的。但是你现在想新添加一些功能。但是这个新功能不是很快就可以添加的，所以，如果你要修改新功能的话，现有的项目就不能正常运行了。这个时候`Branch`的好处就体现出来了，你可以新建一个分支，然后她并不影响你原有的项目，你也可以高兴的添加新功能，当你新功能添加完成后，还可以合并两个分支。
关于分支的介绍可以参考[廖雪峰老师的教程](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424),下面介绍一些分支的常用命令:
- `git checkout -b dev` `git checkout`命令加上`-b`表示创建并切换分支，相当于这两条命令`git branch dev`,`git checkout dev`.
- `git branch`会列出所有的分支，并在当前分支前标`*`
- `git merge branch_name`将名为branch_name的分支与当前分支合并，如果分支存在冲突，我们将手动处理冲突。
- `git branch -d branch_name`将名为branch_name的分支删除，**不能删除自己正在的那个分支，不能自己杀自己嘛**
- `git log --graph`可以查看分支合并图。
- 补充，由于前面讲到的撤销操作的命令也是`git checkout -- file_name`，这就很迷惑了，Git还有一种切换分支的命令为`git switch branch_name`,`gti switch -c branch_name`,创建并切换
最后，Git鼓励大量使用分支！
- 补充:在提交的过程中出现了一个这样的错误`nothing added to commit but untracked files present`,意思就是还有未提交文件的存在。如果不想提交这些文件，可以新建一个`.gitignore`将不需要提交的文件加在里面，如果需要提交的话就一一提交就ok了[参考连接](https://blog.csdn.net/qq_40170358/article/details/79866936)
<<<<<<< HEAD
dwiedjowckdd
=======
Create branch is simple & quick
>>>>>>> test
