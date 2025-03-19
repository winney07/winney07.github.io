---
title: 腾讯云服务器中使用nvm管理Node.js版本
date: 2025-03-19 22:30:54
tags:
- 云服务器
categories: 
- 云服务器
---

##### 使用`node -v`在腾讯云服务器查看Node.js版本时，报：

```
node: /lib64/libm.so.6: version `GLIBC_2.27' not found (required by node)
node: /lib64/libc.so.6: version `GLIBC_2.25' not found (required by node)
node: /lib64/libc.so.6: version `GLIBC_2.28' not found (required by node)
node: /lib64/libstdc++.so.6: version `CXXABI_1.3.9' not found (required by node)
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.20' not found (required by node)
node: /lib64/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by node)
```

### 问题分析

1. **GLIBC 版本过旧**：系统目前的 `GLIBC` 版本太低，不支持 Node.js 需要的 `GLIBC_2.27` 及以上版本
2. **libstdc++ 版本不匹配**：Node.js 也需要 `libstdc++` 提供的 **C++ ABI 兼容性**，但服务器上 `libstdc++` 版本较低

### 解决方案：

⚠️注意：我不想升级系统的 `GLIBC`，使用 **nvm（Node Version Manager）** 来安装适配的 Node.js 版本：

```
curl -fsSL https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
nvm install 16
```

##### 切换到 Node.js 16：

```
nvm use 16
```

##### 再检查

```
node -v
```

##### 返回版本啦

```
v16.13.0
```

##### 如果希望每次登录服务器都自动使用 Node.js 16，可以运行：

```
nvm alias default 16
```

##### 返回：

```
default -> 16 (-> v16.13.0)
```

这样以后登录服务器时，`nvm` 会默认使用 Node.js 16。
