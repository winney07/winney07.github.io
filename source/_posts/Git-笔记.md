---
title: Git-笔记
date: 2021-01-14 14:47:55
tags:
- Git
categories: 
- 工作笔记
- Git
---

正确的github工作流

#### 提交到远程仓库报错

```
OpenSSL SSL_connect: Connection was reset in connection to github.com:443
 
 或
 
OpenSSL SSL_connect: Connection was reset in connection to github.com:403
```

解决方法，将.git/config：

```
[remote "origin"]
	url = https://github.com/winney07/winney07.github.io.git
```

改为：

```
[remote "origin"]
	url = git@github.com:winney07/winney07.github.io.git
```



#### Github创建仓库

![Github创建仓库](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Git-%E7%AC%94%E8%AE%B0/create.png)

### Git常用命令速查表

#### 创建版本库

1. 克隆远程版本库

   ```
   git clone <url>
   ```

2. 初始化本地版本库

   ```
   git init
   ```

#### 修改和提交

1. 查看状态

   ```
   git status
   ```

2. 查看变更内容

   ```
   git diff
   ```

3. 跟踪所有改动过的文件

   ```
   git add .
   ```

4. 跟踪指定的文件

   ```
   git add <file>
   ```

5. 文件改名

   ```
   git mv <old> <new>
   ```

6. 删除文件

   ```
   git rm <file>
   ```

7. 停止跟踪文件但不删除

   ```
   git rm --cached <file>
   ```

8. 提交所有更新过的文件

   ```
   git commit -m "commit message"
   ```

9. 修改最后一次提交

   ```
   git commit --amend
   ```



#### 查看提交历史

1. 查看提交历史

   ```
   git log
   ```

2. 查看指定文件的提交历史

   ```
   git log -p <file>
   ```

3. 以列表方式查看指定文件的提交历史

   ```
   git blame <file>
   ```



#### 撤销

1. 撤销工作目录中所有未提交文件的修改内容

   ```
   git reset --hard HEAD
   ```

2. 撤销指定的未提交文件的修改内容

   ```
   git checkout HEAD <file>
   ```

3. 撤销指定的提交

   ```
   git revert <commit>
   ```



#### 分支与标签

1. 显示所有本地分支

   ```
   git branch
   ```

2. 切换到指定分支或标签

   ```
   git checkout <branch/tag>
   ```

3. 创建新分支

   ```
   git branch <new-branch>
   ```

4. 删除本地分支

   ```
   git branch -d <branch>
   ```

5. 列出所有本地标签

   ```
   git tag
   ```

6. 给予最新提交创建标签

   ```
   git tag <tagname>
   ```

7. 删除标签

   ```
   git tag -d <tagname>
   ```



#### 合并与衍合

1. 合并指定分支到当前分支

   ```
   git merge <branch>
   ```

2. 衍合指定分支到当前分支

   ```
   git rebase <branch>
   ```



#### 远程操作

1. 查看远程版本库信息

   ```
   git remote -v
   ```

   

2. 查看指定远程版本库信息

   ```
   git remote show <remote>
   ```

   

3. 添加远程版本库

   ```
   git remote add <remote> <url>
   ```

   

4. 从远程库获取代码

   ```
   git fetch <remote>
   ```

   

5. 下载代码及快速合并

   ```
   git pull <remote> <branch>
   ```

   

6. 上传代码及快速合并

   ```
   git push <remote> <branch>
   ```

   

7. 删除远程分支或标签

   ```
   git pull <remote> : <branch/tag-name>
   ```

   

8. 上传所有标签

   ```
   git push --tags
   ```

   

### 管理分支

#### 1、查看本地分支

使用 git branch命令，如下：

```ruby
$ git branch
* master
```

***标识的是你当前所在的分支。**

#### 2、查看远程分支

命令如下：

```undefined
git branch -r
```

#### 3、查看所有分支

命令如下：

```undefined
git branch -a
```

#### 2、本地创建新的分支

命令如下：

```css
git branch [branch name]
```

例如：

```undefined
git branch save
```

#### 3、切换到新的分支

命令如下：

```css
git checkout [branch name]
```

例如：

```ruby
$ git checkout save
```

#### 4、创建+切换分支

创建分支的同时切换到该分支上，命令如下：

```css
git checkout -b [branch name]
```

git checkout -b [branch name] 的效果相当于以下两步操作：

```css
git branch [branch name]
git checkout [branch name]
```

#### 5、将新分支推送到github

命令如下：

```css
git push origin [branch name]
```

例如：

```undefined
git push origin save
```

#### 6、删除本地分支

命令如下：

```css
git branch -d [branch name]
```

例如：

```undefined
git branch -d save
```

#### 7、删除github远程分支

命令如下：

```css
git push origin :[branch name]
```

分支名前的冒号代表删除。
 例如：

git push origin :save



#### 查看配置信息

```
git config --list
```

#### 查看状态

```
git status
```

#### 提交工作区文件到暂存区

1. 提交工作区中所有文件到暂存区

   ```
   git add .
   ```

2. 提交工作区中指定文件到暂存区

   ```
   git add <file1> <file2> 
   ```

3. 提交工作区中某个文件夹中所有文件到暂存区

   ```
   git add [dir]
   ```

#### 提交到本地仓库

1. 将暂存区中的文件提交到本地仓库中，即打上新版本

   ```
   git commit -m "commit_info"
   ```

2. 将所有已经使用git管理过的文件暂存后一并提交，跳过add到暂存区的过程

   ```
   git commit -a -m “commit_info”
   ```

3. 提交文件时，发现漏掉几个文件，或者注释写错了，可以撤销上一次提交

   ```
   git commit --amend
   ```

#### 查看本地仓库关联的远程仓库

1. 查看本地仓库关联的远程仓库

   ```
   git remote
   ```

2. 查看远程仓库的url地址

   ```
   git remote -v
   ```

   

#### 解决git pull后本地写的代码没了的问题

第一步：git reflog

第二步：git reset --hard HEAD@{n}   (HEAD:为版本号，就前面那一串数字，n是你要回退到的引用位置)

```
git reset --hard 84ef223
```

#### 创建分支，回退到某个版本

```
git branch pagination 96ba9b3
git branch 分支名称 版本号
```

> 如果为了测试原来的代码，将它回退到某个版本，但是为了不影响当前分支里面的内容，创建一个新的分支。  如果git branch 分支名称，不加版本号，会在当前版本下创建分支。   如果需要回退到某个版本，需要在创建分支的时候加上版本号。

如果要切换回原来的分支(master)，要先对新创建的分支(pagination)的内容提交，这个提交只会提交到pagination分支里面，不会影响到master分支

提交：

```
git add .
git commit -m "复习"
```

切换：

```
git checkout master
```

#### [解决pre -commit hook failed (add --no-verify)的问题](https://www.jianshu.com/p/aac394600727)

```
cd .git

rm hooks/pre-commit
```



git commit 不单保存了当前的版本号还保存了他的父版本号



#### 查看命令：

```
git / git help
```

#### 查看所有命令：

```
git help -a
```

#### 查看使用手册：

```
git help -g
```

#### 查看某个命令的详细使用：

如：

```
git help add
```

按Q可以退出

`.git`是做版本控制的，如果想去除，直接删了这个目录。

是隐藏文件，在mac 用`open .git`打开（在.git的上层目录）



Git基本工作流程

Git初始化及仓库创建和操作

Git管理远程仓库

Github Pages搭建网站

