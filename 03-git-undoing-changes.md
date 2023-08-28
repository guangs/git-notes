## Git“删除”代码的主要操作
- git reset
- git revert
- git restore


## Git各阶段的撤销操作（“删除”代码）
- 未跟踪文件(Untracked files)
- 工作区(Workspace)的撤销操作
- 暂存区(Staging Area)的撤销操作
- 本地仓库(Local Repository)的撤销操作
- 远程仓库(Remote Repository)的撤销操作


### 未跟踪文件: 从来没有执行过git add操作
这个时候文件的修改和撤销操作git是无法追踪的，但可以删除为跟踪文件
```shell
git clean -f filename
```

### 工作区阶段：跟踪文件, 新的改动还没有执行git add

```shell
# 撤销当前目录所有文件内容的修改，恢复到本地仓库上次commit时的状态
git checkout . 

# 撤销某个文件内容的修改，恢复到本地仓库上次commit时的状态
git checkout filename

# 撤销所有文件内容的修改，恢复到本地仓库上次commit时的状态
git reset --hard 
```

### 暂存区阶段：执行了git add，但是还没有git commit

```shell

# 将所有文件从暂存区撤销, 回到工作区，但是已经修改的内容不会撤销
# 退回到了git add . 之前的状态
git reset

# 将某个文件从暂存区撤销, 回到工作区，但是已经修改的内容不会撤销
# 退回到了git add filename 之前的状态
git reset filename

# 撤销所有文件内容的修改，恢复到本地仓库上次commit时的状态，暂存区也被清空
git reset --hard 

# 将所有文件从暂存区撤销, 回到工作区，但是已经修改的内容不会撤销
# 退回到了git add . 之前的状态
git restore --staged .

# 将某个文件从暂存区撤销, 回到工作区，但是已经修改的内容不会撤销
# 退回到了git add filename 之前的状态
git restore --staged filename

# 丢弃工作区的所有文件的改动，暂存区的已有改动仍保留
git restore .

# 丢弃工作区的某个文件的改动，暂存区的已有改动仍保留
git restore filename
```

### 本地仓库阶段：执行了git commit，但是还没有git push
```shell
# 撤销本地仓库的改动, 重置为服务器端的最新版本
git reset --hard origin/master

# 撤销本地仓库的改动, 重置为本地的某次commit，随后的commit都会被删除，因为这会丢失git的历史记录，所以注意  
# - 这个操作一定不能在公共的分支上进行
# - reset的id节点一定不要是在remote header之前的节点
git reset --hard <commit id or head~n>

# 撤销本地仓库的改动, 单单撤销某一次的commit，随后的commit不会被删除，revert是通过新创建commit的方式来撤销之前某次commit的修改，历史记录不受影响
git revert <commit id or head~n>
```


### 远程仓库阶段：已经执行了git push
```shell
# 撤销上次的提交
git revert HEAD 
# 撤销上上次的提交，注意：数字从0开始 
git revert HEAD~1 
# 撤销某次的提交， 0ffaacc是commit id
git revert 0ffaacc

# 本地revert之后，在将更新push到远程仓库, master分支
git push origin master
```

