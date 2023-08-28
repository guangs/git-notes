## 重写Git的提交历史，主要方法有
- git commit --amend
- git rebase -i
> 注意所有修改git提交历史的操作都不要在公共的分支上执行

## git commit --amend
```shell
# 对最近的一次提交进行修改，默认情况下会弹出编辑窗口，在编辑窗口可以修改commit message信息
git commit --amend

# 对最近的一次提交进行修改，并提供新的commit message，此时不会再弹出编辑窗口
git commit --amend -m "new message"

# 对commit message不做修改，只做代码修改
git commit --amend --no-edit
```

## git rebase -i

### scenario1: 合并多个commits(squash)
```shell
git rebase -i head~5
```
![scenario1](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*YAQwxKiMNjs8rToiTni_qg.png)

### scenario2: 编辑多个commit message
```shell
git rebase -i head~4
```
![scenario2](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*BkmjnKSirDrroTBc_p4tww.png)

### scenario3: 删除某次的commit
```shell

# 假设想去掉commit 7df0321
git log --oneline
9c19114 (HEAD -> dev, main) 5.txt
0e14c45 4.txt
7df0321 3.txt
92ddaa5 2.txt
25613cb 1.txt

# 回到7df0321的前一次commit，92ddaa5
git rebase -i 92ddaa5

# 在编辑对话中，将7df0321前面的pick改为drop(d)，保存退出即可
d 7df0321 3.txt
pick 0e14c45 4.txt
pick 9c19114 5.txt

# 再次查看git history，发现7df0321已经被移除
git log --oneline
476c831 (HEAD -> dev) 5.txt
25024f6 4.txt
92ddaa5 2.txt
25613cb 1.txt

# 如果需要强制推送到remote repository，则执行
git push --force-with-lease
```


## Reference
- [5 Useful Tricks To Rewrite Your Git History](https://betterprogramming.pub/5-useful-tricks-to-rewrite-your-git-history-92268f8b6933)
- [rewriting-history](https://www.atlassian.com/git/tutorials/rewriting-history)