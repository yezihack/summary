# 高级使用

> 查看远程仓库地址

```
git remote -v 查看远程仓库地址
git remote show origin 查看所有远程创库详细
git remote add origin(名称,随意) 远程git地址
```

> 暂存工作进度

```json
git stash 保存当前工作进度
Git stash pop 恢复当前工作进度
git stash list 查看
Git stash clear 清理
```

> 回退远程仓库版本

- 首先在本地回退版本,然后再将本地版本强推送到远程,实现远程仓库回退

```json
git push -f origin HEAD:master
```

> 设置配置

```json
#查看
Git config user.name
Git config user.email

#设置全局的
git config --global user.name "admin"
git config --global user.email admin@example.com

#设置当前项目的
git config user.name "admin"
git config user.email admin@example.com


```

> 建立别名

```json

git config --global -e

#将下面代码复制进支

[alias]
        st = status
        co = checkout
        ci = commit
        br = branch
        brr = branch -vv
        brv = branch -r
        unstage = reset HEAD
        last = log -1
        lg = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
        info = log --stat --graph --oneline --relative-date --abbrev-commit --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
        desc = log --stat --graph --oneline --relative-date --abbrev-commit -p --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
        self = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)
        <%an>%Creset' --abbrev-commit --author=你的名称
        info = --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) \na\n

或者直接运行
#查看所有提交的每个文件修改详情
git log --stat --graph --oneline --relative-date --abbrev-commit -p --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'  

— 制作别名
git config --global alias.desc "log --stat --graph --oneline --relative-date --abbrev-commit -p --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'"

#查看所有的提交的文件 
git log --stat --graph --oneline --relative-date --abbrev-commit --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' 

git config --global alias.info "log --stat --graph --oneline --relative-date --abbrev-commit --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'" 

#简洁的所有提交信息
git log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

git config  --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"


git log  --graph --stat --color --abbrev-commit --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' 

```