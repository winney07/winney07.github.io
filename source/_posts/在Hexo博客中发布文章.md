---
title: 在Hexo博客中发布文章
date: 2018-08-02 11:34:29
tags:
- Hexo
categories: 
- 工作笔记
- Hexo
---
#### 1、新建一篇文章
（1）在hexo博客目录下，进入Git Bash命令窗口中，输入以下命令：
```bash
hexo new "在这里"
```
（2）在博客目录下的/source/_posts/ 文件夹下，可以看到已经生成了标题为(在这里.md)的博客文件：
如图所示：
{% asset_img zai.png %}
（3）在（在这里.md）文件中编辑自己的博客文章即可。
注意：Hexo 发布的文章是 Markdown 格式的文件， Markdown 基本语法的网址：{% link 点这里前往  http://www.markdown.cn/ %} 
<!--more-->
#### 2、给文章添加分类和标签
(1) 在（在这里.md）文件中设置tags和categories属性：
```bash
title: 在这里
date: 2018-08-02 11:41:10
tags:
- 博客           //多个标签可以这样添加
- hexo
categories: web前端
```
如图所示：
{% asset_img zai-edit.png %}
#### 3、启动服务器，本地测试
```bash
hexo s
```
如图所示：
{% asset_img zai-page.png %}
#### 4、添加“阅读全文”按钮
方法一：在文章任意你想添加的位置添加<!--more-->即可
```bash
<!--more-->        
```
例如：
在这里.md里面的内容是：
```bash
---
title: 在这里
date: 2018-08-02 11:41:10
tags:
- 博客
- hexo
categories: web前端
---
javascript是一门充满活力、简单易用的语言，又是一门具有许多复杂微妙技术的语言。即使是经验丰富的javascript开发者，如果没有认真学习的话，也无法真正理解它们，这就是javascript的矛盾之处。由于javascript不必理解就可以使用，因此通常来说很难真正理解语言本身，这就是我们面临的挑战。不满足于只是让代码正常工作，而是想要弄清楚为什么，勇于挑战这条崎岖颠簸的少有人走的路，拥抱整个javascript
<!--more-->
后面的内容在首页不显示，只显示到<!--more-->这里
```
在页面中显示的效果是：
{% asset_img zai-more.png %}
方法二：设置首页文章以摘要形式显示，打开主题配置文件，找到auto_excerpt进行修改：
```bash
auto_excerpt:
  enable: true
  length: 150
```
其中length代表显示摘要的截取字符长度。
注：这两种方法，在博客首页显示的效果不一样，根据自己的需要，选择自己喜欢的方法
#### 5、在博文中添加图片
方法一：
(1)在hexo目录下，安装插件：
```bash
npm install hexo-asset-image --save
```
(2)在hexo\source 目录下新建一个img文件夹，把图片放置在里面；
(3)在xxx.md文件中引用图片：
```bash
![header]( img/header.jpg)
```
方法二：
(1)在全局配置文件（hexo/_config.yml)中将post_asset_folder设置为true；
(2)创建文章（在创建的时候，会在hexo/source/_post目录下，生成一个XXX.md文件和一个XXX的文件夹）：
```bash
hexo new "XXX"
```
(3)把XXX这个博文需要展示的图片放在XXX文件夹目录下；
(4)在XXX.md文件中引入图片的方式：
```bash
{% asset_img example.jpg This is an example image %}
```
#### 6、发布到Github上
（1）发表的文章在本地预览无误后，在 Git Bash 命令窗口执行以下命令：
```bash
hexo clean && hexo g && hexo d
```
（2）在浏览器，访问自己的博客域名，即可看到刚 发布的文章