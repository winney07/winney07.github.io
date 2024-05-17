---
title: 修改文件选择框input type=file的样式
date: 2019-08-14 14:56:23
tags:
- CSS
categories: 
- CSS
---
文件选择框(input type="file")的默认样式跟项目中的样式不是很搭，所以需要修改文件选择框的样式。

效果图：

![文件选择框](https://images.winney07.cn/blog/input-file-btn.png)

## 方式一，使用::file-selector-button

HTML:

```
<input type="file" id="default-btn">
```

CSS:

```
#default-btn::file-selector-button{
    padding: 6px 10px;
    background-color: #1E9FFF;
    border: 1px solid #1E9FFF;
    border-radius: 3px;
    cursor: pointer;
    color: #fff;
    font-size: 12px;
}
```

这种方法，文件选择框右侧默认就显示“未选择文件”的文字。如果您想隐藏这些文字，可以设置选择框`input`元素的`font-size：0`，即：

```
#default-btn{
    font-size: 0;
}
```

了解更多关于[::file-selector-button](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::file-selector-button)

## 方式二，使用label标签

HTML：


```
<span>
    <label for="fileInput" class="input-button" title="选择您的头像图片进行上传">选择文件</label>
    <input id="fileInput" type="file" style="display: none;">
</span>
<span id="fileName"></span>
```

CSS： 


```
.input-button {
    display: inline-block;
    padding: 6px 10px;
    background-color: #1E9FFF;
    border: 1px solid #1E9FFF;
    border-radius: 3px;
    cursor: pointer;
    color: #fff;
    font-size: 12px;
}
```

## 方式三，使用相对定位+透明

HTML：


```
<span class="inputBtn">
    <span>选择文件</span>
    <input class="inputFile" type="file" id="myImg" name="myImg" title="选择您的头像图片进行上传">
    </span>
<span id="fileName"></span>
```

CSS：

```
.inputBtn {  
    position: relative;  
    display: inline-block;  
    padding: 6px 10px;  
    border: 1px solid #1E9FFF;  
    border-radius: 3px;  
    background-color: #1E9FFF;  
    cursor: pointer;  
    font-size: 12px;  
    color: #fff;  
}  
.inputBtn:hover{  
    border: 1px solid #3aa9fb;  
    background-color: #3aa9fb;  
}  
.inputFile {  
    position: absolute;  
    left: 0;  
    top: 0;  
    width: 100%;  
    height: 100%;  
    opacity: 0;  
    filter: alpha(opacity=0);  
}  
```

> 方法三无法修改鼠标移上去时的手势，即input框设置为\`cursor: pointer\`不生效。因为方法三将input框的透明度设置为0，实际上还是在按钮上方的。如果项目没有要求鼠标移上去时的手势，就忽略这个问题。



## 显示上传文件的文件名称：

> 针对方法二和方法三

效果图：

![显示文件名称](https://images.winney07.cn/blog/input-file-btn2.png)

默认的文件选择框上传完文件之后，在右侧会显示上传文件的文件名称。如果需求需要显示，则可以按以下方式实现，如果不需要可忽略。   

```
const myImgEL = document.getElementById('myImg');  
const fileNameEL = document.getElementById('fileName');  
myImgEL.addEventListener('change', (event) => {
    // event.target.value的值打印是C:\fakepath\head.jpg
    // var name = event.target.value.split('\\')[2];	// 这种方式也可以  
    // console.log(name);
    const fileName = event.target.value.match(/[^\\|/]*$/)[0];
    console.log(fileName)
    fileNameEL.innerHTML = fileName;
});
```



想鼠标移上去，显示手指手势，设置了`cursor: pointer;`不起作用，解决方法：将input的字体大小设置为0：`font-size: 0`
