---
title: Markdown
date: 2021-06-10 14:26:57
tags: Markdown
---

#### Markdown合并表格单元格

Markdown本身不支持单元格合并

> 考虑到 Markdown 支持 html ，
> 所以，我们可以通过插入 html 中的 table 来实现。

#### Html 合并行

```
<table>
    <tr>
        <td>第一列</td> 
        <td>第二列</td> 
   </tr>
    <tr>
        <td colspan="2">这里是合并行</td>    
    </tr>
    <tr>
        <td colspan="2">这里也是合并行</td>    
    </tr>
</table>
```

#### Html 合并列

```
<table>
    <tr>
        <td>第一列</td> 
        <td>第二列</td> 
   </tr>
    <tr>
        <td rowspan="2">这里是合并列</td>    
        <td >行二列二</td>  
    </tr>
    <tr>
        <td >行三列二</td>  
    </tr>
</table>
```

#### Html 合并行和列

```
<table>
    <tr>
        <td>第一列</td> 
        <td>第二列</td> 
   </tr>
   <tr>
        <td colspan="2">我是合并行</td>    
   </tr>
   <tr>
        <td>行二列一</td> 
        <td>行二列二</td> 
   </tr>
    <tr>
        <td rowspan="2">我是合并列</td>    
        <td >行三列二</td>  
    </tr>
    <tr>
        <td >行四列二</td>  
    </tr>
</table>
```

##### 在markdown文档中使用GitHub仓库的图片地址

1. 在GitHub中创建一个`Public`仓库存放图片

   注意：建立`Private`仓库，图片访问时，后面会加上一个token值，过一段时间就会失效。（这个很关键）

2. 在仓库中选择“Add file”——Upload files，直接把图片上传到仓库；也可以将仓库下载到本地，然后push上去
3. 在仓库中，选择需要的图片点进去，然后选择“Download"按钮，会新开一个窗口显示图片
4. 复制新开窗口中，复制图片的访问路径(域名地址栏)
5. 在markdown中插入图片标签，如： `![加载失败的文字提示](图片的链接)`

#### [如何用markdown文档做任务清单](https://jingyan.baidu.com/article/ab69b27090131d2ca7189f85.html)

```
- [ ] aaa
- [ ] bbb
-空格[空格]空格aaaa
```

### markdown编辑软件

- Typora（收费了）
- 在VSCode中，安装Typora扩展（Edit markdown like typora in vscode.），还不错。跟Typora真的挺像的。

### markdown自动生成器

##### [docsify](https://docsify.js.org/#/)

#### 语雀
