---
title: 在Github上使用仓库存放.md笔记
date: 2020-07-08 11:59:41
tags:
- md笔记
categories: 
- 工作笔记
- md笔记
---
### 一、在GitHub上创建一个仓库，例如：GaoShu

### 二、在本地新建一个存放.md笔记的文件夹GaoShu

### 三、执行git命令
**…or create a new repository on the command line**
```
echo "# GaoShu" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/AAAAAA/GaoShu.git
git push -u origin master
```
**…or push an existing repository from the command line**
```
git remote add origin https://github.com/AAAAAA/GaoShu.git
git push -u origin master
```