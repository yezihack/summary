#git 使用

### 工作中常用到的命令

> 提交本地仓库 

```json
#查看git状态
git status 

#查看哪些代码修改了
git diff 

#将修改的文件提交到暂存区
git add .
(.点代表所有,如果需要指定文件添加,直接写文件路径)
git add app/file.go

#提交到本地仓库
git commit -m "注释,一定要写好注释"

```

> 合并代码

A分支合并到B分支,先切换B分支下,然后再执行git merge A 

```json
#查看本地所有分支
git branch 

#切换到B分支
git checkout B

#将A分支合并到B分支
git merge A 
```

> 将本地代码提交到远程分支

将本地B分支提交到远程的C分支

```json
git push origin C
```

> 拉取与推送远程仓库

```json
#拉取
git pull origin master

#推送
git push origin master

```