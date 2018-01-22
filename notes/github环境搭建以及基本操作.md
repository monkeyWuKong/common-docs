# GitHub

## 设置git

### 设置用户名
[Setting your username in Git](https://help.github.com/articles/setting-your-username-in-git/#platform-linux)

用户名与你的github账号是不一样的，你随时可以更改。用户名在今后的push记录中会出现。对于以前的push记录，显示的会是老的用户名。

**全局用户名**

```
$ git config --global user.name "Mona Lisa"
```
确认设置正确：
```
$ git config --global user.name
> Mona Lisa
```

**为单独的仓库设置用户名**

转到对应仓库的目录：
```
$ git config user.name "Mona Lisa"
```
确认：
```
$ git config user.name
> Mona Lisa
```

### 设置邮件地址

[Setting your email in Git](https://help.github.com/articles/setting-your-email-in-git/)

```bash
git config --global user.email "email@example.com"
#check
git config --global user.email
```

### 生成新的 SSH key 并 加入到 ssh-agent

```bash
#Generating a new SSH key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### 开始使用

#### [fork](https://help.github.com/articles/fork-a-repo/)

A fork is a copy of a repository. 

```bash
#Create a local clone of your fork
git clone https://github.com/YOUR-USERNAME/Spoon-Knife

git remote -v
```

## git 与 svn 的差异

## 日常常用命令

[Git-基础-记录每次更新到仓库](https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%AE%B0%E5%BD%95%E6%AF%8F%E6%AC%A1%E6%9B%B4%E6%96%B0%E5%88%B0%E4%BB%93%E5%BA%93)

**检查当前文件状态**

`git status`

`git status -s`

**跟踪新文件**

`git add README`

**提交更新**

`git commit`

**移动文件**

`git mv file_from file_to`

相当于：

```
$ mv README.md README
$ git rm README.md
$ git add README
```

**库上删除本地保留**

`git rm --cached README`

>以前只是了解，现在真正用的时候发现，git易用性真的不如svn，工具就是应该简单，不应该在工具上花太多时间。

## 撤销

**你提交后发现忘记了暂存某些需要的修改，可以像下面这样操作**

```bash
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

**取消暂存的文件**

```
git reset HEAD CONTRIBUTING.md
```

**还原已经修改过的文件**

前提不在暂存区中

`git checkout -- CONTRIBUTING.md`

## 远程仓库

origin - 这是 Git 给你克隆的仓库服务器的默认名字。

查看远程仓库

`git remote -v`

查看某个远程仓库

`git remote show [remote-name]`

添加远程仓库

`git remote add remmote-name http://gitlab.jkl/xyz/abc.git`

remote-name可以自定义

拉取远程仓库

`git fetch remmote-name`

同步代码

`git merge remmote-name/master`

推送到远程仓库

`git push [remote-name] [branch-name]`

*将 master 分支推送到 origin 服务器*

`git push origin master`

其它

```
//重命名
git remote rename pb paul
//移除
git remote rm paul
```

## 分支操作

创建分支

`git branch testing`

切换当前工作分支

```
git checkout testing
git checkout master
```

创建分支并直接切换

```
git checkout -b iss53
//相当于如下2条命令
$ git branch iss53
$ git checkout iss53
```

合并分支到master
```
git checkout master
git merge iss53
```

删除分支

`git branch -d hotfix`



## 查看历史

```
git log --oneline --decorate --graph --all
```

**查看最新一次的简略历史**

`git log -n 1 --stat`

**查看最新一次提交的文件差异**

`git log -p -2`

