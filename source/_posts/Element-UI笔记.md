---
title: Element-UI笔记
date: 2021-05-13 11:36:28
tags: Element-UI
---

#### 安装

```javascript
cnpm i element-ui -S
```

#### 引入element-ui

在 main.js 中写入以下内容（完整引入）：

```javascript
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

#### ElementUI表格合并单元格

摘抄自[博客](https://www.cnblogs.com/yuwenjing0727/p/10110721.html)，仅用于学习。

<table>
  <tr>
    <th>序号</th>
    <th>工单类型</th>
    <th>taskKey</th>
    <th>templateUrl</th>
    <th>操作</th>
  </tr>
  <tr>
    <td rowspan="3">1</td>
    <td rowspan="3">事件单</td>
    <td>shijian_01</td>
    <td>/shijian_01</td>
    <td>编辑   删除</td>
  </tr>
  <tr>
    <td>shijian_02</td>
    <td>/shijian_02</td>
    <td>编辑   删除</td>
  </tr>
  <tr>
    <td>shijian_03</td>
    <td>/shijian_03</td>
    <td>编辑   删除</td>
  </tr>
  <tr>
    <td rowspan="3">2</td>
    <td rowspan="3">问题单</td>
    <td>shijian_04</td>
    <td>/shijian_04</td>
    <td>编辑   删除</td>
  </tr>
  <tr>
    <td>shijian_05</td>
    <td>/shijian_05</td>
    <td>编辑   删除</td>
  </tr>
  <tr>
    <td>shijian_06</td>
    <td>/shijian_06</td>
    <td>编辑   删除</td>
  </tr>
</table>


代码附上：

```
<template>
  <div class="">
    <el-table
        :data="listData"
        :span-method="objectSpanMethod"
        class="tableArea"
        style="width: 100%">
        <el-table-column
          prop="type"
          label="序号"
          align="center"
          width="200"/>
        <el-table-column
          prop="sheetType"
          label="工单类型"
          />
        <el-table-column
          prop="taskKey"
          label="taskKey"
          />
        <el-table-column
          prop="templateUrl"
          label="templateUrl"
          />
        <el-table-column
          label="操作"
          >
          <template slot-scope="scope">
              <el-tooltip class="item" effect="dark" content="修改" placement="top-start">
                      <i class="el-icon-edit-outline"  @click="modify(scope)" />
                    </el-tooltip>
                    <el-tooltip class="item" effect="dark" content="删除" placement="top-start">
            <i class="el-icon-delete" @click="deleteData(scope)" />
                    </el-tooltip>
          </template>
        </el-table-column >
      </el-table>
  </div>
</template>
<script>

