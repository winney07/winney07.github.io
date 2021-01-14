---
title: Vue项目处理跨域请求
date: 2020-12-14 11:42:51
tags:
- Vue.js
categories:
- 工作笔记
- Vue.js
---

#### 1、设置配置文件

- 方法一：在根目录中新建vue.config.js文件

```
module.exports = {
    runtimeCompiler: true,
    devServer: {
        proxy: {
            // 匹配请求路径中的字符，
            // 如果符合就用这个代理对象代理本次请求，路径为target的网址，
            // changeOrigin为是否跨域，
            // 如果不想始终传递这个前缀，可以重写路径
            // pathRewrite为是否将指定字符串转换一个再发过去。
            '/api': {
              target: 'http://ttapi.research.itcast.cn/',
                ws: true,
                changeOrigin: true,
                pathRewrite: {
                    '^/api': ''
                }
            }
        }
    }
}
```



- 方法二：在根目录中，新建config>index.js文件

```
module.exports = {
    dev: {
        proxyTable: {
            '/api': {
              target: 'http://ttapi.research.itcast.cn/', // 接口的域名
              secure: false, // 如果是https接口，需要配置这个参数
              changeOrigin: true, // 如果接口跨域，需要进行这个参数配置
              pathRewrite: {
                '^/api': '' // '/api/a/user' =='localhost:8080/user'
              }
            }
        }
    }
}

```

#### 2、axios请求方法的写法：

```
axios.get('http://ttapi.research.itcast.cn/app/v1_0/comments', {
    params: {
        type: 'a',
        source: this.source,
        offset: this.offset,
        limit: this.limit
    }
})
.then(function (response) {
    console.log('response')
    console.log(response)
})
.catch(function (error) {
    console.log(error)
})
```

#### name属性是父组件传过来的，除了数组，对象，其他都不允许修改

>  props里面的数据，除了数组，对象，其他都不允许修改，所以不能用于页面元素的v-model属性中，因为v-model是双向绑定的

```
<van-field
   v-model="localName"
   ...
/>
 props: {
     name: {
         type: String,
         required: true
     }
 },
 
data () {
  return {
      localName: this.name
  }
 },
```



#### 当传递给子组件的数据既要使用又要修改，这种情况下我们可以使用v-model简写：

例如：父组件的name

```
:name="user.name"
@update-name="user.name=$event"
```

修改为：

```
v-model="user.name"
```

子组件也要跟着修改：

```
 props: {
     value: {
         type: String,
         required: true
     }
 },
 
 this.$emit('input', this.localName)
```

> v-model="user.name"
>
> 默认传递一个名字叫value的数据：    ：value="user.name"
>
> 默认监听input事件:      @input="user.name=$event"
>
> v-model的本质还是父子组件通信，它仅仅是简化了父组件的使用，子组件还是按照原来那样使用

注：在同一个子组件传递中，v-model只能使用一次

```
这样是错误的：
<update-name
    v-model="user.name"
    v-model="user.photo"
/>
```

##### 在同一个子组件传递中，v-model只能使用一次，如果有多个数据需要保持同步，使用.sync修饰符

```
<update-name
    v-model="user.name"
    :gender.sync="user.photo"
/>
```

> 注：我们一般把最常用的数据设计为v-model绑定，把不太常用的数据设计为.sync



#### 销毁组件的一种方法：

1、加上v-if来控制渲染

```
<update-name
    v-if="isEditNameShow"
    v-model="user.name"
    @close="isEditNameShow=false"
/>
```

#### 在Vue中操作DOM，要给该元素添加ref属性

例如：点击头像，选择图片来修改头像

1、给input  file添加ref属性

```
<input type="file" hidden ref="file">
<van-cell title="头像" is-link center @click="$refs.file.click()">
    <van-image
        width="30"
        height="30"
        round fit="cover"
        :src="user.photo"
    />
</van-cell>
```

2、控制选择的文件类型：accept属性

