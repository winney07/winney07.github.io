---
title: Git常用命令
date: 2020-03-22 10:12:23
tags:
- Git
categories: 
- Git
---

### 将目录的内容提交到`Github`的私有仓库中

1. 在服务器的目录中，确保已经初始化了 Git 仓库，执行了 `git init` 命令

2. 配置 `Git` 用户信息，使用以下命令替换 `<YOUR_NAME>` 和 `<YOUR_EMAIL>` 为您的 `GitHub` 用户名和邮箱地址：

   ```
   git config --global user.name "<YOUR_NAME>"
   git config --global user.email "<YOUR_EMAIL>"
   ```

3. 添加要提交的文件到暂存区。如果您要提交整个目录的内容，可以使用 `.` 来表示当前目录：

   ```
   git add .
   ```

4. 提交更改到本地仓库，并添加提交信息：

   ```
   git commit -m "Your commit message"
   ```

5. 在 `GitHub` 上创建一个私有仓库，并将其作为远程仓库添加到您的本地仓库。执行以下命令，将 `<YOUR_GITHUB_REPO_URL>` 替换为您的 `GitHub` 私有仓库的 URL：

   ```
   git remote add origin <YOUR_GITHUB_REPO_URL>
   ```

6. 推送本地提交到 `GitHub` 私有仓库。执行以下命令：

   ```
   git push -u origin master
   ```

   > 如果您的默认分支不是 `master`，请将 `master` 替换为您的默认分支名称。

### git切换分支

1. 列出所有可用的分支：

   ```
   git branch
   ```

2. 切换到已存在的分支：

   ```
   git checkout <branch_name>
   ```

3. 创建并切换到新分支：

   ```
   git checkout -b <new_branch_name>
   ```

4. 强制切换分支（丢弃当前分支的更改）：

   ```
   git checkout -f <branch_name>
   ```

5. 切换到远程分支：

   ```
   git checkout <remote_name>/<branch_name>
   ```

### 更改分支的名称

将 `master` 分支的名称更改为 `wordpress`

1. 确保您当前不在要更改名称的分支上。如果当前在 `master` 分支上，请先切换到其他分支：

   ```
   git checkout <other_branch>
   ```

2. 更改分支的名称：

   ```
   git branch -m master wordpress
   ```

3. 将远程仓库中的分支名称也更新为新的名称：

   ```
   git push origin :master wordpress
   git push origin -u wordpress
   ```

### 删除分支

1. 删除本地分支：

   ```
   git branch -d <branch_name>
   ```

   > 注意，如果分支还有未合并的更改，使用 `-d` 选项会提示您进行确认。如果要强制删除分支，无论是否合并，可以使用 `-D` 选项。

2. 删除远程分支：

   ```
   git push origin --delete <branch_name>
   ```

   

### 克隆远程仓库并指定某个分支

```
git clone -b <branch_name> <remote_repository_url>
```

### 云服务器拉取代码

在云服务器上拉取从本地提交到 Git 远程仓库的 `WordPress` 分支的代码

1. 首先，进入您的 `WordPress` 项目所在的目录：

   ```
   cd /path/to/wordpress
   ```

   > 将 `/path/to/wordpress` 替换为您 `WordPress` 项目的实际路径。

2. 确保您已经将远程仓库添加为 Git 的远程仓库。如果尚未添加，请执行以下命令：

   ```
   git remote add origin <remote_repository_url>
   ```

   > 将 `<remote_repository_url>` 替换为您的远程仓库的 URL。

3. 切换到目标分支（即 `WordPress` 分支）：

   ```
   git checkout wordpress
   ```

   这将切换到名为 `wordpress` 的分支，确保您使用正确的分支名称。

4. 拉取最新的代码：

   ```
   git pull origin wordpress
   ```

   

### 本地仓库重新关联到远程新仓库

1. 查看当前本地仓库关联的远程仓库：

   ```
   git remote -v
   ```
	这将显示当前本地仓库关联的远程仓库信息，包括远程仓库的名称（通常是 `origin`）和对应的 URL。
2. 移除当前关联的远程仓库：

   ```
   git remote remove origin
   ```
	这将移除本地仓库当前关联的远程仓库（假设当前远程仓库的名称是 `origin`）
3. 添加新的远程仓库地址：

   ```
   git remote add origin 新的远程仓库URL
   ```

4. 验证新的远程仓库是否关联成功：

   ```
   git remote -v
   ```
	现在，您的本地仓库已经重新关联到新的远程仓库。在将代码推送到远程仓库时，可以使用 `git push` 命令，例如：
5. 将代码推送到远程仓库：

   ```
   git push -u origin master
   ```
	其中，`origin` 是新远程仓库的名称，`master` 是要推送的分支名。
   
   
   
   请注意，如果您之前的本地分支与远程仓库有相关联，新关联的远程仓库可能不会自动与这些分支关联。如果需要将旧的本地分支与新的远程仓库关联，您可以使用 git branch --set-upstream-to 命令。例如：
   
   ```
   git branch --set-upstream-to=origin/master master
   ```
   
   这将把本地 `master` 分支与新的远程仓库的 `master` 分支关联起来。
   
   `请确保在进行这些操作之前备份您的本地仓库，以防意外情况。`