export default {
  name: 'myNeedDeal',
  data() {
    return {
      rowList: [],
      spanArr: [],
      position: 0,
      listData: []
    }
  },

  methods: {
      queryData(){//查询操作
          this.listData = [
              {
            id:1,
          type:1,
          sheetType: "事件单",
          taskKey: "shijian_01",
          templateUrl: "/shijian_01"
        },
        {
            id:2,
          type:1,
          sheetType: "事件单",
          taskKey: "shijian_02",
          templateUrl: "/shijian_02"
        },
        {
            id:3,
          type:1,
          sheetType: "事件单",
          taskKey: "shijian_03",
          templateUrl: "/shijian_04"
        },
        {
            id:4,
          type:2,
          sheetType: "问题单",
          taskKey: "wenti_01",
          templateUrl: "/wenti_01"
        },
        {
            id:5,
          type:2,
          sheetType: "问题单",
          taskKey: "wenti_02",
          templateUrl: "/wenti_02"
        },
        {
            id:6,
          type:2,
          sheetType: "问题单",
          taskKey: "wenti_03",
          templateUrl: "/wenti_03"
        }
          ];
          this.rowspan()
      },
      rowspan() {
          this.listData.forEach((item,index) => {
            if( index === 0){
                this.spanArr.push(1);
                this.position = 0;
            }else{
                if(this.listData[index].type === this.listData[index-1].type ){
                    this.spanArr[this.position] += 1;
                    this.spanArr.push(0);
                }else{
                    this.spanArr.push(1);
                    this.position = index;
                }
            }
        })
      },
    objectSpanMethod({ row, column, rowIndex, columnIndex }) {  //表格合并行
        if (columnIndex === 0) {
            const _row = this.spanArr[rowIndex];
            const _col = _row>0 ? 1 : 0;
            return {
                rowspan: _row,
                colspan: _col
            }
        }
        if(columnIndex === 1){
            const _row = this.spanArr[rowIndex];
            const _col = _row>0 ? 1 : 0;
            return {
                rowspan: _row,
                colspan: _col
            }
        }
    }
  },
  mounted() {
    this.queryData();
  }
}
</script>
<style lang="scss" scoped>
.el-select {
  margin-right: 15px;
}
.el-input {
  margin-right: 15px;
  width: 200px;
}
.tableArea {
  margin-top: 20px;
  box-shadow: 0 0 8px 0 #aaa;
}
i[class^="el-icon"] {
  margin-right: 5px;
  font-size: 16px;
  cursor: pointer;
}
.modify_table{
    td{
        padding: 10px ;
    }
}
.item_title{
    text-align: right;
}
</style>
```

详细说明：

```
:span-method="objectSpanMethod"  
```

这个是官方给定的绑定属性和对应的方法，objectSpanMethod 传入了 { row, column, rowIndex, columnIndex }

row: 当前行

column: 当前列

rowIndex：当前行号

columnIndex ：当前列号

该函数可以返回一个包含两个元素的数组，第一个元素代表`rowspan`，第二个元素代表`colspan`。 也可以返回一个键名为`rowspan`和`colspan`的对象。

```
this.spanArr 数组 ，返回的是相对应的行合并行数
```

这个示例打印出的this.spanArr为 [3, 0, 0, 3, 0, 0]，比如，第一个元素为3，表示第一行应该向下合并3行（即第一行的rowspan为3），第二个元素的rowspan为0，就让它“消失”。

```
rowspan（）这个函数就是用来返回 this.spanArr 数组的，定义每一行的 rowspan
```

rowspan（）函数，if( index === 0)，第一行，直接先给数组push进一个1，表示自己先占一行，this.position是数组元素的位置（此时是从数组元素的第一个开始，所以this.position为0）， this.position为0意思表示的就是数组的第一个元素。

当到了index为2的时候，if(this.listData[index].type === this.listData[index-1].type )，让第二行与第一行作比较，

如果第二行与第一行相等的话，this.position就+1，当有n行第一行相同，this.position就为n，表示向下合并n行；第二行自己就this.spanArr.push(0)，表示第二行“消失”，因为第一行和第二行合并了啊。

如果第二行与第一行不相等的话，那么this.spanArr.push(1);就让第二行自己独占一行；this.position = index意思就是把指针拿到index这行来，表示设置数组this.spanArr[this.position]的元素值，然后定义从此行开始向下合并几行（可能这句话我表述的不是很清楚你可以根据我这个示例研究下，当index为3时，this.position为3，当index为4时，第四行与第三行需要合并，那么在数组的this.position元素就要+1了，也就是this.spanArr[this.position] += 1）

还有最后一句话

```
const _col = _row>0 ? 1 : 0;
```

定义的这一个单元格列的合并，我们项目只合并行，不合并列；

_row：代表合并行的行数，_row的值要么是1，或者更大的自然正整数，要么是0。

1代表：独占一行

更大的自然数：代表合并了若干行

0：代表“消失”的哪那一个单元格，后面的单元格向前推一格



注意：如果配合分页一起渲染数据，要在rowspan函数中，先将this.spanArr清空数组。不添加，点分页加载数据会导致表格错乱。

```
rowspan() {
    this.spanArr=[];
    .......
},
```



[elementui表格动态数据单元格合并](https://blog.csdn.net/weixin_33982670/article/details/91446060)

[elementUI table合并相同数据的单元格](https://www.imooc.com/wenda/detail/522127)

[elementUI table表格动态合并](https://segmentfault.com/a/1190000019176628)



### slot的使用

##### slots

| 事件名称 | 说明     |
| -------- | -------- |
| title    | 标题内容 |
| content  | 内容     |

```javascript
<el-page-header @back="goBack" content="管理">
  <div slot="title">修改标题</div>
	<div slot="content">修改内容</div>
</el-page-header>
```

#### [解决引用Element UI 导致弹出多个message消息提示的问题](https://www.cnblogs.com/cndarren/p/14691315.html)

#### [改造elementui的穿梭框，让他直接点击选项就穿梭到另一个框](https://blog.csdn.net/yangmiemie120/article/details/100736154)



#### [element-ui change事件传值](https://blog.csdn.net/qq_15601471/article/details/89048951)

```javascript
@change="handleSelect($event)"

handleSelect(event) {
  console.log(event)
},
```

#### [vue使用elementUI表单的获取select,checkbox的value值](https://blog.csdn.net/weixin_43834855/article/details/108817517)

```javascript
 <el-checkbox
  v-for="game in gameData"
  :label="game.id"
  :key="game.id"
  :data-id="game.id"
  :data-group="game.group_id">
  {{game.name}}</el-checkbox>

// 把想要的value值放在label中，将需要显示的内容放在 <el-checkbox>标签之间
<el-checkbox :label="想要获取的value值">{{显示的内容值}}</el-checkbox>
```

checkbox的获取可以通过label来获得，将原来的label写在<el-checkbox>{名称}</>中，因为elementUI获取绑定的是label，
即<el-checkbox label=[value]>[label]</>



事件传多参数

```javascript
<ul class="ul-list txt-left">
  <li
    v-for="(game, index) in checkedData"
    :label="game.id"
    :key="game.id"
     @click="chooseGame(index, game.id)"
    :class = "isactive == index ? 'blue-txt' : '' " 
    class="active">
    {{game.name}}</li>
</ul>

isactive: 0,
  
chooseGame(index, id) {
  this.isactive = index
  this.thisGameChannels = this.allGameChannels[id]
},
```

### [Element ui el-row el-col里面高度不一致的问题](https://blog.csdn.net/sinat_33255495/article/details/114366877)

```javascript
<el-row type="flex">
  <el-col>
	<textarea autocomplete="off" class="el-textarea__inner" style="min-height: 33.2333px;"></textarea>
 </el-col>
  <el-col>test<br>test</el-col>
</el-row>
```

用饿了吗el-row，el-col布局页面的时候会因为el-col的内容高度不统一，造成布局混乱，解决方案就是在el-row中添加type="flex"。

注意：里面的内容要有设定的高度，不然加上flex也无效。