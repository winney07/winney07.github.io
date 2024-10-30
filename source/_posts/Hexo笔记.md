---
title: Hexo笔记
date: 2018-03-07 14:43:47
tags:
- Hexo
categories: 
- Hexo
---

#### 本地预览：

```
hexo s
```

当默认端口4000被占用时：

```
FATAL Port 4000 has been used. Try other port instead.
```

#### 解决默认端口4000被占用：

1. 直接在终端命令行中指定端口

   ```
   hexo server -p 4002
   ```

2. 修改项目运行所在端口号

   > 修改`package.json`文件里的server,修改前: `"server": "hexo server"` 修改后: `"server": "hexo server -p 4001"` 注意:这时候你需.

   ```
   npm run server
   ```

   

