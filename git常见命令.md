## git常见命令
1. git init
   - 初始化一个新的Git仓库
2. git clone [url]
   - 从远程仓库克隆一个项目到本地
3. git add [file]
   - 将文件添加到暂存区
4. git commit -m "commit message"
   - 提交暂存区的文件到本地仓库
5. git push
   - 将本地仓库的提交推送到远程仓库
6. git pull
   - 从远程仓库拉取最新的提交到本地
7. git branch
   - 列出所有本地分支
8. git checkout [branch]
   - 切换到指定分支
9. git merge [branch]
   - 将指定分支的提交合并到当前分支
10. git status
    - 显示工作区和暂存区的状态
11. git log
    - 显示提交日志
12. git remote -v
    - 查看远程仓库的地址
13. git reset [file]
    - 从暂存区中移除文件
14. git stash
    - 将当前工作目录的改动暂存起来
15. git pull --rebase
    - 从远程仓库拉取最新的提交并进行变基操作

## 基础语法：

- git [command] [options] [arguments]
- command：表示要执行的命令，如init、clone、add等
- options：表示命令的选项，如-m表示提交消息
- arguments：表示命令的参数，如文件名、分支名、远程仓库地址等