# winney07.github.io
个人博客

<span style="color:red;">备注：如果用hexo重新搭建一个博客，创建仓库后可以：1、先创建hexo分支，2、然后将hexo设置为默认分支，3、然后git clone到本地，4、然后再做其他操作</span>



#### 步骤

1. 在github创建winney07.github.io仓库

2. git clone https://github.com/winney07/winney07.github.io.git 到本地

   执行命令会报错：

   ```
   fatal: Not a git repository (or any of the parent directories): .git 
   ```

   原因是：没有切换到仓库目录，解决方法：切换到仓库目录

   

   **如果在一个没有.git文件夹的目录下报上面这个错**，就执行：

   ```
   git init
   ```

3. 切换到仓库目录

   ```
   cd winney07.github.io
   ```

4. 查看当前仓库：

   ```
   $ git branch
   * main
   ```

5. 在当前目录(winney07.github.io)下初始化Hexo

   ```
   hexo init
   ```

   报错：

   ```
   G:\Github\winney07.github.io not empty, please run `hexo init` on an empty folder and then copy your files into it
   ```

   原因：hexo init 项目名称     （项目名称不能为空）

   解决方案：

   1-对原有winney07.github.io目录重命名winney07.github.io-backup

   2-然后初始化hexo：

   ```
   hexo init winney07.github.io
   ```

6. 切换到winney07.github.io目录

   ```
   cd winney07.github.io
   ```

7. 安装依赖包

   ```
   cnpm i
   ```

8. 部署形成的文件

   ```
   hexo g
   ```

9. 启动服务器

   ```
   hexo s
   ```

   `如果想在4002端口允许：hexo s -p 4002 `

10. 将winney07.github.io-backup目录下的内容拷贝到winney07.github.io，即.git文件夹和README.md文件

    ```
    .git
    README.md
    ```

11. 提交到远程仓库

    ```
    hexo clean
    hexo g
    hexo d
    ```

    报错：

    ```
    Validating config
    ```

    解决方案：修改winney07.github.io\\_config.yml

12. 修改winney07.github.io\\_config.yml

    ```
    deploy:
      type: 'git' #部署的类型
      repository: https://github.com/winney07/winney07.github.io.git   #仓库地址
      branch: main   #分支名称    
      ——————hexo d的代码是部署到main分支里面的(而博客的链接就是访问main分支里面的内容),即博客的内容
    ```

    报错：

    ```
    INFO  Validating config
    ERROR Deployer not found: git
    ```

    解决方案：

    ```
    cnpm i --save hexo-deployer-git
    ```

13. 创建博客文章

    ```
    hexo new "博客文章标题名称"
    ```

14. 再次执行：

    ```
    hexo clean
    hexo g
    hexo d
    ```

14. 修改hexo的主题为next（winney07.github.io\\_config.yml）,

    注：下载next主题放在themes目录下

    ```
    theme: next
    ```

15. 修改主题样式，选择Pisces（winney07.github.io\themes\next\\_config.yml）

    ```
    # scheme: Muse  ——默认是Muse
    #scheme: Mist
    scheme: Pisces
    #scheme: Gemini
    ```
    
17. 修改站点个人信息（winney07.github.io\\_config.yml）

    ```
    # Site 站点信息配置
    title: winney     #站点名
    subtitle: It is never too old to learn.  #站点副标题
    description: Doing is better than saying.     #站点信息简介
    keywords: winneyBlog   博客
    author: winney   #站点作者
    language: zh-CN     #站点语言，default默认是英文，zh-Hans是中文
    timezone: Asia/Shanghai      #时区
    ```

18. 如果之前有博客，把之前的博客仓库source目录下的内容拷贝到winney07.github.io\source

19. 重新生成文件

    ```
    hexo clean
    hexo g
    hexo d
    ```

20. 自定义hexo文章置顶(node_modules\hexo-generator-index\lib\generator.js)

    ```
    // sort(posts.data, (a, b) => (b.sticky || 0) - (a.sticky || 0));
    
    posts.data = posts.data.sort(function(a, b) {
        if(a.top && b.top) { // 两篇文章top都有定义
            if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
            else return b.top - a.top; // 否则按照top值降序排
        }
        else if(a.top && !b.top) { // 以下是只有一篇文章top有定义，那么将有top的排在前面（这里用异或操作居然不行233）
            return -1;
        }
        else if(!a.top && b.top) {
            return 1;
        }
        else return b.date - a.date; // 都没定义按照文章日期降序排
    });
    ```

