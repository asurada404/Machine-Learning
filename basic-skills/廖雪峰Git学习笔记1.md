# [廖雪峰Git](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)学习笔记
- [会做数学的厨子](https://github.com/xiaochuhub) 20170408
## 1. Git安装
```shell
 $ sudo apt-get install git
 #配置个人信息
 $ git config --global user.name "Your Name"
 $ git config --global user.email "email@example.com"
```
- 安装GitGUI https://git-scm.com/download/gui/linux
- GitKraken比较cool https://www.gitkraken.com/
-----------------------------------------------------
## 2. 创建版本库
```shell
$ mkdir git-learn
$ cd git-learn
$ git init #初始化Git仓储
$ git add readme.txt #文件添加到仓储
$ git commit -m "wrote a readme file" #提交文件 -m "说明信息"
```
-------------------------------------------------------

## 3. 版本信息及修改
```shell
#查看Git状态
$ git status
#查看file的改动信息
$ git diff filename
#查看改动日志
$ git log
#退回到上一个版本（ HEAD^表示上一个版本，HEAD~x表示上x个版本
$ git reset --hard HEAD^
$ git reset --hard HEAD~x
#通过版本id（commit_id)退回到原来的版本
$ git reset --hard commit_id
#查看命令历史
$ git reflog
```
- HEAD 版本头
- commit_id  提交（版本）id
```
------------------------------------------------------------

## 4. add → commit：暂缓区 → 分支
### 创建，添加到暂缓区

![](https://raw.githubusercontent.com/xiaochuhub/MarkdwonImg/master/create-add.jpg)

### 提交暂缓区的文件到master

![](https://raw.githubusercontent.com/xiaochuhub/MarkdwonImg/master/add-commit.jpg)

-------------------------------------------------------------
## 5. 撤销修改
```shell
$ git chekout -- filename
```
- 回到最近一次git add 或者还没有add时的状态
- readme.txt自修改后还没有add到暂存区，撤销修改就回到和版本库一模一样的状态
- readme.txt已经add暂存区后，又作了修改，撤销修改就回到添加到暂存区后的状态
- 如果已经add commit到版本库可以使用reset退回

-----------------------------------------------------------------
## 6. 关联远程库
```shell
#本地库关联远程库
$ git remote add origin git@server-name:path/repo-name.git
#第一次推送master分支的所有内容
# origin为远程库的Name
$ git push -u origin master
#随后的本地提交后
$ git push origin master

```
-----------------------------------------------------------------
## 7. 从远程库下载
```shell
#git协议比http快
$ git clone git@github.com:xiaochuhub/mmd.git
$ git clone https://github.com/xiaochuhub/mmd.git
```
-----------------------------------------------------------------
## 8. 创建和合并分支
```shell
#查看分支
$ git branch
#创建分支
$ git branch <name>
#切换分支
$ git checkout <name>
#创建+切换分支
$ git checkout -b <name>
#合并某分支到当前分支
$ git merge <name>
#删除分支
$ git branch -d <name>

```
### 演示动画
```HTML
<video id="video" controls="" preload="none" poster="http://media.w3.org/2010/05/sintel/poster.png">
      <source id="mp4" src="https://rawgit.com/xiaochuhub/MarkdwonImg/master/videos/master-and-dev-ff.mp4" type="video/mp4">

      <p>Your user agent does not support the HTML5 Video element.</p>
</video>
```
-----------------------------------------------------------------
## 9. 冲突
```shell
$ cat README.md
<<<<<<< HEAD
xxxxxxxWWWWWWLLLLLLLL   # 这是来自当前分支的修改
=======
xxxxxxxaAAAAAAA            # 这是来自feature1分支的修改
>>>>>>> feature1

$ git log --graph --pretty=oneline --abbrev-commit
*   59bc1cb conflict fixed
|\
| * 75a857c AND simple
* | 400b400 & simple
|/
* fec145a branch test
...

```
-----------------------------------------------------------------
## 10. 分支结构(分支使用)

![](https://cdn.rawgit.com/xiaochuhub/MarkdwonImg/592ac149/Img/branch-structrue.png)
``` shell
$ git branch -D branchname #强行删除分支（未合并）
```

-----------------------------------------------------------------
## 10. Bug 分支
```shell
#保存手头的工作，创建新的分支修bug
$ git stash #保留现场
$ git stash list #查看现场
$ git stash pop #回到现场，并删除现场记录
$ git stash apply #回到现场，保留现场记录
$ git stash drop  #删除现场记录
```
-----------------------------------------------------------------
## 11. 多人协作
```shell
$ git remote -v #查看远程库信息
$ git push origin master #推送master分支到远程库
$ git push origin dev #推送dev分支到远程库
```
- master分支是主分支，因此要时刻与远程同步；
- dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

-----------------------------------------------------------------
## 12. tag
### tag是commit id的语义化（快照，不能移动的分支
```shell
#打标签(省略commit_id就是为当前状态打ｔａｇ)
$ git tag <name> commit_id
#打标签并附上说明信息
$ git tag -a <name> -m 'guide message'  commit_id
＃打PGP标签，必须安装GPG
$ git tag -s <tagname> -m 'guide message' commit_id
＃查看标签
$ git tag　
#推送tag到远程
$ git push origin  <tagname>
#推送所有的tag到远程
$ git push origin  --tags
＃删除所有的tag
$ git tag -d <tagname>
#删除远程tag
$ git push origin :refs/tags/<tagname>
```
