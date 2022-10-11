---
title: ad_manage_react-项目笔记
date: 2021-10-10 11:31:33
tags:
- React
- 项目笔记
---

### 启动项目注意事项：

1. 启动Apifox应用——项目的mock接口

### 项目目录结构

```
src
│  App.js
│  App.less
│  App.test.js
│  index.css
│  index.js
│  reportWebVitals.js
│  setupTests.js
│
├─api					——接口文件（分模块）
│      source.js		——素材管理模块相关Api
│      user.js			——用户模块相关Api
│
├─app								——app公用
│      BreadcrumbMap.jsx			——面包屑相关配置
│      leftMenus.js					——左侧导航栏相关数据
│      leftMenus—对应旧的LeftNav.js	  ——antd左侧导航旧版的做法
│      rootReducers.js				——reducer的集合
│      router.js					——路由配置
│      store.js						——store的配置
│
├─assets							——静态资源
│  ├─css
│  │      style.css
│  │
│  ├─images
│  │      header.jpeg
│  │
│  └─less							
│          common.less				——公用样式
│          cover_antd.less			——覆盖antd默认样式的样式文件
│          style.less				——其他样式
│
├─components						——组件集合
│  │  Bottom.jsx					——页面底部
│  │  EditableTable.jsx				——可编辑表格
│  │  LeftNav-旧的使用方法.jsx
│  │  LeftNav.jsx					——左侧导航栏组件
│  │  Top.jsx						——页面顶部
│  │
│  └─charts							——图表相关组件
│          LineChart.jsx			——线性图组件
│
├─pages								——页面组件（根据模块划分）
│  ├─agent
│  │      Account.jsx
│  │      AddAccount.jsx
│  │      AddAgent.jsx
│  │      Agent.jsx
│  │
│  ├─dashboard
│  │      Overview.jsx
│  │
│  ├─group
│  │      AddGroup.jsx
│  │      Group.jsx
│  │
│  ├─home
│  │      Container.jsx
│  │      Home.jsx
│  │
│  ├─login
│  │      Login.jsx
│  │
│  ├─manage
│  │      Customevent.jsx
│  │      Datacb.jsx
│  │
│  ├─product
│  │      AddProduct.jsx
│  │      EditProduct.jsx
│  │      Product.jsx
│  │
│  ├─source
│  │      AddSource.jsx
│  │      EditSource.jsx
│  │      Source.jsx
│  │      SourceUpload.jsx
│  │
│  ├─tool
│  │      Attribute.jsx
│  │      Logtool.jsx
│  │
│  └─user
│          EditPassword.jsx
│
├─reducers							——reducers相关（根据模块划分）
│      userSlice.js					——用户模块相关reducer处理
│
└─utils								——自定义相关文件
        fetchUtil.js				——接口请求相关封装
```



## 项目笔记

