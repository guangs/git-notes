## Git“添加”代码的主要操作有：

- git commit

- git merge
- git rebase
- git fetch

- git cherry-pick
- git pull 等价于 git fetch + git merge
- git pull --rebase 等价于 git fetch + git rebase


## Git rebase

在rebase的过程中，有时也会有conflict，这时Git会停止rebase并让用户去解决冲突，解决完冲突后，用git add命令去更新这些内容，然后不用执行git-commit,直接执行git rebase --continue,这样git会继续apply余下的补丁