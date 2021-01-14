---
title: git管理分支
date: 2021-01-14 14:47:55
tags:
- Git
categories: 
- 工作笔记
- Git
---

# 管理分支

## 1、查看分支

### 1、查看本地分支

使用 git branch命令，如下：

```ruby
$ git branch
* master
```

***标识的是你当前所在的分支。**

### 2、查看远程分支

命令如下：

```undefined
git branch -r
```

### 3、查看所有分支

命令如下：

```undefined
git branch -a
```

## 2、本地创建新的分支

命令如下：

```css
git branch [branch name]
```

例如：

```undefined
git branch save
```

## 3、切换到新的分支

命令如下：

```css
git checkout [branch name]
```

例如：

```ruby
$ git checkout save
```

## 4、创建+切换分支

创建分支的同时切换到该分支上，命令如下：

```css
git checkout -b [branch name]
```

git checkout -b [branch name] 的效果相当于以下两步操作：

```css
git branch [branch name]
git checkout [branch name]
```

## 5、将新分支推送到github

命令如下：

```css
git push origin [branch name]
```

例如：

```undefined
git push origin save
```

## 6、删除本地分支

命令如下：

```css
git branch -d [branch name]
```

例如：

```undefined
git branch -d save
```

## 7、删除github远程分支

命令如下：

```css
git push origin :[branch name]
```

分支名前的冒号代表删除。
 例如：

git push origin :save

