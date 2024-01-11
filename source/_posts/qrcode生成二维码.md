---
title: qrcode生成二维码
date: 2021-01-27 11:09:11
tags:
- qrcode
categories: 
- 工具
---

####  qrcode生成二维码

```
<script type="text/javascript" src="jquery.min.js"></script>
<script type="text/javascript" src="qrcode.js"></script>
```

```
<input id="text" type="text" value="https://www.baidu.com/" style="width:80%" /><br />
<div id="qrcode" style="width:100px; height:100px; margin-top:15px;"></div>
```

```
<script type="text/javascript">
    var qrcode = new QRCode(document.getElementById("qrcode"), {
        width : 100,
        height : 100
    });

    function makeCode () {		
        var elText = document.getElementById("text");

        if (!elText.value) {
            alert("Input a text");
            elText.focus();
            return;
        }

        qrcode.makeCode(elText.value);
    }

    makeCode();

    $("#text").on("blur", function () {
        makeCode();
    }).on("keydown", function (e) {
        if (e.keyCode == 13) {
            makeCode();
        }
    });
</script>
```

#### 微信二维码电子名片生成系统

[【示意图】](https://gitee.com/winney/work/blob/master/Plugs/qrcode/code.png)

清空二维码

```
qrcode.clear(); // clear the code.
```

加上中文内容会报错：

```
qrcode.min.js:1 Uncaught Error: code length overflow. (3452>1440)
```

解决方案：

 [Keeex/qrcode]( https://github.com/KeeeX/qrcodejs)，用这里的js替换原来的js，但生成的内容格式跟原来的是不一样的。