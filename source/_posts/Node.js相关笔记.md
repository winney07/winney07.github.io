---
title: Node.js相关笔记
date: 2020-08-22 11:12:23
tags:
- node.js
categories: 
- node.js
---

[认识 Node.js | Node.js学习指南 (poetries.top)](https://blog.poetries.top/node-learning-notes/notes/base/01-环境搭建.html#环境搭建)

## 认识 Node.js

- Node 是一个服务器端 JavaScript 解释器
- Node.js 是一个基于 Chrome V8 引擎的 JavaScript 运行环境
- Node.js 使用了一个事件驱动、非阻塞式 I/O 的模型，使其轻量又高效
- Node.js 的包管理器 npm，是全球最大的开源库生态系统
- Node.js 是一门动态语言，运行在服务端的 Javascript

### NVM

> Node.js Version Manager（简称 NVM）是一个用于管理 Node.js 版本的命令行工具。Node.js 是一个流行的服务器端 JavaScript 运行时环境，用于构建 Web 应用程序和服务。NVM 允许您在同一台计算机上安装多个 Node.js 版本，并轻松在它们之间切换，以确保您的应用程序与特定的 Node.js 版本兼容。

- `nvm install <version>`：安装指定版本的 Node.js。
- `nvm use <version>`：切换到指定版本的 Node.js。
- `nvm ls`：列出已安装的 Node.js 版本。
- `nvm alias <name> <version>`：创建 Node.js 版本别名。

#### 安装

使用git bash工具

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.25.2/install.sh | bash
```

`这些命令可以在 macOS 和 Linux 上使用。请注意，NVM 不支持 Windows，但您可以使用类似的工具，如 nvm-windows 或 nvmw。`

**nvm-windows 的安装和使用**:

1. 下载 `nvm-setup.zip` 安装文件。您可以在 [nvm-windows GitHub Releases 页面](https://github.com/coreybutler/nvm/releases) 下载最新版本的 `nvm-setup.zip`。

2. 解压缩 `nvm-setup.zip` 文件，并运行 `nvm-setup.exe` 安装程序。按照安装程序的指示进行安装。

3. 安装完成后，`打开一个新的命令提示符窗口（cmd.exe）或 PowerShell 窗口`。

4. 使用以下命令来查看所有可用的 Node.js 版本并安装其中一个：

   - 列出可用版本：

     ```
     bashCopy code
     nvm list available
     ```

   - 安装特定版本，例如 14.17.5：

     ```
     bashCopy code
     nvm install 14.17.5
     ```

5. 使用以下命令来选择已安装的 Node.js 版本：

   ```
   bashCopy code
   nvm use 14.17.5
   ```

   这将设置当前的 Node.js 版本为 14.17.5。

6. 验证 Node.js 版本是否正确切换：

   ```
   bashCopy code
   node -v
   ```

7. 您还可以使用其他 nvm-windows 命令来管理 Node.js 版本，如 `nvm list`、`nvm uninstall` 等。