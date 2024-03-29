---
title: 将Hexo博客主题更换为NexT主题
date: 2018-08-01 17:10:28
tags:
- Hexo
- Git
categories: 
- Git
---

1、[下载NexT主题]( https://gitforwindows.org/)，下载解压后，将该文件夹命名为next，把这个文件夹放置到博客目录的themes 文件夹下，如图所示：
![将主题的文件夹命名为next](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%B0%86Hexo%E5%8D%9A%E5%AE%A2%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%8D%A2%E4%B8%BANexT%E4%B8%BB%E9%A2%98/next.png)
想了解更多，可以查看NexT 主题使用文档： [官方使用文档 ](http://theme-next.iissnan.com/ ) 

2、修改主配置文件_`config.yml`（`hexo`目录下的`_config.yml`文件)，将`theme`属性修改为`next`，如下所示：

```bash
# Extensions 扩展
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next
```
3、在博客目录，右键点击`Git Bash`，进入命令窗口，输入下面的命令，本地预览博客，如果发现`Hexo`博客的主题已经变成了`NexT`主题，说明你已经成功更换主题了

```bash
hexo server
```
4、打开主题配置文件 `_config.yml`
如图所示：
![打开主题配置文件 _config.yml](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%B0%86Hexo%E5%8D%9A%E5%AE%A2%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%8D%A2%E4%B8%BANexT%E4%B8%BB%E9%A2%98/next-config.png)
5、在主题配置文件 `_config.yml`中将`scheme`设置为 `Pisces`（`Hexo`默认样式是`Muse`，根据你自己的喜好选择你想要设置的样式，这里以`Pisces`为例)

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
6、在主题配置文件 `_config.yml`中配置博客网站底部的基本信息：

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
 7、在主题配置文件 `_config.yml`中配置菜单按钮，找到`menu`属性，做以下配置：
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
（1）执行命令`hexo s`，本地预览我们的博客页面，会发现，点击分类、标签、关于这几个页面的时候，会显示`404`。
（2）在`Git Bash`命令窗口，输入以下命令来创建相应页面：

```bash
hexo new page 'categories'
hexo new page 'tags'
hexo new page 'about'
```
（3）可以在`hexo/source`目录下看到创建的3个文件夹
如图所示：
![在hexo/source目录下看到创建的3个文件夹](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%B0%86Hexo%E5%8D%9A%E5%AE%A2%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%8D%A2%E4%B8%BANexT%E4%B8%BB%E9%A2%98/source.png)
9、每一个分类菜单都生成了一个 `index.md` 初始文件（在刚创建的文件夹目录下)，默认包含了 `title` 和 `date` 字段，我们需要给每一 `index.md` 文件添加上 `type` 字段
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
（1）安装 `hexo-generator-searchdb` ，在 `Git Bash` 命令窗口，输入以下命令：

```bash
npm install hexo-generator-searchdb --save
```
（2）打开全局配置文件`（hexo/_config.yml）`，新增以下代码：
```bash
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```
（3）打开主题配置文件`（hexo/themes/next/_config.yml）`，找到 `local_search` 属性，开启本地搜索功能：
```bash
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```
11、执行命令`hexo s`，本地预览我们的博客页面，发现刚才的配置已经完成
如图所示：
![预览本地博客页面](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/%E5%B0%86Hexo%E5%8D%9A%E5%AE%A2%E4%B8%BB%E9%A2%98%E6%9B%B4%E6%8D%A2%E4%B8%BANexT%E4%B8%BB%E9%A2%98/winney-blog.png)
12、在命令窗口，输入以下命令，将修改后的本地`hexo`项目托管到`GitHub`上

```bash
hexo clean && hexo g && hexo d
```
13、上传成功后，可以通过自己的博客域名访问修改主题和修改相关配置后的博客页面