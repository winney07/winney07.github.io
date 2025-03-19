---
title: 删除 GitHub 仓库中本该ignore的.DS_Store 文件
date: 2025-03-19 14:51:45
tags:
- Git
categories: 
- Git
---

> 前提：在提交文件到GitHub上之前，忘了加上.gitignore文件，把.DS_Store文件提交到github上面了

> 说明：.DS_Store 是 macOS 系统生成的文件，用于存储文件夹的元数据（如图标位置等），通常不需要提交到 Git 仓库

## 删除 GitHub 仓库中已经提交的 `.DS_Store` 文件

⚠️ 注意：终端命令行操作路径是当前项目目录

##### **步骤 1：创建 `.gitignore` 文件（如果没有的话）**

在项目根目录下创建一个 `.gitignore` 文件，并添加以下内容：

```
# 忽略 .DS_Store 文件
.DS_Store
```

##### **步骤 2：删除已经提交的 `.DS_Store` 文件**

#####  删除所有 `.DS_Store` 文件
 运行以下命令递归删除项目中的 `.DS_Store` 文件：

```
find . -name ".DS_Store" -delete
```

##### **步骤 3：从 Git 仓库中移除 `.DS_Store` 文件**

即使你删除了 `.DS_Store` 文件，这些文件仍然存在于 Git 的历史记录中。执行以下命令将它们从 Git 记录中删除：

```
git rm --cached -r .
```

##### **步骤 4：重新添加文件到 Git**

在 `.gitignore` 文件生效后，重新添加文件：

```
git add .
```

##### **步骤 5：提交更改**

提交此次删除 `.DS_Store` 文件的更改：

```
git commit -m "Remove .DS_Store files and update .gitignore"
```

##### **步骤 6：推送到 GitHub**

将更改推送到远程仓库：

```
git push origin main
```

⚠️ 注意：`main` 是默认分支名，如果你的分支名是 `master` 或其他分支名，请替换 `main`。

#### **完成！**

现在 `.DS_Store` 文件已经从 GitHub 仓库中删除，并且 `.gitignore` 会阻止它们再次被提交！