```
<input type="file" hidden ref="file" accept="image/*">
```

3、监听文件的change事件

```
<input
    type="file"
    hidden
    ref="file"
    accept="image/*"
    @change="onFileChange"
>
```

4、解决选择相同文件不触发change事件,手动清空file的value值

```
onFileChange() {
    ....
    
     // 手动清空file的value值
     this.$refs.file.value = ''
}
```

5、展示弹出层，在弹出层预览图片

```
onFileChange() {
     // 展示弹出层
     this.isEditPhotoShow = true

    //  在弹出层预览选择的图片
    const blod = window.URL.createObjectURL(this.$refs.file.files[0])
    this.previewImage = blod

     // 手动清空file的value值
     this.$refs.file.value = ''
 }
```

6、父传，子收。并展示预览图片

```
父传：
<update-photo
    :image="previewImage"
/>
子收：
 props: {
     image: {
         type: String,
         required: true
     }
 },
 
<div class="update-photo">
     <img :src="image">
</div>
```

7、修改父子组件传值的文件格式

> 如果Content-Type  要求是 multipart/form-data，则一定要提交FormData数据对象，专门用于文件上传的，不能提交{}对象，没用

所以要修改父组件传过来子组件的文件格式，保留原来的文件格式：

```
父组件：
onFileChange() {
    ....
    const blod = this.$refs.file.files[0]
    this.previewImage = blod
	....
 }
 
<update-photo
    :file="previewImage"
    @close="isEditPhotoShow=false"
/>
子组件：
 props: {
     file: {
        //  type: String,
         required: true
     }
 },
 data () {
  return {
      image: window.URL.createObjectURL(this.file)
  }
 },
```

8、处理接口传参

```
// 文件格式处理
 const fd = new FormData()
 fd.append('photo', this.file)
 // photo为参数名，this.file为参数值

 await updateUserPhoto(fd)
```

9、处理图片裁切，使用 [cropperjs](https://github.com/fengyuanchen/cropperjs)  这个跟vue没有关系，其他项目也可以使用） 也可以在[Awesome](https://github.com/vuejs/awesome-vue) 中搜crop找裁切工具

- 1、安装

```
cnpm install cropperjs
```

- 2、引入

```
import 'cropperjs/dist/cropper.css'
import Cropper from 'cropperjs'
```

- 3、使用：放在mounted里面

```
<img :src="image" ref="image">

mounted() {
    const image = this.$refs.image
    const cropper = new Cropper(image, {
        viewMode: 1,
        dragMode: 'move',
        aspectRatio: 1,
        // autoCropArea: 1,
        cropBoxMovable: false,
        cropBoxResizable: false,
        background: false,
        movable: true
    })
    console.log(cropper)
},
```

- 4、让裁切区居中显示

```
.update-photo{
    position: absolute;
    top: 50%;
    margin-top: -185px;
    margin-left: -185px;
    height: 370px;
    left: 50%;
    width:370px;
}
```

- 5、获取裁切结果，getCroppedCanvas()

```
 data () {
  return {
      image: window.URL.createObjectURL(this.file),
      cropper: null
  }
 },

使用Promise返回一个裁切对象，用于async
 getCroppedCanvas() {
     return new Promise(resolve => {
     // 因为cropper定义在mounted中，在这里无法使用，
     	为了能够在这里能调用cropper，将cropper放在data中
          this.cropper.getCroppedCanvas().toBlob((file) => {
            resolve(file)
        })
     })
 },
 
getCroppedCanvas返回的Promise对象，在这里面使用：
async onConfirm() {
     .....
     const file = await this.getCroppedCanvas()
     const img = window.URL.createObjectURL(file)

    // 文件格式处理
     const fd = new FormData()
     fd.append('photo', file)
     
     await updateUserPhoto(fd)

     this.$emit('close')
     this.$emit('update-photo', img)

     this.$toast.success('保存成功')
 }
```