21. 再次部署(实在没有清缓存的话，将.deploy_git和public目录下的内容清空)

    ```
    hexo clean
    hexo g
    hexo s
    hexo d
    ```

    如果看到页面还是的置顶排序还是没有变化

    试一下将post_asset_folder修改为true，（winney07.github.io\\_config.yml）

    ```
    post_asset_folder: true
    ```

22. 修改每页显示博客数量（winney07.github.io\\_config.yml）

    ```
    per_page: 3
    ```

23. hexo-next添加搜索功能

    - 安装插件

      ```
      cnpm i hexo-generator-searchdb --save
      ```

    - 修改站点的配置文件（winney07.github.io\\_config.yml）

      ```
      #Search
      search:
        path: search.xml
        field: all
        format: html
        limit: 10000
      ```
      > `path`：索引文件路径，相对于根目录
      > `field`：搜索范围，默认是post，另外可以选择page、all，设置成all表示搜索所有页面
      > `limit`：最大搜索条目数
      >
      > 这里把field改为all

    - 修改next主题配置文件（themes\next\\\_config.yml找到 local_search 项，将它的enable修改为true）

      ```
      local_search:
        enable: true
      ```

24. 创建分支hexo（用于存放博客的源文件） [参考教程](https://www.cnblogs.com/kaerxifa/p/11045573.html)

    ```
    创建hexo分支：
    $ git branch hexo
    
    查看当前所有分支：
    $ git branch
      hexo
    * main
    
    推送到远程服务器：git push origin 分支名称
    git push origin hexo
    
    Create a pull request for 'hexo' on GitHub by visiting(在github仓库中就可以看到hexo分支)
    ```

25. 在该仓库->Settings->Branches->Default branch中将默认分支设为hexo

    > 将仓库克隆下来（因为已经有仓库的目录，新建一个文件夹存放clone下来的内容），将里面的.git文件夹覆盖winney07.github.io目录下的.git文件夹
    >
    > ---可以在创建仓库的时候就创建hexo分支，就不会因为提交了比较多的内容，clone的时间比较长

26. 查看当前所在分支：

    ```
    $ git branch
    * hexo
    
    可以看到已经切换到hexo分支
    ```

27. 将博客源文件提交到hexo分支

    ```
    git add .
    git commit -m 'back up hexo files'
    git push
    
    在github仓库的hexo分支可以看到备份的源文件
    ```

28. 修改博客网页添加到手机主屏幕的显示图标

    themes里面的apple-touch-icon-next.png

    1. `\themes\next\layout\_partials\head\head.swig`
    
       ```
       {%- if theme.favicon.apple_touch_icon %}
         <link rel="apple-touch-icon" sizes="180x180" href="{{ url_for(theme.favicon.apple_touch_icon) }}">
       {%- endif %}
       ```
    
    2. `\themes\next\_config.yml`
    
       ```
       favicon:
         small: /images/favicon-16x16-next.png
         medium: /images/favicon-32x32-next.png
         apple_touch_icon: /images/apple-touch-icon-next.png
         safari_pinned_tab: /images/logo.svg
       ```
    
       
    
    

> hexo d 部署的代码到main分支，也就是博客网页访问的内容
>
> git push的内容是提交到hexo分支，用作备份博客的源文件，配置文件等



终于部署完，坚持就是胜利。 在折腾的过程中，才能更好地理解git分支



注：db.json文件不需要上传到GitHub，克隆项目，运行项目时，会重新生成。





报错：

```
 14 files changed, 8968 insertions(+), 8866 deletions(-)
kex_exchange_identification: Connection closed by remote host
Connection closed by 20.205.243.166 port 22
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
FATAL {
  err: Error: Spawn failed
      at ChildProcess.<anonymous> (H:\Github\winney07.github.io\node_modules\hexo-deployer-git\node_modules\hexo-util\lib\spawn.js:51:21)
      at ChildProcess.emit (node:events:390:28)
      at ChildProcess.cp.emit (H:\Github\winney07.github.io\node_modules\cross-spawn\lib\enoent.js:34:29)
      at Process.ChildProcess._handle.onexit (node:internal/child_process:290:12) {
    code: 128
  }
} Something's wrong. Maybe you can find the solution here: %s https://hexo.io/docs/troubleshooting.html

```

重新再执行一次以下代码：

```
hexo clean && hexo g && hexo d
```



### [一个github账号怎么实现多个静态网站](https://blog.csdn.net/qq_39583550/article/details/128546569)

1. 往仓库里面放入`index.html`文件
2. 设置里面开启github page
3. 此时就可以通过`username.github.io/仓库名`访问了(部署需要时间, 需要稍等片刻哦)

在新创建的仓库中，选择`“Setting"——>”Pages"——>"**Branch**"选择"main"(选择网页所在分支)`
