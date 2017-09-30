# Git命令
### 配置

##### 配置账号信息
```
git config --global user.name dzqlx1993

git config --global user.email dzq1993@qq.com

git config --list #查看配置的信息

git help config #获取帮助信息
```
##### 配置自动换行
```
git config --global core.autocrlf input #提交到git自动将换行符转换为lf
```
##### 配置密钥
```
ssh-keygen -t ras -C dzq1993@qq.com #生成密钥
ssh -T git@github.com #测试是否成功
```
##### 新建仓库
```
git init #初始化仓库

git status #查看当前仓库状态

git add file #添加文件（.或者*表示全部添加）

git commit -m "commit message" #提交代码

git remote add origin git@github.com:xxxx.git #添加远程仓库

git push -u origin master #push本地代码到远程仓库
```
##### 从现有仓库克隆
```
git clone git://xxxxx.git

git clone git://xxxxx.git myresposity #克隆到本地指定文件夹
```
##### 本地
```
git add * #跟踪所有新文件

rm &git rm #移除文件

git rm --cached * #取消跟踪

git mv file_from file_to #重命名跟踪文件

git log #查看提交记录

git commit -a #直接提交，跳过暂存步骤

git commit --amend #修改最后一次提交

git reset HEAD * #取消已经暂存的文件

git checkout -- file #取消对file的修改（从暂存区除去file）

git checkout branch|tag|commit -- file_name #从仓库中取出file覆盖当前分支下的该文件

git checkout -- . #从暂存区去除文件的覆盖工作区
```
##### 分支
```
git branch #列出本地分支

git branch -r #列出远程分支

git branch -a #列出所有分支

git branch -merge #查看已经合并到当前分支的分支

git branch --no--merge #查看未合并到当前分支的分支

git branch test #新建test分支

git checkout test #切换到test分支

git checkout -b test #新建test分支并且切换到test分支

git checkout -b dev test #基于test新建dev分支并且切换到dev分支

git branch -d test #删除test分支

git branch -D test #强制删除test分支

git merge test #将teset分支合并到当前分支

git rebase master #将master分支上超前的提交，编辑到当前分支
```
##### 远端
```
git fetch originname branchname #拉去远端上指定分支

git merge originname branchname #合并远端上指定分支

git push originname branchname #推送到远端上指定分支

git push originname localbranch:serverbranch #推送到远端上指定分支 

git checkout -b test origin/dev #基于远端dev新建test分支

git push origin :br  #删除远端分支
```

##### 源

git是一个分布式代码管理工具，所以可以支持多个仓库，在git里，服务器上的仓库在本地称之为remote。个人开发时，多源用的可能不多，但多源其实非常有用。

```
git remote add origin1 git@github.com:yanhaijing/data.js.git

git remote #显示全部源

git remote -v #显示全部源+详细信息

git remote rename origin1 origin2 #重命名

git remote rm origin1 #删除

git remote show origin1#查看指定源的全部信息
```
##### 标签

当开发到一定阶段时，给程序打标签是非常棒的功能。

```
git tag #列出现有标签

git tag v0.1 #新建标签

git tag -a v0.1 -m 'my version 1.4' #新建带注释标签

git checkout tagname #切换到标签

git push origin v1.5 #推送分支到源上

git push origin --tags #一次性推送所有分支

git tag -d v0.1 #删除标签

git push origin :refs/tags/v0.1 1#删除远程标签

```
