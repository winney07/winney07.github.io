---
title: Hexo + GitHub Pages  搭建个人博客
date: 2018-08-01 11:01:02
tags:
- Hexo
categories: 
- 文档网站生成工具
- Hexo
---

## 一、准备工作
### 1. 安装Node.js 
1. 下载Node.js：[官网下载地址](https://nodejs.org/en/download/)（这里以Windows 为例）：
   ![下载Node.js](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/download.png)

2.  双击下载好的`.msi`文件，按下一步下一步，安装好就可以；

3. 在cmd命令窗口，输入下面的这个命令，如果能够显示Node.js的版本，说明安装成功了。

   ```
   node -v
   ```

   ![查看node版本](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/node-v.png)
### 2. 安装Git
1.  下载Git：[官网下载地址](https://gitforwindows.org/)（这里以Windows 为例，我是在这里下载的） 你也可以到[官网下载](https://git-scm.com/downloads )  ；

2. 双击下载好的Git安装包，按下一步下一步，进行安装即可；

3.  在cmd命令窗口，输入下面的这个命令，如果能够显示Git的版本，说明安装成功了。

   ```
   git -version
   ```

   ![查看git版本](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/git-v.png)

4.  想对Git有更多的了解，可以从下面几个网站学习，若你有更好的网站，也可以推荐给我：
   - [官网]( https://git-scm.com/book/zh/v2)
   - [W3Cschool](https://www.w3cschool.cn/git/)
   -  [廖雪峰网站教程]( https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

## 二、Hexo搭建博客
### 1. 安装Hexo
1. 在计算机中，新建一个`winneyBlog`文件夹，用于存放自己的博客内容。

2. 在`winneyBlog`文件夹内，鼠标右键，选择`Git Bash`,进入到命令窗口
   ![博客目录-进入命令窗口](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/blog-path.png)

3. 在命令窗口中，输入下面代码：

   ```
   npm install -g hexo-cli
   ```

   如图所示：
   ![安装hexo-cli](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/hexo-cli.png)

### 2. 初始化Hexo 
1. 在命令窗口中，输入下面代码：(会在`winneyBlog`目录下，新建了一个`hexo`文件夹)

   ```
   hexo init hexo
   ```

   如图所示：
   ![初始化hexo](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/hexo-init.png)

### 3. 配置Hexo
1. 进入hexo文件夹

   ```
   cd hexo
   ```

2. 安装依赖

   ```
   npm install
   ```

3. 部署形成的文件

   ```
   hexo generate
   ```

   如图所示：
   ![部署形成的文件](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/hexo-gen.png)

### 4. 启动服务器
1. 在命令窗口执行下面代码：

   如图所示：（想要进行别的命令操作，可以按`Ctrl + C`停止服务器）
   ![启动服务器](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/hexo-server.png)

   ```
   hexo server
   ```

2. 在浏览器地址栏中输入http://localhost:4000/  （默认端口是4000），如果能够看到如图所示的效果，说明初始化的Hexo博客搭建成功了。
   如图所示：
   ![浏览器中查看博客](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/hexo-blog.png) 

## 三、将本地的 Hexo 博客部署到 GitHub Pages上
1. 新建一个仓库，仓库名为`winney07.github.io`（这个仓库的名称必须严格按照 `username.github.io` 的格式来命名）【前提是你要有一个Github账号】
   如图所示：（因为我已经创建过这个库了，所以会显示红色警告，只是后来为了截图，重新写一个同名的）
   ![创建仓库](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/hexo-git.png)

2. 进入已经创建好的仓库（点击自己的头像，选择Your profile，点击刚创建好的那个仓库进去仓库里面），点击settings，找到GitHub Pages 选项，点击 Choose a theme 选择一个主题（可以选择也可以不选择，根据自己的需求决定是否操作这一步）
   如图所示：
   ![配置Github Pages](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/git-pages.png)

3. 配置Git个人信息，在`winneyBlog`目录下，鼠标右键，选择`Git Bash`，进入命令窗口，输入下面的命令

   ```
   git config --global user.name "Github用户名"       //自己Github的账号名
   git config --global user.email "Github邮箱"        //自己注册Github的邮箱地址
   ```

4. 生成SSH KEY,意思是生成一个公钥和密钥，因为Github需要一个密钥才能与本地相连接。在命令窗口输入下面的命令，然后需要连续按3次回车生成密钥（每按一次回车你可以看到对应的信息） 【你也可以先查看是否已经有了ssh密钥：`cd ~/.ssh`   如果没有密钥则不会有此文件夹，有则备份删除】

   ```
   ssh-keygen -t rsa -C  "Github邮箱"        //自己注册Github的邮箱地址
   ```

   如图所示：
   ![生成SSH KEY](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/ssh-key.png)

5. 生成的SSH KEY会保存到 `C:/Users/电脑名用户名/.ssh` 目录中（根据你自己电脑用户名，打开对应的目录）
   ![SSH KEY存放目录](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/win-user.png)
   （1）打开.ssh 这个目录，打开 id_rsa.pub 文件，复制里面的全部内容（这些内容就是密钥）
   ![打开 id_rsa.pub 文件](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/user-ssh.png)
6. 在GitHub中添加`SSH keys`
   1. 打开Github，点击头像，选择`Settings`；
      ![设置](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/set.png)
   2. 选择`SSH and GPG keys`项,点击右上角`New SSH key`按钮，将刚刚复制到的密钥粘贴到`key`输入框中，title自己给它命一个名就好
      ![添加ssh key 到仓库](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/add-key.png)
   3. 最后点击`Add Key`，如果显示这样的界面，说明SSH KEY 配置成功：
      ![SSH KEY 配置成功](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/ssh-keys.png)
7. 修改全局配置文件
   1. 在hexo文件夹下，找到`_config.yml`文件；
      如图所示：
      ![_config.yml文件](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/config1.png)
   2. 复制仓库地址：
      如图所示：
      ![复制仓库地址](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/git-href.png)
   3. 修改`_config.yml`文件里的deploy属性(目的是将本地hexo项目放到Github上)
      如图所示：
      ![修改_config.yml文件里的deploy属性](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/deploy.png)
      注：【如果`repository`中填写的是`https`协议的，`hexo d`上传代码到Github时有下面类似错误，可以将`repository`改为`ssh`的链接】
      如图所示：
      ![报错信息](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/deploy-error.png)
      ![使用 SSH链接](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Hexo-GitHub-Pages-%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/ssh-link.png)

8. 安装`hexo-deployer-git` 插件，目的是将代码快速托管到Github上

   ```
   npm install hexo-deployer-git --save
   ```

9. 将hexo项目托管到GitHub上（命令可以分开写也可以一起写）

   ```
   hexo clean && hexo generate && hexo deploy
   ```

     **备注：**
     `hexo clean` ：清除缓存文件 (db.json) 和已生成的静态文件 (public)
     `hexo generate` ：部署之前预先生成静态文件，简写为`hexo g`
     `hexo deploy` : 文件生成后立即部署网站，简写为`hexo d`

10. 在浏览器地址栏输入 https://username.github.io/ 即可访问，（username也就是你的Github账户名），如果能够正常访问，并且跟本地hexo项目显示的内容是一样的，那么说明你已经把本地hexo项目部署到Github上了。

## 四、配置博客的个人信息
1. 在hexo目录中，找到全局配置文件`_config.yml`

2. 配置信息如下所示：

   ```
   # Hexo Configuration
   ## Docs: https://hexo.io/docs/configuration.html
   ## Source: https://github.com/hexojs/hexo/
   
   # Site 站点信息配置
   title: winney     #站点名
   subtitle: It is never too old to learn.  #站点副标题
   description: Doing is better than saying.     #站点信息简介
   keywords: winneyBlog   博客
   author: winney   #站点作者
   language: zh-Hans     #站点语言，default默认是英文，zh-Hans是中文
   timezone: Asia/Shanghai      #时区
   
   # URL   博客地址
   ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
   url: https://AAAAAAAAAA.github.io/
   root: /
   permalink: :year/:month/:day/:title/
   permalink_defaults:
   
   # Directory  目录设置
   source_dir: source
   public_dir: public
   tag_dir: tags
   archive_dir: archives
   category_dir: categories
   code_dir: downloads/code
   i18n_dir: :lang
   skip_render:
   
   # Writing 文章布局
   new_post_name: :title.md # File name of new posts
   default_layout: post
   titlecase: false # Transform title into titlecase
   external_link: true # Open external links in new tab
   filename_case: 0
   render_drafts: false
   post_asset_folder: true
   relative_link: false
   future: true
   highlight:
     enable: true
     line_number: true
     auto_detect: false
     tab_replace:
     
   # Home page setting  主页设置
   # path: Root path for your blogs index page. (default = '')
   # per_page: Posts displayed per page. (0 = disable pagination)
   # order_by: Posts order. (Order by date descending by default)
   index_generator:
     path: ''
     per_page: 3  #每页文章数量
     order_by: -date
     
   # Category & Tag   分类和标签
   default_category: uncategorized
   category_map:
   tag_map:
   
   # Date / Time format  日期 / 时间格式
   ## Hexo uses Moment.js to parse and display date
   ## You can customize the date format as defined in
   ## http://momentjs.com/docs/#/displaying/format/
   date_format: YYYY-MM-DD
   time_format: HH:mm:ss
   
   # Pagination    归档显示
   ## Set per_page to 0 to disable pagination
   per_page: 10
   pagination_dir: page
   
   # Extensions  扩展
   ## Plugins: https://hexo.io/plugins/
   ## Themes: https://hexo.io/themes/
   theme: next
   
   # Deployment
   ## Docs: https://hexo.io/docs/deployment.html
   deploy:
     type: git    #部署的类型
     repository: https://github.com/AAAAAAA/AAAAAAA.github.io.git    #仓库地址
     branch: master    #分支名称
     message: hexo deploy  #提交信息
   
   #Search
   search:
     path: search.xml
     field: post
     format: html
     limit: 10000
   ```

     `注意`：`.yml` 文件有严格的格式要求，文件里所有的配置都是：冒号 空格 值，并且冒号是英文状态下的输入。想了解更多的可以前往 官网 。

3. 在博客目录下，右键点击Git Bash，进去命令窗口，输入下面的命令，即可在浏览器中看到刚刚设置的内容显示在页面中：

   ```
   hexo server    // 简写为 hexo s
   ```

#### 提交到远程仓库报错

报403或者每次提交都要输入账号密码

可以将`_config.yml`里的

```
repository: https://github.com/*********.github.io.git   #仓库地址
```

改为：

```
repository: git@github.com:*********.github.io.git   #仓库地址
```

