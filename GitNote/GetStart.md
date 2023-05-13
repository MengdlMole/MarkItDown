Hello Git!
# Basic Code
## 初始化：
git init
## 查看日志：
git log
### 配置别名 git-log
touch ~/.bashrc
vim ~/.bashrc
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
alias ll='ls -al'
source ~/.bashrc
## 查看状态：
git status
## 添加到缓存区：
git add
## 删除文件
git rm -rf ***.txt
Hint: 不要rm -rf * !!!
## 提交：
git commit -m "说明"
## 历史日志：
git reflog
## 回退：
git reset --hard commitID 
## 查看分支：
git branch
## 创建分支：
git branch branchName
## 常用分支：feature -> develop -> master，还有 hotfix, test, pre
## 切换分支：
git checkout branchName
## 创建并切换分支：
git checkout -b branchName
## 合并分支：
git merge branchName
## 如果有冲突会将冲突位置标注，手动解决后可add和commit
## 检查并删除分支：
git branch -d branchName
## 强制删除分支（不进行检查）：
git branch -D branchName
## 未完全 merge 时可用 -D 强制删除
## 删除分支后推送到远程
git push --delete MarkItDown iPad
## 重命名分支名称：
git branch -M main
## windows 生成密钥对：
ssh-keygen -t rsa
## 测试连接 github：
ssh -T git@github.com
## 添加远程仓库：
git remote add origin http://...
## 查看远程仓库：
git remote
## 将本地 push 到远程仓库：
git push origin main
git push origin main:main
git push [-f] [--set-upstream] [远端名称 [本地分支名][:远端分支名]]
git push
## -f : 强制覆盖
## --set-upstream:push 时建立对应关系
## 查看对应关系：
git branch -vv
## 从远程仓库克隆：
git clone <仓库路径> [本地目录]
## 从远程仓库抓取：
git pull
## fetch+merge
## 从远程仓库拉取：
git fetch
git merge origin/main
## 远程分支也是分支
