### 常用命令

- git init（创建版本库）
- git add "fileName"（将修改文件加入提交列表）
- git commit -m "注释"（提交）
- git log（查看版本）
- git log --pretty=oneline（查看版本，单行显示）
- git reset --hard HEAD^  （返回上一个版本）
- git reset --hard 1094a（返回到某版本，版本号没必要写全，前几位就可以了，Git会自动去找）
- git reflog（用来查询你的每一次命令）
- get status （查看状态）
- git diff HEAD --fileName（查看工作区和版本库里面最新版本的区别）
- git checkout -- fileName（丢弃工作区的修改）
- git reset HEAD fileName（把暂存区的修改撤销掉，重新放回工作区）
- get rm "fileName"（删除文件）

- `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。



### 远程仓库

- 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；
- 关联一个远程库时必须给远程库指定一个名字，`origin`是默认习惯命名；
- 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；
- 此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；
- 如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息：
- `git clone git@github.com:server-name/repo-name.git`克隆一个本地库



### 分支管理

- 查看分支：`git branch`

- 创建分支：`git branch <name>`

- 切换分支：`git checkout <name>`或者`git switch <name>`

- 创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

- 合并某分支到当前分支：`git merge <name>`

- 删除分支：`git branch -d <name>`

- `git stash`可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作

- 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

- 当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

- 在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。
- 多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

### 标签

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。
- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。

### 配置

- `git config --global user.name "Your Name"`配置用户名
- ` git config --global user.email "email@example.com"`配置邮箱地址
- 