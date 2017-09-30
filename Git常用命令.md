# Git常用命令

### 1.放弃本地修改
```
git checkout . && git clean -df
```
### 2.删除本地修改
```
git branch -D br //br为branch name
```
### 3.删除远程分支
```
git push origin :br //br为branch name
```
### 4.本地代码回滚
```
回滚到commit-id,将commit-id之后提交的commit都去除
	git reset --hard commit-id  //id为commit时的id
将最近3次的提交回滚
	git reset --hard HEAD~3
```
### 5.远程代码回滚
先将本地分支退回到某个commit，删除远程分支，再重新push本地分支

```
git checkout br
git pull
git branch br_backup //备份一下当前这只分支的情况
git reset --hard thi_commit_id //把the_branch本地回滚到the_commit_id
git push origin :the_branch //删除远程分支
git push origin the_branch //用回滚后的本地分支重新建立远程分支
git push origin :the_branch_backuo //如果当前面都成功了，删除这个备份分支
