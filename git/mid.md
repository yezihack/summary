# git中级使用

> 查看git日志

```json
#查看日志
git log 

#查看所有分支的所有操作记录
git reflog 

#将日志显示为一行,方便查看
git log --oneline
```




> 回退版本

可以回退任何版本
还可以回退已回退的版本,使用git reflog查看commit id

```json
#log_id就是git log列出来的commit id
git reset --hard log_id

```

> 查看分支和远程分支
 
- 分支前面有个*星号代表当前分支
- 如果分支名前名有origin代表远程分支
- 如果分支信息里有中括号,如[origin/master]代表本地分支与远程分支关联在一起

```json
#查看本地分支
git branch 

#查看远程分支 
git branch -r 

#查看本地和远程所有的分支
git branch -a 

#查看分支简明信息
git branch -v 

#查看分支详情信息,包括关联远程状态
git branch -vv 

```

> 分支切换并创建

```json
#分支切换
git checkout 分支名

#创建新分支并自动切换之
git checkout -b 新分支名

#将远程分支拉到本地新建分支并与之关联再切换之
git checkout -b 新分支名 origin/远程分支名

```

> 基于某分支创建分支

```json
#基于当前分支创建新分支 
git branch 新分支

#基于当前分支创建新分支并切换之
git checkout -b 新分支

```

> 本地分支与远程建立关联关系

作用主要是方便远程拉取与推送

```json

#将本地分支与远程分支关联起来
git branch -u origin/远程分支名

#取消关联关系
git branch --unser-upstream

```

> 删除本地分支和远程分支

```json
#删除本地分支
git branch -D 分支名

#删除远程分支 
git push origin :master 
或
git push origin --delete master 

```

> 同步远程分支

```json
#正常推送
git push origin master

#-u参数是代表下次无需加origin master,已经将远程分支关联到本地分支了.使用git branch -vv验证
git push -u origin master
```

