# winney07.github.io
个人博客

#### 步骤

1. 在github创建winney07.github.io仓库

2. git clone https://github.com/winney07/winney07.github.io.git 到本地

   执行命令会报错：

   ```
   fatal: Not a git repository (or any of the parent directories): .git 
   ```

   解决方法：

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

10. 将原来winney07.github.io-backup目录下的内容拷贝到winney07.github.io