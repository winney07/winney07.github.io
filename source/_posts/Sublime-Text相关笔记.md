---
title: Sublime Text相关笔记
date: 2019-08-24 16:36:46
tags:
- Sublime Text
categories:
- 代码编辑器
- Sublime Text
---



![img](https://raw.githubusercontent.com/winney07/Images/main/Note/Submit%20Text.jpg)

## Sublime3安装配置

Sublime跨平台的前端开发神器，共享软傺

下载最新Sublime3安装包

- 官网地址: http://www.sublimetext.com/

- 网盘地址: http://pan.baidu.com/s/1ntszCgT
- 安装包管理器

- - 打开Sublime3控制台，ctrl+~
  - 输入安装包管理器命令代码(见备注)
  - 注意需要联网才能安装，因为是在线下载包。
  - 包管理器的官网地址: https://packagecontrol.io

#### [Sublime Text 3 安装Package Control](https://www.cnblogs.com/luoshupeng/p/3310777.html)

#### 格式化代码

[SublimeText自带格式化代码功能 - reindent](https://www.douban.com/note/326071630/?type=like&_i=3394023-X_1kzR)

1、首先通过以下路径打开用户按键绑定文件：

```
Preferences → Key Bindings – User
```

2、然后在其中添加以下代码（如果你有需要的话，其中的快捷键组合是可以自己定义的）：

```
{"keys": ["ctrl+shift+r"], "command": "reindent" , "args":{"single_line": false}}
```

