---
title: vue3-vite-疫情
date: 2022-08-01 10:59:14
tags:
- Vue3
- Vite
categories:
- 前端开发框架
- Vue.js
---



`备注：` 对应项目vue3-vite-yiqing  【移动端——展示疫情实时数】

[Vite官网](https://vitejs.dev/guide/#scaffolding-your-first-vite-project)

优点：使用vite创建的项目，运行比webpack创建的要快

#### 创建项目

```
npm create vite@latest
```

```
√ Project name: ... vue3-vite-yiqing
√ Select a framework: » vue
√ Select a variant: » vue-ts
```

```
cd vue3-vite-yiqing
npm install
npm run dev
```

VSCode中安装Vetur插件

#### 安装less

```
cnpm i less less-loader -D
```

#### 在main.ts中引入reset.less

```
import './assets/css/reset.less'
```

#### reset.less

```
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	// font-size: 100%;
	// font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```

#### 设置根节点font-size值，使用rem适配

```
:root{
 font-size: 0.13333333vw;
}
```

> 这样设置之后1px = 1rem



#### 垂直居中

```
body {
  margin: 0;
  display: flex;
  place-items: center;
  min-width: 320px;
  min-height: 100vh;
}
```

#### 配置手机可访问本地电脑项目

[Vite 使用本地ip+localhost访问服务](http://www.manongjc.com/detail/29-saiyfskdbsqqcmz.html)

使用vite新建的项目默认访问链接：http://127.0.0.1:5173/

1. 修改`vite.config.js`文件，添加`server`配置

   ```
   server: {
       host: '0.0.0.0',
       port: 8888,
       open: true
   },
   ```

   ```
   export default defineConfig({
     plugins: [vue()],
     base:'./',    // 处理打包后放正式环境的相对路径的问题
     server: {		// 处理使用本地ip访问页面
       host: '0.0.0.0',
       port: 8888,
       open: true
     },
   })
   ```

2. 若使用手机访问本地ip页面，访问不成功（显示“服务器已停用”）。即要将本地电脑的防火墙“关闭”即可。[手机和电脑连接同一wifi,手机访问不了电脑起的项目](https://blog.csdn.net/zoepriselife316/article/details/117957732)

   电脑的“设置”——“网络和共享中心”——“Windows Defender 防火墙”（左下角）——“启用或关闭Windows Defender 防火墙”（左侧）——选择“关闭”（专用网络和公用网络都关闭）

   注意：使用完，最好重新“启用”防火墙。

[vite.config.js之resolve.alias配置](https://www.jianshu.com/p/dd26cae7d7b2)



#### axios请求数据

vue3中在onMounted生命周期中发出请求

```
cnpm i axios
```

```
import axios from 'axios';
import { onMounted } from 'vue'


onMounted(() => {
    console.log('onMounted')
    axios('https://c.m.163.com/api/ug/api/wuhan/app/data/list-total?t=330415245809')
    .then(res => {
        console.log(res);
    })

})
```

#### 跨域请求处理

修改`vite.config.ts`文件，添加以下代码

```
server: {
    // hmr: true,  // 开启热更新
   proxy: {
      '/api': {
        target: 'https://c.m.163.com',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      },
    }
}
```

`vite.config.ts`修改后

```
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()],
  base:'./',    // 处理打包后放正式环境的相对路径的问题
  server: {
    host: '0.0.0.0',
    port: 8888,
    open: true,
    proxy: {
      '/api': {
        target: 'https://c.m.163.com',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      },
    }
  },
})

```

注意：修改配置文件后，要重启项目。(在vite搭建的项目，不需要重启)

##### 修改请求链接

```
axios('/api/ug/api/wuhan/app/data/list-total?t=330415245809')
.then(res => {
    console.log(res);
})
```



#### 对接口获取到的数据对象使用TS进行数据类型约束

1. 使用泛型

   ```
   interface IData{
   	name: string;
   	type: number;
   }
   
   const data = reactive<IData>{
   	name: 'winney',
   	type: 1
   }
   ```

2. 企业级开发模式常用

#### 接口返回字段：

- input:境外输入
- noSymptom:无症状感染者
- incrNoSymptom:新增
- confirm:确诊
- dead:死亡
- heal:治愈
- 现有确诊数=累计确诊数-累计死亡数-累计治愈数
- confirm-dead-heal

总数：total

较昨日：today

## JS的实现

```
const data = reactive({
    name: "winney",
    areaTree: [],
    chinaDayList: [],
    chinaTotal: {},
    china: [],
    hbData: {},
    type: 1,
    mapType: 1,
    lineType: 1,
    lastUpdateTime:""
})
```

```
onMounted(() => {
    axios('/api/ug/api/wuhan/app/data/list-total?t=330415245809')
    .then(res => {
        const resData = res.data.data;
        data.areaTree = resData.areaTree;
        data.chinaDayList = resData.chinaDayList;
        data.chinaTotal = resData.chinaTotal;
    })
})
```

为了避免使用数据时，每次都写`data.` , 对数据进行解构

```
const { chinaTotal } = toRefs(data);
```

使用：

```
<p> <strong class="red">{{chinaTotal.total.input}}</strong></p>
```

直接使用会报错：

原因，异步请求是在组件onMounted之后的。 在第一次渲染的时候，当时还没有chinaTotal的数据

```
<ul class="tab-content" v-if="chinaTotal.total">
```



#### Tab切换模块的功能

```
// 获取中国的数据
data.china = data.areaTree.find((v) => v.id==="0").children;
// 获取湖北的数据
data.hbData = data.china.find((v) => v.id === "420000")
```

```
const { chinaTotal, hbData } = toRefs(data);
```

```
 <div class="tab-box" v-if="chinaTotal.total">  // 判断放在父盒子，做一次判断
 	
 	 <!-- 全国疫情数据 -->
 	 <ul class="tab-content" v-show="type=== 1">
 	  <!-- 湖北的数据 -->
 	  <ul class="tab-content" v-show="type=== 2">

</div>
```

#### tab切换事件

动态绑定class的方法 `:class="{active: type === 1}"`

```
<div class="tab-btn" @click="tabChange(1)" :class="{active: type === 1}">全国疫情数据(含港澳台)</div>
<div class="tab-btn" @click="tabChange(2)" :class="{active: type === 2}">湖北疫情数据</div>
```

```
const tabChange = (type: number) => {
    data.type = type
}
```



## TS的实现

不把跟业务无关的代码写在vue文件中

在src目录中新建一个type目录，存放所有的type

#### 1. `src/type/index.ts`

```
interface IData{
    name: string;
    type: number;
}
// 导出的时候要使用type,而不是普通对象
export type{
    IData
}
```

页面中使用：

```
import type { IData } from "../../type/index"
```

在src中新建pageJs目录，用于存放所有页面的逻辑js

#### 1. `pageJs/index.ts`

```
import type { IData } from "../type/index"
```



#### 2. `src/type/index.ts`

```
interface IData{
    name: string,
    areaTree: any[],
    chinaDayList: any[],
    chinaTotal: any[],
    china: any[],  // 中国的数据
    hbData: Object, // 湖北的数据
    type: number,
    mapType: number,
    lineType: number,
    lastUpdateTime:string
}

export type{
    IData
}
```

VSCode中TS实现接口的快捷方式：

![VSCode中ts实现接口](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/vue3-vite-%E7%96%AB%E6%83%85/Snipaste_2022-08-01_16-49-24.png)

![VScode中ts接口实现](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/vue3-vite-%E7%96%AB%E6%83%85/Snipaste_2022-08-01_16-50-16.png)



#### 2. `pageJs/index.ts`

优点：可重复使用

```
import type { IData } from "../type/index"

class InteData implements IData {
    name: string =""
    areaTree: any[] = []
    chinaDayList: any[] = []
    chinaTotal: any[] = []
    china: any[]= []
    hbData: Object = {}
    type: number = 1
    mapType: number = 1
    lineType: number = 1
    lastUpdateTime: string =""

}

export {
    InteData
}
```

#### 3.页面中使用

```
import { InteData } from '../../pageJs/index'
 
const data = reactive(new InteData())
```

#### 4.请求数据方法封装

注：setup函数中是不支持异步的

##### 4.1  `pageJs/index.ts`

```
import axios from 'axios';
import type { IData } from "../type/index"

class InteData implements IData {
    name: string =""
    areaTree: any[] = []
    chinaDayList: any[] = []
    chinaTotal: any[] = []
    china: any[]= []
    hbData: Object = {}
    type: number = 1
    mapType: number = 1
    lineType: number = 1
    lastUpdateTime: string =""

}

const initDataFun = (data:InteData) => {
    axios('/api/ug/api/wuhan/app/data/list-total?t=330415245809')
    .then(res => {
        const resData = res.data.data;
        data.areaTree = resData.areaTree;
        data.chinaDayList = resData.chinaDayList;
        data.chinaTotal = resData.chinaTotal;

        // 获取中国的数据
        data.china = data.areaTree.find((v) => v.id==="0").children;
        // 获取湖北的数据
        data.hbData = data.china.find((v) => v.id === "420000")
    })
}

export {
    InteData,
    initDataFun
}
```

##### 4.2 页面中使用

```
import { InteData, initDataFun } from '../../pageJs/index'

onMounted(() => {
    initDataFun(data)
})
```



## [Echarts](https://echarts.apache.org/zh/index.html)的使用

[地图图表](https://echarts.apache.org/examples/zh/editor.html?c=map-HK)

[在项目中引入 Apache ECharts](https://echarts.apache.org/handbook/zh/basics/import)

```
cnpm i echarts --save
```

```
<!-- 地图 -->
<div class="map-box">
    <div 
        :class="mapType === 1 ? 'to-left' : 'to-right'"
        id="map"
    ></div>
    <div 
        :class="mapType === 1 ? 'to-left' : 'to-right'"
        id="map2"
    ></div>
</div>
```

#### 2.`pageJs/index.ts`

```
import * as echarts from 'echarts';

type EChartsOption = echarts.EChartsOption;


const initDataFun = (data:InteData) => {
    var mapDom = document.getElementById('map')!;
    var mapDom2 = document.getElementById('map2')!;

    var optionMap: EChartsOption = {
        title:{
            subtext: '单击省份可查看病例数'
        },
        tooltip: { // 提示框
            trigger: 'item',
            formatter: '现有确诊病例<br/>{b}: {c}'
        },
        visualMap:{
            show:false
        }
    }
    var myMap = echarts.init(mapDom);
    var myMap2 = echarts.init(mapDom2);
    myMap.showLoading();
    myMap2.showLoading();
   ....
}
```

加上自带的loading

```
var myMap = echarts.init(mapDom);
var myMap2 = echarts.init(mapDom2);
myMap.showLoading();
myMap2.showLoading();
```

#### 获取数据

```
// 地图数据
let mapData:any[] = []
data.china.map((v:any) => {
    mapData.push({
        name: v.name,
        value: v.total.confirm - v.total.dead - v.total.heal || 0,
    })
})
```

#### 2.1.完整代码

```
const initDataFun = (data:InteData) => {
    var mapDom = document.getElementById('map')!;
    var mapDom2 = document.getElementById('map2')!;

    var optionMap: EChartsOption = {
        title:{
            subtext: '单击省份可查看病例数'
        },
        tooltip: { // 提示框
            trigger: 'item',
            formatter: '现有确诊病例<br/>{b}: {c}'
        },
        visualMap:{
            show:false
        }
    }

    // 将重复的配置抽出来
    var series = {
        type: "map",
        map: "china",
        colorBy: "series",
        zoom: 1.3,
        top: 80,
        label:{
            show: true,
            color: "#333",
            fontSize: 10,
        }
    }

    var myMap = echarts.init(mapDom);
    var myMap2 = echarts.init(mapDom2);
    myMap.showLoading();
    myMap2.showLoading();

    axios('/api/ug/api/wuhan/app/data/list-total?t=330415245809')
    .then(res => {
        const resData = res.data.data;
        data.areaTree = resData.areaTree;
        data.chinaDayList = resData.chinaDayList;
        data.chinaTotal = resData.chinaTotal;

        // 获取中国的数据
        data.china = data.areaTree.find((v) => v.id==="0").children;
        // 获取湖北的数据
        data.hbData = data.china.find((v) => v.id === "420000")

        // 地图数据
        let mapData:any[] = []
        data.china.map((v:any) => {
            mapData.push({
                name: v.name,
                value: v.total.confirm - v.total.dead - v.total.heal || 0,
            })
        })

        myMap.hideLoading();
        myMap.setOption({
            ...optionMap, 
            series:{
                ...series, 
                data: mapData,   // 数据源
            }
        })
    })
}
```

#### 3.引入china.json文件

[【echarts 中国地图】vue实现中国地图，省份居中china.json文件下载](https://blog.csdn.net/seeeeeeeeeee/article/details/121495485?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-4-121495485-null-null.pc_agg_new_rank&utm_term=china.json%20geojson&spm=1000.2123.3001.4430)

在pageJs/index.ts

```
import chinaJson from '../assets/china.json';

echarts.registerMap("china", (chinaJson as any))
```

## List组件封装

#### 子组件List组件：

```
<template>
    <div>
        数据列表组件
    </div>
</template>

<script setup lang='ts'>
const props = defineProps({
    list: Array,
    msg: String,
})

console.log(props.list)

</script>

<style lang='less' scoped>

</style>
```

#### 重点1：处理初始化会报错问题-判断是否渲染子组件

子组件的setup会在父组件的onMounted之前执行，所以传参的时候，要进行判断，是否渲染子组件

```
import List from '../../components/situation/List.vue';

<List v-if="china.length > 0" :list="china" :msg="'中国疫情'"/>
```



#### 动态数据传值

动态数据，这样写会报错：`:msg="中国疫情"`

要加上引号：`:msg="'中国疫情'"`



#### props里面的数据无需解构，可以直接使用

```
const props = defineProps({
    list: Array,
    msg: String,
})

{{list}}
```

#### 组件自调用——递归

#### 重点2：组件自调用，要写上name值

`List.vue`

```
<script setup name="List" lang='ts'>
</script>
```

```
<template>
    <div class="list-box">
        <div class="info-title info">
            <p>地区</p>
            <p>现有确诊</p>
            <p>确诊</p>
            <p>死亡</p>
            <p>治愈</p>
        </div>
        <div class="list" v-for="i in list" :key="i.id">
            <div class="p-box">
                <div class="info" @click="getShowChildren(i.id)">
                    <p>{{i.name}}</p>
                    <p>{{i.total.confirm - i.today.dead - i.today.heal}}</p>
                    <p>
                        <span>{{i.total.confirm}}</span>
                        <span>较昨日{{i.today.confirm}}</span>
                    </p>
                    <p>{{i.total.dead}}</p>
                    <p>{{i.total.heal}}</p>
                </div>
                  <!-- 世界数据不展示children -->
                <div v-if="showChildren">
                    <div class="children" v-show="data.isShowChildren == i.id">
                        <List :list="i.children"/>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
```

#### 重点3：定义子组件接收的属性

```
<script setup name="List" lang='ts'>
import { reactive } from 'vue';

const props = defineProps({
    list: Array,
    showChildren: Boolean  // 是否显示children数据 （中国病例显示，世界病例不显示—）
})
console.log(props.list)

const data = reactive({
    isShowChildren: ""    // 是否有children
})

const getShowChildren = (id: string) => {
    data.isShowChildren == id
    ? (data.isShowChildren = "")
    : (data.isShowChildren = id)
};

</script>
```

#### 文字溢出不换行显示

```
white-space: nowrap;
```



### 懒加载——下拉刷新上拉加载

国际病例数据较多——使用懒加载方式。

#### 上拉加载下拉刷新的组件-ScrollCom

```
<template>
    <div class="box">
        <!-- ref="scrollEl" 这里scrollEl 不是一个变量，是字符串-->
        <!-- :ref="scrollEl" 这里scrollEl 是一个变量-->
        <!-- ref不会被渲染到DOM元素上去， 是一个内部属性，
            用于与data中的属性进行绑定，如果在data中找到了对应名称的响应式的key值(属性)时,
            当这个元素渲染完之后，会把这个元素的指针给到data中与之相同的key值的对象上去-->

        <!-- 绑定滚动事件：@scroll -->
        <div 
            @scroll="scrollEvent"
            ref="scrollEl" 
            class="scrollEl">
            <div class="loadingBox" v-if="touchstartTitleShow">释放可刷新...</div>
            <div class="loadingBox" v-if="touchendTitleShow">加载中...</div>
            <!-- 插槽——————这个组件可以被多个组件使用 -->
            <slot></slot>
            <div v-if="!isScroll" class="">{{endText}}</div>
        </div>
    </div>
</template>

<script setup lang='ts'>
import { reactive, toRefs } from 'vue';

const props = defineProps({
    distance: {
        type: Number,
        default: 100
    },
    isScroll: Boolean,
    endText: {
        type: String,
        default: '没有更多了'
    }
})

 const $emit = defineEmits(['getList'])

const data = reactive({
    scrollEl: null,   // 用来装实例对象，  用于ref获取元素对象
    startText: "释放可刷新",
    scrollTop: 0,
    scrollY: 0,
    translateY: 0,
    touchstartTitleShow: false, // 控制手指按下屏幕的title显示
    touchendTitleShow: false,   // 控制手指离开屏幕的title显示
})

let { 
    scrollEl,
    startText,
    scrollTop,
    scrollY,
    translateY,
    touchstartTitleShow,
    touchendTitleShow,
 } = toRefs(data);

// 滚动事件
 const scrollEvent = (e:any) =>{
    data.scrollTop = e.srcElement.scrollTop;
    if(!props.isScroll) return;
    if(
        data.scrollTop + e.srcElement.offsetHeight > 
        e.srcElement.scrollHeight - props.distance
    ){
        // 获取下一页的数据————子组件给父组件传值
        $emit('getList')
    }
 }

</script>
```



#### 使用ScrollCom

```
<ScrollCom 
    :distance="100"
    :isScroll="true"
    @getList="getList"
>
    <List 
    	v-if="areaTree.length > 0"
    	:showChildren="false" 
    	:list="areaTree" 
    	:msg="'世界疫情'"/>
</ScrollCom>
```

#### 对分页加载的数据进行拆解

```
const getPageList = (list:any[]) => {
    const arr:Array<any[]>[] = [];  // 二维数组
    for(let index = 0; index < list.length; index += 30){
        arr.push(list.slice(index, index + 30))
    }

    return arr;
}



// 对分页加载的数据进行拆解
// 结构 如：[[1-30][31-60]....] 1-30条数据为第一页，31到60为第二页
data.areaTree = getPageList(resData.areaTree);
data.showList = data.areaTree[0];    // 第一页数据
```

第一页数据：`:list="showList"`

```
<ScrollCom 
    :distance="100"
    :isScroll="true"
    @getList="getList"
>
    <List v-if="showList.length > 0" :showChildren="false" :list="showList" :msg="'世界疫情'"/>
</ScrollCom>
```

##### 处理上拉加载报错：

```
TypeError: data.areaTree[page] is not iterable (cannot read property undefined)
```

原因：页数等于数据长度仍去获取数据； 解决：页数等于数据长度，就显示“没有更多”

```
if(page === data.areaTree.length - 1) {
    data.isScroll = false;  // 不可下拉加载数据
    return;
};
```

#### 下拉刷新

- touchstart
- touchmove
- touchend

```
<div 
    @scroll="scrollEvent"
    @touchstart="touchstart"
    @touchmove="touchmove"
    @touchend="touchend"
    ref="scrollEl" 
    :style="{top: `${translateY}px`}"
    class="scroll-box">
    <div class="loadingBox" v-if="touchstartTitleShow">释放可刷新...</div>
    <div class="loadingBox" v-if="touchendTitleShow">加载中...</div>
    <!-- 插槽——————这个组件可以被多个组件使用 -->
    <slot></slot>
    <div v-if="!isScroll" class="end-text">{{endText}}</div>
</div>
```

```
 // 手指触碰到屏幕
 const touchstart = (e:any) => {
    console.log(e.targetTouches[0])
    let y = e.targetTouches[0].pageY;
    data.startY = y;
 }

// 手指开始滑动
const touchmove = (e:any) => {
    let y = e.targetTouches[0].pageY;
    if(y > data.startY && data.scrollTop ==0) {
        data.touchstartTitleShow = true;
        // 如果当前移动距离大于初始点击坐标，则视为下拉，并且要处于顶部
        data.translateY = (y - data.startY) / 2;
    } else {
        data.touchstartTitleShow = false;
    }
};

// 手指松开
const touchend = (e:any) => {
    let y = e.changedTouches[0].pageY;
    if(y > data.startY) {
        data.translateY = 0;
        data.touchstartTitleShow = false;
        data.touchendTitleShow = true;
        $emit('refreshFun', () => {
            // 更新完数据的回调
            data.touchendTitleShow = false;
        })
        data.startY = 0;
    }
}
```

```
const $emit = defineEmits(['getList','refreshFun'])
```

#### 下拉刷新方法及回调处理

```
// 下拉刷新方法及 回调处理
const refreshFun = (fun:Function) =>{
    // 注：要将initDataFun改为promise函数  即使用async await
    
    initDataFun(data).then(() => {
        page = 0;
        data.isScroll = true;
        fun();
    })
}
```

注：要将initDataFun函数改为返回promise

```
const initDataFun = async (data:InteData) => {
	....
	let res = await axios('/api/ug/api/wuhan/app/data/list-total?t=330415245809')
	....
}
```

#### 下拉的空白区域的宽度

```
 :style="{top: `${translateY}px`}"
```



#### 折线图，y轴上的刻度数据被挡住，使用以下方法调整样式

```
yAxis: {
    axisLabel:{
      margin: -20,  
    }
},
```



### 打包上线

[关于vue3.0 + vite + ts 打包的坑](https://blog.csdn.net/qq_37656005/article/details/119818759)

[记一次 vue-tsc 引起的错误](https://www.modb.pro/db/114083)

打包报错：

将package.json的

```
"build": "vue-tsc --noEmit && vite build",
```

改为

```
"build": "vite build",
```

##### [vue3.0+vite+ts项目搭建-分环境打包(四)](https://www.shuzhiduo.com/A/nAJvZxqGJr/)

[rollup.js](https://rollupjs.org/guide/en/#outputmanualchunks  )



[ECharts y轴（yAxis）](https://blog.csdn.net/weixin_45536484/article/details/120041748)

备注：完整代码在`Gitee`中` Vue3_demo/vue3-vite-yiqing`

备注：获取疫情数据的接口：https://c.m.163.com/api/ug/api/wuhan/app/data/list-total?t=330415245809



[解决vue本地环境跨域请求正常，版本打包后跨域代理不起作用，请求不到数据的方法](https://cloud.tencent.com/developer/article/1620882)

[vue项目打包后请求地址错误/打包后跨域操作](https://www.qb5200.com/article/164553.html)

[**vite 打包后本地不能访问**](https://blog.csdn.net/weixin_43110440/article/details/124882324)

[vue3+vite项目配置axios及跨域](https://www.it610.com/article/1506847191577198592.htm)

#### [VITE+VUE3 跨域环境变量配置](https://blog.csdn.net/xm2395939/article/details/125140690?app_version=5.7.0&csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22125140690%22%2C%22source%22%3A%22winney07%22%7D&ctrtid=shInB&utm_source=app)

[神坑——后端允许了跨域但是前端（vue3+vite+axios）仍然提示跨域](https://blog.csdn.net/lsjweiyi/article/details/124645896)



#### [axios封装请求](https://www.it610.com/article/1506847191577198592.htm)

#### [使用vite如何配置跨域，以及环境配置](https://blog.csdn.net/jch923798729/article/details/123658250)

[vue部署Linux上 跨域问题](https://blog.csdn.net/m0_62152730/article/details/125082425)

```

var http = axios.create({
  timeout: 1000 * 20,
  baseURL: import.meta.env.DEV? '': import.meta.env.VITE_BASE_URL
})
```



```
server: {
  port: 4000, // 设置服务启动端口号
  open: true, // 设置服务启动时是否自动打开浏览器
  cors: true, // 允许跨域

  // 设置代理，根据我们项目实际情况配置
  proxy: {
    '/api': {
      target: env.VITE_BASE_URL, // 环境变量
      changeOrigin: true,
      secure: false,
      rewrite: (path) => path.replace('/api/', '')
    }
  }
}
```

https://blog.csdn.net/m0_62152730?type=blog