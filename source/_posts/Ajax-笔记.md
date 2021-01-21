---
title: Ajax-笔记
date: 2021-01-21 10:53:32
tags: 
- Ajax
categories: 
- 工作笔记
- Ajax
---

| [jQuery.ajax](https://api.jquery.com/jquery.ajax/)         |                                                        |      |      |      |
| ---------------------------------------------------------- | ------------------------------------------------------ | ---- | ---- | ---- |
| [AJAX教程](https://www.runoob.com/ajax/ajax-tutorial.html) | [W3school](https://www.w3school.com.cn/ajax/index.asp) |      |      |      |

```
$.ajax({
    url:"",
    timeout:8000,
    type:"POST",
    dataType:"json",
    data:{name:"大名",age:"23"},
    success:function(data,status,xhr){

    },
    error:function(xhr,status,error){
        $(".success").hide();
        $(".maskBg").hide();      
        if(xhr.status === 0){
            if(status === "timeout"){
                app.alert("网络不给力，请检查网络设置"); 
            }
        }else if(xhr.status.toString().charAt(0) === "4"){
            app.alert("客户端出错，请重新操作：" + xhr.status);   
        }else if(xhr.status.toString().charAt(0) == "5"){
            app.alert("服务端出错，请联系网站管理员！错误代码："  + xhr.status);  
        }
    }
})
```

