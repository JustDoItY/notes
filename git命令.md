# git命令

## 一. 克隆，提交，拉取代码

### 1. 克隆，提交代码
- git clone：远端仓库地址
- git remote add upstream： 上游远端仓库地址（fork代码的原地址）。添加上游远端仓库
- git add -A
- git commit -m '描述'
- git push

### 2. 从上游远端仓库拉取冲突代码，解决冲突

- git pull upstream master -r：把冲突部分拉下来，使用rebase合并代码，不会产生合并信息，不使用rebase确实回产生的。pull细节：把工作区的修改暂存起来，把远端代码和上一次提交合并，然后把暂存的修改再合并到分支上
- git add -A
- git rebase --continue：重新提交代码文件，不会产生额外的commit。如果合并的分支中存在多个commit，需要重复处理多次冲突。 只有处理冲突时候才能用这个命令。
- git push -f：强制提交代码

### 3. 修补最近一次的提交

- git commit —amend(-a)：修补最近一次push

### 4. 拉取代码

- git pull 等价于 git fetch & git merge：这时从远端拉取代码，回产生一个合并日志，产生分叉
- git pull --rebase (-r)：使用 git rebase 合并代码

## 二. 删除远端误提交代码文件

- git rm —cached test.txt：不删除本地文件的情况下，删除远端文件
- git rm -f test.txt：删除远端文件的同时删除本地文件
- git rm -r test：删除远端文件夹的同时删除本地文件夹
- 做完上述删除动作，直接commit就好，不用add

## 三. 撤销修改

- git reset --hard version：修改本地仓库版本，把之后的修改全部清除
- git reset --soft version: 回退到这个版本，同时把之后的提交当作修改保存下来
- git reset HEAD 文件：把提交到缓存区的代码，回退到本地工作区
- git checkout --文件：撤销本地工作区的修改

## 四. 标签管理

- git tag：列出所有标签
- git show v1.0：查看标签信息
- git tag v1.0 commit：给分支打标签。在后面添加commit信息，可以把标签打到以前的commit上
- git tag -a 标签名  -m '标签描述' 1094adb：给标签写上描述
- git tag -d v1.0：删除标签
- git push origin v1.0：提交标签到远程仓库

## 五. 分支管理

- git branch：列出所有分支
- git branch &lt;branch&gt;：创建分支
- git branch -av：显示所有远程、本地分支，并显示最后提交的commit信息
- git branch -d ：小写时分支上的commit必须已经全部合并到其他分支；大写为强制删除
- git checkout <branch>：切换分支
- git checkout -b <branch>：创建并切换分支
- git merge -m '合并信息' <branch>：合并分支
- git merge --abort：放弃这次merge（同时也放弃pull）

## 六. diff

- git diff：比较修改后的文件和修改前的文件的区别
- git diff commit：比较工作区和指定提交之间的比较

## 七. log

- git log：查看日志
- git log --graph：查看提交历史图表
- git log --oneline：把提交信息整合到一行显示
- git log --stat：显示某次commit中添加行、删除行的总数

## 八. rebase

- git rebase --abort：放弃本次变基操作
- git rebase <branch>：基于某个提交（或分支）重新提交你的代码。在另一个分支提交修改代码，然后切换回master分支，执行命令，把另一个分支合并到master分支。并不会产生额外提交信息。

## 九. 初始化

- git init：初始化
- .gitignore：忽略提交文件
- README.md：代码描述文件

## 十. 暂存修改

- git stash：保存当前工作区到暂存区
- git stash list：列出当前保存的修改
- git stash pop：弹出保存的修改

## 十一. 一些心得体验
- rebase，实际上这个命令没这么难，我解说下。
- 当使用git rebase &lt;branch&gt;合并分支的时候。会把你当前的commit给去除，临时保存起来，然后把要合并的分支，从开始分叉的地方，全部搬到master分支上，然后把临时保存的commit放在头部，这样就变成了一条线。如果接下来再使用rebase，他会续借原来的分支commit，而不是放在头部
- 如果使用merge的话，会存在一个分叉，然后再合并到master上，多产生一个commit信息
-     master：commit1=>commit2
-     dev:dev1=>dev2
-     这两个分支使用rebase合并
-     commit1=>dev1=>dev2=>commit2,如果继续使用rebase，
-     commit1=>dev1=>dev2(dev分支上的commit全都会加入到这后面)=>commit2（master分支的commit全部会加入到这后面）
-      如果使用merge的话
-      commit1=>dev1=>dev2=>commit2=>merge dev(新产生一个commit信息，合并分支的)
-      dev3(dev分支会添加到commit2的下面，产生分叉)
