---
title: WEB前端-页面跳转的相关处理
date: 2019-09-12 11:33:31
tags:
- JavaScript
categories: 
- JavaScript
---
### 跳转到新页面

```
window.location.assign('https://www.baidu.com/');
```

```
window.location.href = https://www.baidu.com/
```

如果想在新标签中打开：

```
window.open("https://www.baidu.com/");
```

#### 阻止浏览器的默认行为

```
function stopDefault(e) { 
	if ( e && e.preventDefault ) {
		e.preventDefault(); 
	}
}
```
