```
#提交到本地仓库
git add 路径 
git commit -m/-v

# 提交到远程仓库
git remote add origin git@XXXX
git branch  -M  main
git push -u origin main 

# 简单
git add
git commit -m
git push

# 下载
git clone  git@XXXXX

#报错:git push 时候出现Everything up-to-date问题

# 新建分支
git branch new branch

# 切换分支
git checkout new branch

#继续提交
git add
git commit

# 切换到主分支
git checkout main

# 合并
gei merge new branch

# 提交到远程
git push

# 查看冲突
 git diff

# 删除分支
git branch -D new branch

# 拉取远程最新代码
git pull = git fetch + git merge             
//git pull比下面的多一个分叉
git pull --rebase = git fetch + git rebase 

git pull发生冲突时
撤回git pull
git reflog main //查看分支历史变更
git reset --hard main@{} //然后撤回
再拉取新代码
git pull --rebase
修复 bug:main|REBASE 1/4 
git pull --abort
```
