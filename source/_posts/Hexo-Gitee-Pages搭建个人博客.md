---
title: Hexo-Gitee-Pages搭建个人博客
date: 2020-07-07 15:31:55
tags:
- Hexo
categories: 
- 工作笔记
- Hexo
---
### 一、环境配置
node.js  {% link 官网 https://nodejs.org/zh-cn/ %}
Git   {% link 官网 https://git-scm.com/ %}

### 二、Hexo的安装与基本命令
#### 安装hexo
如果没有安装hexo的，只需要在目录中单击右键启动Git Bash Here，输入命令：
```
npm install -g hexo 
```
#### 初始化在本地生成Hexo相关目录
```
hexo init Note  # 初始化创建，会再桌面创建Note文件夹
cd Note         # 进入Note目录
npm install     # 进一步安装hexo所需文件
```
#### Hexo三连
```
hexo clean(or c)          # 清空已有hexo网站文件
hexo generate(or g)   # 依据网页文本与新的CSS样式生成新网站文件
hexo server(or s)     # 启动本地服务器，可以在localhost:4000查看网站修改效果
```
### 配置Git个人信息
Git 全局设置:
```
git config --global user.name "Github用户名"       //自己Github的账号名
git config --global user.email "Github邮箱"        //自己注册Github的邮箱地址
```
创建 git 仓库:
```
mkdir test
cd test
git init
touch README.md
git add README.md
git commit -m "first commit"
git remote add origin git@gitee.com:AAAA/AAAA.git
git push -u origin master
```
已有仓库?
```
cd existing_git_repo
git remote add origin git@gitee.com:AAAA/AAAA.git
git push -u origin master
```
### 三、主题下载与安装

Hexo官网上提供了丰富的主题可选，你只需要打开对应的界面（<a href="https://hexo.io/themes/" rel="nofollow noreferrer" target="_blank">https://hexo.io/themes/</a>）选择喜欢的，然后点击<strong>名称</strong>跳转到<strong>GitHub</strong>仓库选择<em>下载或者克隆</em>对应的<strong>zip</strong>文件到本地，并且解压到网站目录下的<strong>themes</strong>目录即可。

然后接下来，你需要修改两个配置文件：
<li>你的网站根目录下的<strong>_config.yml</strong>文件，即网站配置文件；</li>
<li>你选择的主题的自带配置文件<strong>_config.yml</strong>，即主题样式配置文件；</li>

#### 生成/添加 SSH 公钥之后，测试是否连接成功:
```
ssh -T git@gitee.com

如果成功，会显示：
Hi xxx! You've successfully authenticated, but GITEE.COM does not provide shell access.

```

#### 图片路径设置

![图片路径设置](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-Gitee-Pages%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/images-set.png)