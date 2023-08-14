## git merge的简单过程
### 情况1（fast-forward）
1. 开始状态
   ```
   master branch:  a -> b
   feature branch: a -> b -> c
   ```
2. master branch merge feature branch
   ```
   master branch:  a -> b -> c
   feature branch: a -> b -> c
   ```
### 情况2（no-fast-forward）
1. 开始状态
   ```
   master branch:  a -> b -> d
   feature branch: a -> b -> c1
   ```
2. feature branch merge master branch（此时feature c没开发完，只完成了c1但是需要同步 master上最新的改动d，来做测试）
   ```
   master branch:  a -> b -> d
   feature branch: a -> b -> c1 -> d -> 1st-merge-commit
   ```
3. feature branch 上增加c2，完成了feature c的所有代码， master branch 进了新的feature e
   ```
   master branch:  a -> b -> d -> e
   feature branch: a -> b -> c1 -> d -> 1st-merge-commit -> c2
   ```
4. feature branch merge master branch (feature c开发完，需要同步 master上最新代码，做测试)
   ```
   master branch:  a -> b -> d -> e
   feature branch: a -> b -> c1 -> d -> 1st-merge-commit -> c2 -> e -> 2nd-merge-commit
   ```
5. master branch merge feature branch
   ```
   master branch:  a -> b -> c1 -> d -> 1st-merge-commit -> c2 -> e -> 2nd-merge-commit
   feature branch: a -> b -> c1 -> d -> 1st-merge-commit -> c2 -> e -> 2nd-merge-commit
   ```
## git rebase的简单过程
### 情况1（fast-forward）
1. 开始状态
   ```
   master branch:  a -> b
   feature branch: a -> b -> c
   ```
2. feature branch rebase master branch
   ```
   master branch:  a -> b
   feature branch: a -> b -> c
   ```
3. master branch merge feature branch
   ```
   master branch:  a -> b -> c
   feature branch: a -> b -> c
   ```
### 情况2（no-fast-forward）
1. 开始状态
   ```
   master branch:  a -> b -> d
   feature branch: a -> b -> c1
   ```
2. feature branch rebase master branch（此时feature c没开发完，只完成了c1但是需要同步master上最新的改动d，来做测试）
   ```
   master branch:  a -> b -> d
   feature branch: a -> b -> d -> c1
   ```
3. feature branch 上增加c2，完成了feature c的所有代码， master branch 进了新的feature e
   ```
   master branch:  a -> b -> d -> e
   feature branch: a -> b -> d -> c1 -> c2
   ```
4. feature branch rebase master branch (feature c开发完，需要同步master上最新代码，做测试)
   ```
   master branch:  a -> b -> d -> e
   feature branch: a -> b -> d -> e -> c1 -> c2
   ```
5. master branch merge feature branch
   ```
   master branch:  a -> b -> d -> e -> c1 -> c2
   feature branch: a -> b -> d -> e -> c1 -> c2
   ```
## git merge与git rebase的区别
- rebase不会创建额外的merge commit信息
- rebase会把一个feature不同时间的commit，都集中在一起
## 个人心得
- git rebase相比git merge，可以使历史记录更加清晰
- git merge相比git rebase，更加简单安全
- feature branch同步master branch更建议用rebase（feature branch同时有多个developer提交代码的情况除外）
- master branch同步feature branch更建议用merge