[在 create-react-app 中使用](https://ant.design/docs/react/use-with-create-react-app-cn)

注：先引入less，免得后面再来配置的时候，由于依赖包之间的版本之间存在冲突问题。

#### 安装和初始化

```
yarn create react-app ad_manage_react
```

```
cd antd-demo
yarn start
```

#####  安装并引入 antd

```
yarn add antd
```

##### 安装 craco 并修改 `package.json` 里的 `scripts` 属性

```
yarn add @craco/craco
```

```
/* package.json */
"scripts": {
-   "start": "react-scripts start",
-   "build": "react-scripts build",
-   "test": "react-scripts test",
+   "start": "craco start",
+   "build": "craco build",
+   "test": "craco test",
}
```

在项目根目录创建一个 `craco.config.js` 用于修改默认配置

##### 自定义主题

首先把 `src/App.css` 文件修改为 `src/App.less`，然后修改样式引用为 less 文件。

```diff
/* src/App.js */
- import './App.css';
+ import './App.less';
```

```
/* src/App.less */
- @import '~antd/dist/antd.css';
+ @import '~antd/dist/antd.less';
```

然后安装 `craco-less` 并修改 `craco.config.js` 文件如下。

```
yarn add craco-less
```

```bash
const CracoLessPlugin = require('craco-less');

module.exports = {
  plugins: [
    {
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': '#1DA57A' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};
```

#### 添加react-router-dom@6

```
yarn add react-router-dom@6
```

#### 添加react-redux

```
yarn add react-redux
```

#### 添加Redux Toolkit

```
yarn add @reduxjs/toolkit
```

#### 添加redux-persist

```
yarn add redux-persist
```

#### 异步获取数据

##### useEffect

##### 可变的变量不放在useEffect中

错误用法：

这样写会报错

```
let sourceList = [];
useEffect(() => {
    getSourcesList(1).then(res => {
    	sourceList = res
    })
},[])
```



 改为：

注：useEffect后面的依赖项，要加[]，不加，会一直执行这个方法。

```
const [sourceList, setSourceList] = useState([]);
useEffect(() => {
    getSourcesList(1).then(res => {
      console.log('res获取素材列表');
      console.log(res);
      setSourceList(res)
    })
},[])
```



#### antd表格

数组数据，每一项要有key值



#### 使用数据图表

[使用echarts-for-react数据图表](https://www.csdn.net/tags/MtjaUg3sNTM3OTQtYmxvZwO0O0OO0O0O.html)

##### [ECharts for React](https://git.hust.cc/echarts-for-react/)

[ECharts--官网文档](https://echarts.apache.org/zh/option.html#title)



注：要安装echarts，不然会报以下错误：

```
Module not found: Error: Can't resolve 'echarts' in 'H:\Gitee\ad_manage_react\node_modules\echarts-for-react\esm'
```

```
yarn add echarts
```

```
yarn add echarts-for-react
```

```
import React from 'react';
import ReactECharts from 'echarts-for-react';
const options = {
    grid: { top: 8, right: 8, bottom: 24, left: 36 },
    xAxis: {
      type: 'category',
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    },
    yAxis: {
      type: 'value',
    },
    series: [
      {
        data: [820, 932, 901, 934, 1290, 1330, 1320],
        type: 'line',
        smooth: true,
      },
    ],
    tooltip: {
      trigger: 'axis',
    },
};


<ReactECharts option={options} />
```

#### 工具栏组件

##### toolbox



#### echart图表生成表格

toolbox---features---dataView

[将echarts的数据视图装换为table表格,并且导出excel](https://zhuanlan.zhihu.com/p/375435811)

[将ECHARTS的数据视图展示为TABLE并且导出EXCEL](https://www.freesion.com/article/1308912177/)

##### 一、使用工具栏的方法

工具栏生成表格的设置，在`toolbox->feature->dataView`中设置

```
const options = {
    xAxis: {
      type: 'category',
      name: '日期',
      key: 'date',
      data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
    },
    yAxis: {
      type: 'value',
    },
    legend: {
      data: ['自然量', '推广量']
    },
    grid: {
      left: '3%',
      right: '4%',
      bottom: '3%',
      containLabel: true
    },
    series: [
      {
        name: '自然量',
        key: 'nature',
        type: 'line',
        stack: 'Total',
        data: [120, 132, 101, 134, 90, 230, 210]
      },
      {
        name: '推广量',
        key: 'spread',
        type: 'line',
        stack: 'Total',
        data: [220, 182, 191, 234, 290, 330, 310]
      },
    ],
    tooltip: {
      trigger: 'axis',
    },
    toolbox: {
      feature: {
        dataView: {
          show: true,
          readOnly: false,
          lang: ['', '关闭', '刷新'],
          optionToContent: function(opt) {
            var axisData = opt.xAxis[0].data;
            var series = opt.series;
            var table = '<table class="chart-table" style="width:100%;text-align:center" border="1">'+
                      '<thead><tr>'
                        + '<th>时间</th>'
                        + '<th>时间</th>'
                        + '<th>时间</th>'
                      +'</thead></tr>'
                       + '<tbody>';
            for (var i = 0, l = axisData.length; i < l; i++) {
                table += '<tr>'
                         + '<td>' + axisData[i] + '</td>'
                         + '<td>' + series[0].data[i] + '</td>'
                         + '<td>' + series[0].data[i] + '</td>'
                         + '</tr>';
            }
            table += '</tbody></table>';
            return table;
          }
        },
      }
    },
};
```

```
const onChartReadyCallback = (echarts) =>{
    myLineChart = echarts;
}

<ReactECharts option={options} onChartReady={onChartReadyCallback}/>
```

##### 二、自定义表格的方法

需要设置toolbox属性

缺点：表头的固定不好设置

设置dataView为不可见

```
.....

feature: {
   dataView: {
      show: true
   }
}
......

let myLineChart = '';
const onChartReadyCallback = (echarts) =>{
    myLineChart = echarts;
}

const toggleToTable = () => {
	let opt = myLineChart.getOption();
	var tbHtml = opt.toolbox[0].feature.dataView.optionToContent(opt);
	
	// 然后将生成的HTML填充到对应的节点
}


<div onClick={toggleToTable}>生成表格</div>
```

##### 三、使用antd生成表格

注：

1. 主要是处理`columns`和`dataSource`数据
2. 不需要设置toolbox属性



#### [legend](https://echarts.apache.org/zh/option.html#legend)

图例组件展现了不同系列的标记(symbol)，颜色和名字

```
legend: {
  data: ['自然量', '推广量']
},
```

#### [grid](https://echarts.apache.org/zh/option.html#grid)

设置这个位置，可以让legend显示在图表上方位置，而不是覆盖在图表上

直角坐标系内绘图网格

```
grid: {
    left: '3%',
    right: '4%',
    bottom: '3%',
    containLabel: true  //grid 区域是否包含坐标轴的刻度标签。
},
```

#### [折叠图叠加](https://echarts.apache.org/examples/zh/editor.html?c=line-stack)

##### series

```
{
    name: '自然量',
    type: 'line',
    stack: 'Total',
    data: [120, 132, 101, 134, 90, 230, 210]
},
{
    name: '推广量',
    type: 'line',
    stack: 'Total',
    data: [220, 182, 191, 234, 290, 330, 310]
},
```

#### [echart添加横向滚动条](https://www.cnblogs.com/-flq/p/9639331.html)

##### [dataZoom](https://echarts.apache.org/zh/option.html#dataZoom)

```
dataZoom: [
  {
    type: 'slider',
    show: true,
    xAxisIndex: [0],
  }
],
```



#### 左侧导航栏-新版本的使用

```
const items = [
  { label: '菜单项一', key: 'item-1' }, // 菜单项务必填写 key
  { label: '菜单项二', key: 'item-2' },
  {
    label: '子菜单',
    key: 'submenu',
    children: [{ label: '子菜单项', key: 'submenu-item-1' }],
  },
];
return <Menu items={items} />;
```

##### [加上页面跳转](https://ant.design/components/menu-cn/)

```
{
    label: (
      <a href="https://ant.design" target="_blank" rel="noopener noreferrer">
        Navigation Four - Link
      </a>
    ),
    key: 'alipay',
},
```

##### 项目中-加上页面跳转的做法

```
import { Link } from 'react-router-dom';

{
    label: ( <Link to="/product">全部产品</Link>),
    key:'/product',
    icon: <AppstoreOutlined />
},
```

#### Menu新版本—左侧导航栏完整代码

1. 左侧导航menus

   ```
   import { 
       AppstoreOutlined,
       ToolOutlined, 
       MacCommandOutlined,
       FolderOpenOutlined, 
       DashboardOutlined,
       PieChartOutlined,
       SettingOutlined }
   from '@ant-design/icons';
   import { Link } from 'react-router-dom';
   
   const leftMenus = [
       {
           // label: '全部产品',
           label: ( <Link to="/product">全部产品</Link>),
           key:'/product',
           icon: <AppstoreOutlined />
       },
       {
           // label: '素材管理',
           label: ( <Link to="/source">素材管理</Link>),
           key:'/source',
           icon: <FolderOpenOutlined />
       },
       {
           label: '公共模块',
           key:'/ad',
           icon: <MacCommandOutlined />,
           children: [
               {
                   // label: '权限管理',
                   label: ( <Link to="/ad/account">权限管理</Link>),
                   key:'/ad/account',
                   icon: ''
               },
               {
                   // label: '用户管理',
                   label: ( <Link to="/ad/user">用户管理</Link>),
                   key:'/ad/user',
                   icon: ''
               },
               {
                   // label: '账户管理',
                   label: ( <Link to="/ad/agent">账户管理</Link>),
                   key:'/ad/agent',
                   icon: ''
               },
               {
                   // label: '项目管理',
                   label: ( <Link to="/ad/group">项目管理</Link>),
                   key:'/ad/group',
                   icon: ''
               },
               {
                   // label: '渠道管理',
                   label: ( <Link to="/ad/channel">渠道管理</Link>),
                   key:'/ad/channel',
                   icon: ''
               },
               {
                   // label: '设备管理',
                   label: ( <Link to="/ad/device">设备管理</Link>),
                   key:'/ad/device',
                   icon: ''
               },
               {
                   // label: '推广参数设置',
                   label: ( <Link to="/ad/config">推广参数设置</Link>),
                   key:'/ad/config',
                   icon: ''
               },
           ]
       },
       {
           key:'/dashboard',
           label: '仪表盘',
           icon: <DashboardOutlined />,
           children: [
               {
                   // label: '总览',
                   label: ( <Link to="/dashboard/overview">总览</Link>),
                   key:'/dashboard/overview',
                   icon: ''
               },
               {
                   // label: '实时',
                   label: ( <Link to="/dashboard/realtime">实时</Link>),
                   key:'/dashboard/realtime',
                   icon: ''
               },
               {
                   // label: '渠道效果对比',
                   label: ( <Link to="/dashboard/channeleffect">渠道效果对比</Link>),
                   key:'/dashboard/channeleffect',
                   icon: ''
               },
           ]
       },
       {
           key:'/collect',
           label: '报表',
           icon: <PieChartOutlined />,
           children: [
               {
                   // label: '分包推广详情',
                   label: ( <Link to="/collect/subpackage">分包推广详情</Link>),
                   key:'/collect/subpackage',
                   icon: ''
               },
               {
                   // label: 'SEM活动详情',
                   label: ( <Link to="/collect/sem">SEM活动详情</Link>),
                   key:'/collect/sem',
                   icon: ''
               },
               {
                   // label: '激活延迟分析',
                   label: ( <Link to="/collect/effectevaluate">激活延迟分析</Link>),
                   key:'/collect/effectevaluate',
                   icon: ''
               },
           ]
       },
       {
           key:'/tool',
           label: '工具',
           icon: <ToolOutlined />,
           children: [
               {
                   // label: '归因查询',
                   label: ( <Link to="/tool/attribute">归因查询</Link>),
                   key:'/tool/attribute',
                   icon: ''
               },
               {
                   // label: '日志流',
                   label: ( <Link to="/tool/logtool">日志流</Link>),
                   key:'/tool/logtool',
                   icon: ''
               },
           ]
       },
       {
           key:'/manage',
           label: '配置',
           icon: <SettingOutlined />,
           children: [
               {
                   // label: '推广回调管理',
                   label: ( <Link to="/manage/datacb">推广回调管理</Link>),
                   key:'/manage/datacb',
                   icon: ''
               },
               {
                   // label: '埋点管理',
                   label: ( <Link to="/manage/customevent">埋点管理</Link>),
                   key:'/manage/customevent',
                   icon: ''
               },
           ]
       },
   ]
   
   export default leftMenus;
   ```

2. 左侧导航-组件

   ```
   import React, {useState, useEffect} from 'react'
   import { Layout, Menu } from 'antd';
   import { useLocation } from 'react-router-dom';
   
   import leftMenus from '../app/leftMenus';
   import { 
       MenuUnfoldOutlined,
       MenuFoldOutlined,
       }
   from '@ant-design/icons';
   
   const { Sider } = Layout;
   // const { SubMenu } = Menu;
   
   // 左侧导航栏
   export default function LeftNav(props) {
     const location = useLocation();
     const pathname = location.pathname;
     const [selectedKeys, setSelectedKeys] = useState([]);
     const [openKeys, setOpenKeys] = useState([]);
    
     useEffect(() => {
       // 更新选中状态
       
       const rank = pathname.split('/');
       switch(rank.length) {
         case 2 :
           setSelectedKeys([pathname])
           break;
         
         case 3: 
           setSelectedKeys([pathname])
           setOpenKeys([rank.slice(0, 2).join('/')])
           break;
     
         case 4: 
           setSelectedKeys([pathname])
           setOpenKeys([rank.slice(0, 2).join('/'), rank.slice(0, 3).join('/')])
           break;
         default:
           setSelectedKeys([]);
           setOpenKeys([]);
   
       }
     },[pathname]);
   
     // 展开/收起SubMenu触发
     const onOpenChange = keys => {
       setOpenKeys(keys)
     };
   
     // 点击MenuItem时触发
     const onClick = e => {
       setSelectedKeys([e.key])
     }
     return (
       <Sider 
           trigger={null} 
           collapsible 
           collapsed={props.isCollapsed}
           collapsedWidth="60"
           className='left-sider'
           style={{
               overflow: 'auto',
               height: '100vh',
               position: 'fixed',
               left: 0,
               top: 0,
               bottom: 0,
             }}
       >
       <div className="logo">
           <span 
               className='toggleFold' 
               onClick={props.onToggle}
           >
               { props.isCollapsed ? <MenuUnfoldOutlined/> :  <MenuFoldOutlined/>}
           </span>
       </div>
           <Menu
             items={leftMenus} 
             theme="dark"
             mode="inline" 
             openKeys={openKeys}
             selectedKeys={selectedKeys}
             onOpenChange={onOpenChange}
             onClick={onClick}
             defaultSelectedKeys={[selectedKeys]}
           />
       </Sider>
     )
   }
   ```

   

