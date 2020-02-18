# github学习教程
1. 首先我们要知道github是干什么的，github是一个版本控制工具，可以记录你每次提交的code的变化的情况，嗯，大概就是这样。
2. 一下是github几个常用的命令：
- git init 新建一个空的仓库
- git status 查看仓库的状态
- git add + file 向仓库中添加文件
- git commit -m '说明' 先仓库中添加文件后的备注说明
- git push -u origin master 将本地的仓库推送到远程的仓库
- git log 查看变更日志
- git reset -0hard 版本号前六位 回归指定的版本
- git branch 查看分支
- git branch newname 创建一个名叫newname的分支
- git checkout branch_name 切换到名叫branch_namde的分支上
- git merge branch_name 将名叫branch_namde的分支合并到当前的分支上
- git pull origin master 将master分支的内容拉到本地
- git diff file_name 可以查看文件的变化