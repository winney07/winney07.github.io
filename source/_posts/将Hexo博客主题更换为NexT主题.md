---
title: 将Hexo博客主题更换为NexT主题
date: 2018-08-01 17:10:28
tags:
- Hexo
categories: 
- 工作笔记
- Hexo
---
1、{% link 下载NexT主题  https://gitforwindows.org/ %}，下载解压后，将该文件夹命名为next，把这个文件夹放置到博客目录的themes 文件夹下，如图所示：
{% asset_img next.png %}
想了解更多，可以查看NexT 主题使用文档： {% link 官方使用文档  http://theme-next.iissnan.com/ %}
<!--more-->
2、修改主配置文件_config.yml（hexo目录下的_config.yml文件），将theme属性修改为next，如下所示：
```bash
# Extensions 扩展
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```
3、在博客目录，右键点击Git Bash，进入命令窗口，输入下面的命令，本地预览博客，如果发现Hexo博客的主题已经变成了NexT主题，说明你已经成功更换主题了
```bash
hexo server
```
4、打开主题配置文件 _config.yml
如图所示：
{% asset_img next-config.png %}
5、在主题配置文件 _config.yml中将scheme设置为 Pisces（Hexo默认样式是Muse，根据你自己的喜好选择你想要设置的样式，这里以Pisces为例）
```bash
# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
# scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
```
6、在主题配置文件 _config.yml中配置博客网站底部的基本信息：
```bash
footer:
  # Specify the date when the site was setup.
  # If not defined, current year will be used.
  since: 2018      #网站起始运营年份

  # Icon between year and copyright info.
  icon: user     #声明图标

  # If not defined, will be used `author` from Hexo main config.
  copyright: winney07   #版权所有
  # -------------------------------------------------------------
  # Hexo link (Powered by Hexo).
  powered: true

  theme:
    # Theme & scheme info link (Theme - NexT.scheme).
    enable: false    #是否显示主题
    # Version info of NexT after scheme info (vX.X.X).
    version: false     #是否显示驱动
 ```
 7、在主题配置文件 _config.yml中配置菜单按钮，找到menu属性，做以下配置：
 ```bash
 menu:
  home: / || home     #首页，后面的表示图标
  categories: /categories/ || th   #分类
  tags: /tags/ || tags       #标签
  archives: /archives/ || archive     #归档
  about: /about/ || user       #关于
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
  ```
8、创建相应的页面
（1）执行命令hexo s，本地预览我们的博客页面，会发现，点击分类、标签、关于这几个页面的时候，会显示404。
（2）在Git Bash命令窗口，输入以下命令来创建相应页面：
```bash
hexo new page 'categories'
hexo new page 'tags'
hexo new page 'about'
```
（3）可以在hexo/source目录下看到创建的3个文件夹
如图所示：
{% asset_img source.png %}
9、每一个分类菜单都生成了一个 index.md 初始文件（在刚创建的文件夹目录下），默认包含了 title 和 date 字段，我们需要给每一 index.md 文件添加上 type 字段
如下所示：
```bash
---
title: categories
date: 2018-07-30 16:28:33
type: categories
---
```
```bash
---
title: tags
date: 2018-07-30 16:28:54
type: tags
---
```
```bash
---
title: about
date: 2018-07-30 16:29:13
type: about
---
```
10、配置搜索菜单：
（1）安装 hexo-generator-searchdb ，在 Git Bash 命令窗口，输入以下命令：
```bash
npm install hexo-generator-searchdb --save
```
（2）打开全局配置文件（hexo/_config.yml），新增以下代码：
```bash
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
（3）打开主题配置文件（hexo/themes/next/_config.yml），找到 local_search 属性，开启本地搜索功能：
```bash
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```
11、执行命令hexo s，本地预览我们的博客页面，发现刚才的配置已经完成
如图所示：
{% asset_img winney-blog.png %}
12、在命令窗口，输入以下命令，将修改后的本地hexo项目托管到GitHub上
```bash
hexo clean && hexo g && hexo d
```
13、上传成功后，可以通过自己的博客域名访问修改主题和修改相关配置后的博客页面