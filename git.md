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
# 删除远程分支
git push origin --delete new branch

# 更改远程地址
git remote  rm origin
git remote add origin url
git push /or
git push -u origin  main -f
```
