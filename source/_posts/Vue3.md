VSCode 编写Vue项目安装Vetur插件实现   代码高亮

#### VSCode中配置Vue3 +  TS 的用户代码片段

设置——配置用户代码片段——新建代码片段——代码片段文件名（输入该快捷键生成代码片段--例如：vue3）

输入以下内容：

```
{
	"vue-template": {
		"prefix": "vue3",
		"body": [
		"<template>",
		"",
		"</template>",
		"",
		"<script setup lang='ts'>",
		"",
		"</script>",
		"",
		"<style lang='less' scoped>",
		"",
		"</style>",
		],
		"description": "my vue3 template"
	}
}
```

##### 使用方法：

在新建的.vue文件中，输入’vue3‘，即可快速生成以下代码：

```
<template>

</template>

<script setup lang='ts'>

</script>

<style lang='less' scoped>

</style>
```



