---
title: Wampserver-笔记
date: 2021-01-18 15:50:25
tags:
- Wampserver
categories:
- 工具
- Wampserver
---

注：如果重新有问题，启动服务一直是黄色，可以卸载了wamp，然后重启电脑，再重装

#### phpmyadmin默认SQL账号密码:

```
账号：root，密码为空
```

![phpmyadmin默认SQL账号密码](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Wampserver-%E7%AC%94%E8%AE%B0/note1.png)

#### 虚拟目录的配置 

修改默认网站目录

第一步：修改d:\wamp\bin\apache\Apache2.4.9\conf\httpd.conf

```
查找： DocumentRoot "c:/wamp/www/"
修改： DocumentRoot "d:/www/"
查找： <Directory "c:/wamp/www/">
修改： <Directory "d:/www/">
```

第二步：修改wampmanager.ini和wampmanager.tpl

1、修改c:\wamp\wampmanager.ini:

```
(1)打开：c:\wamp\wampmanager.ini
(2)查找：Type: item; Caption: "www 目录"; Action: shellexecute; FileName: "c:/wamp/www"; Glyph: 2
(3)修改：Type: item; Caption: "www 目录"; Action: shellexecute; FileName: "d:/www"; Glyph: 2
```

2、修改c:\wamp\wampmanager.tpl：

```
(1)打开：c:\wamp\wampmanager.tpl
(2)查找：Type: item; Caption: "${w_wwwDirectory}"; Action: shellexecute; FileName: "${wwwdir}"; Glyph: 2
(3)修改：Type: item; Caption: "${w_wwwDirectory}"; Action: shellexecute; FileName: "d:/www"; Glyph: 2
```

#### 修改默认项目目录

1、修改httpd.conf:

```
DocumentRoot "D:/Work/"
<Directory "D:/Work/">
```

2、修改httpd-vhost.conf:

```
<VirtualHost *:80>
	ServerName localhost
	ServerAlias localhost
	DocumentRoot D:/Work/
	<Directory  "D:/Work/">
		Options +Indexes +Includes +FollowSymLinks +MultiViews
		AllowOverride All
		Require local
	</Directory>
</VirtualHost>
```

#### 本地项目-配置服务器访问

1、配置host（C:\Windows\System32\drivers\etc）

例如：

```
127.0.0.1       localhost
192.168.1.49    www.web.com
```

2、配置httpd-vhosts.conf（wampserver\bin\apache\apache2.4.23\conf\extra\httpd-vhosts.conf）

例如：

```
#
listen 8081
<VirtualHost *:8081>
    ServerName www.web.com
    DocumentRoot "E:/wampserver/www/web"
    <Directory "E:/wampserver/www/web">
      Options Indexes FollowSymLinks
      AllowOverride All
      Order allow,deny
      Allow from all
    </Directory>
</VirtualHost>
#
```

3、访问的时候，使用www.web.com来访问本地项目

#### Apache相对路径文件的放置

![Apache相对路径文件的放置](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Wampserver-%E7%AC%94%E8%AE%B0/note2.png)



#### 权限问题——配置

修改`wamp\bin\apache\apache2.4.23\conf\http.conf` 文件

将`Require all denied` 注释掉，改为`Require all granted`

```
<Directory />
    AllowOverride none
    #Require all denied
    Require all granted
</Directory>
```

![权限问题](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Wampserver-%E7%AC%94%E8%AE%B0/1%E6%9D%83%E9%99%90%E9%97%AE%E9%A2%98.png)

#### 工作目录-路径问题——配置

修改`wamp\bin\apache\apache2.4.23\conf\http.conf` 文件

将`DocumentRoot "${INSTALL_DIR}/www"` 和 `<Directory "${INSTALL_DIR}/www/">`  注释掉，更改了工作目录的路径

```
#DocumentRoot "${INSTALL_DIR}/www"
#<Directory "${INSTALL_DIR}/www/">

DocumentRoot "E:/work"
<Directory "E:/work/">
```

![工作目录-路径问题](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Wampserver-%E7%AC%94%E8%AE%B0/2.%E5%B7%A5%E4%BD%9C%E7%9B%AE%E5%BD%95-%E8%B7%AF%E5%BE%84%E9%97%AE%E9%A2%98.png)

#### 手机访问问题——配置

修改`wamp\bin\apache\apache2.4.23\conf\http.conf` 文件

在`Require local` 前面加上`Require all granted `和 ` Allow from all`

```
<Directory "E:/work/">
    #
    # Possible values for the Options directive are "None", "All",
    # or any combination of:
    #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
    #
    # Note that "MultiViews" must be named *explicitly* --- "Options All"
    # doesn't give it to you.
    #
    # The Options directive is both complicated and important.  Please see
    # http://httpd.apache.org/docs/2.4/mod/core.html#options
    # for more information.
    #
    Options +Indexes +FollowSymLinks +Multiviews

    #
    # AllowOverride controls what directives may be placed in .htaccess files.
    # It can be "All", "None", or any combination of the keywords:
    #   AllowOverride FileInfo AuthConfig Limit
    #
    AllowOverride all

    #
    # Controls who can get stuff from this server.
    #
    Require all granted
    Allow from all

#   onlineoffline tag - don't remove
    Require local
</Directory>
```

![手机访问问题](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/Wampserver-%E7%AC%94%E8%AE%B0/3.%E6%89%8B%E6%9C%BA%E8%AE%BF%E9%97%AE%E9%97%AE%E9%A2%98.png)