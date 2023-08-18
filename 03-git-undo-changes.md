## Git各阶段的撤销操作
- 未跟踪文件(Untracked files)
- 工作区(Workspace)的撤销操作
- 暂存区(Staging Area)的撤销操作
- 本地仓库(Local Repository)的撤销操作
- 远程仓库(Remote Repository)的撤销操作


### 未跟踪文件: 从来没有执行过git add操作
这个时候文件的修改和撤销操作git是无法追踪的

### 工作区阶段：还没有执行git add到暂存区

- git checkout . 
- git checkout filename
- git reset --hard 

### 暂存区阶段：

执行了git add，但是还没有git commit
git checkout . （
撤销暂存区改动
）
git reset --hard （
撤销暂存区改动
）
git reset 
（
撤销暂存区改动，是把修改退回到了git add .之前的状态，也就是说文件本身还处于已修改未暂存状态，你如果想退回未修改状态，还需要执行git checkout .
）

### 本地仓库阶段：
已经执行了git commit，但是还没有git push
git reset --hard origin/master （撤销本地仓库的改动）

### 远程仓库阶段：
已经执行了git push
git revert HEAD （撤销到上次修改之前的状态）
git revert HEAD~1   （撤销上上次的提交，注意：数字从0开始 ）
git revert 0ffaacc        （撤销0ffaacc这次提交）
git push （本地revert之后，在将更新push到远程仓库）

git push origin -d <branch name>
