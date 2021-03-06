---
title: Wampserver-笔记
date: 2021-01-18 15:50:25
tags:
- Wampserver
categories:
- 工作笔记
- Wampserver
---

注：如果重新有问题，启动服务一直是黄色，可以卸载了wamp，然后重启电脑，再重装

#### phpmyadmin默认SQL账号密码:

```
账号：root，密码为空
```

{% asset_img note1.png %}

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

{% asset_img note2.png %}

