---
title: Windows环境下利用CMD命令批量修改文件名
date: 2020-01-06 15:54:28
tags:
- 常用命令
categories:
- 常用命令
---
### Windows环境下利用CMD命令批量修改文件名
#### 核心命令
##### ·文件重命名 <span style="color:#c7254e;">ren</span>

1、ren即rename的缩写，使用ren或者rename命令均可实现文件重命名的操作；命令的使用方法很简单，格式为 <span style="color:#c7254e;">ren old_name new_name</span> ；例如，想要将D盘根目录下的文件 a.txt 重命名为 b.doc ，只需要在CMD中进入D盘根目录，执行 <span style="color:#c7254e;">ren a.txt b.doc </span>；或者使用绝对路径，执行 <span style="color:#c7254e;">ren D:\a.txt b.doc  </span>，也可以达到同样的效果

2、需要注意的是，旧文件名 <span style="color:#c7254e;">old_name </span>可以使用相对路径，也可以包含绝对路径，但新文件名 <span style="color:#c7254e;">new_name</span>不能包含任何文件路径，只能是纯文件名；所以，要想批量修改包含子文件夹的多个路径下的大量文件名，还需要用到一款支持通配符匹配查询替换的文本编辑器，以便从路径+文件名的文件目录系统中提取出文件名的部分

3、另外， <span style="color:#c7254e;">ren</span> 也支持使用通配符；例如，想要将扩展名为 <span style="color:#c7254e;">.docx </span>的文件扩展名批量修改为 <span style="color:#c7254e;">.doc</span> ，执行 <span style="color:#c7254e;">ren *.docx  *.doc</span> 即可；但通配符的使用规则十分复杂，若无法完全理解其中的匹配规则，建议只使用通配符来修改文件扩展名


摘抄自：https://blog.csdn.net/hitomitoi/article/details/81566494
