---
title: VScode相关笔记
date: 2020-08-22 11:12:23
tags:
- VScode
categories: 
- VScode
---

[常用快捷键](https://lzw.me/a/vscode-visual-studio-code-shortcut.html) [大牛在用](https://www.awesomes.cn/)

#### 格式化代码

```
Shift + Alt + F
```

代码缩进

选中代码段之后

1、向左

```
shift + TAB 
```

2、向右：

```
TAB
```

#### 更换主题

```
Ctrl + K + T
```

#### `VSCode`搜索指定某个目录下查找文件

1. 先点击选中这个要查找的目录。
2. 右键点击后，点击里面的「Find in Folder」即 在文件夹中查找…..

[将VSCode设置成中文语言环境](https://jingyan.baidu.com/article/7e44095377c9d12fc1e2ef5b.html)

##### 快速在浏览器中打开

1. 安装open in browser插件
2. 重新启动`VSCode`
3. 快捷键：Alt + B

##### 使用sublime快捷键

安装插件：Sublime Text Keymap and Settings Importer

##### 自动换行

https://jingyan.baidu.com/article/6f2f55a14ba6e3b5b93e6cd6.html

https://jingyan.baidu.com/article/6dad5075383c3fa123e36ec3.html

##### `VSCode`编辑器字体大小设置

“settings”——“文本编辑器”——常用设置——`Editor：Font Size`（这里设置为20）

#### `VSCode`如何用浏览器预览运行html文件

在”扩展“中搜索”view in browser“——右键点击html文件，选择View In Browser

`view in browser`已废弃， 换成”open in browser”

#### VSCode 编写Vue项目安装Vetur插件实现 代码高亮

#### VSCode中配置Vue3 + TS 的用户代码片段

设置——配置用户代码片段——新建代码片段——代码片段文件名（输入该快捷键生成代码片段–例如：vue3）

输入以下内容：

```
{
	"vue-template": {
		"prefix": "vue3",
		"body": [
		"<template>",
		"",
		"</template>",
		"",
		"<script setup lang='ts'>",
		"",
		"</script>",
		"",
		"<style lang='less' scoped>",
		"",
		"</style>",
		],
		"description": "my vue3 template"
	}
}
```

##### 使用方法：

在新建的.vue文件中，输入’vue3‘，即可快速生成以下代码：

```
<template>

</template>

<script setup lang='ts'>

</script>

<style lang='less' scoped>

</style>
```

### 插件

- open in browser：在默认浏览器打开
- CodeGeeX

- Vetur插件


### AI自动代码补全插件

#### Tabnine

[tabnine官网](https://www.tabnine.com/)

[Tabnine AI Autocomplete](https://marketplace.visualstudio.com/items?itemName=TabNine.tabnine-vscode)

[TabNine-GitHub](https://github.com/codota/TabNine)

## WebStorm10

WebStorm是最专业的前端IDE开发工具

WebStorm配置和快捷键

## Atom_工具使用

由github发布的前端开发工具

非常强大和非常开发的开发工具平台

- 官网地址: https://atom.io/
- 百度网盘下载地址：http://pan.baidu.com/s/1ntszCgT

Atom的插件和主题安装和配置
