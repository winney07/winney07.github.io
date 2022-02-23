---
title: Element-UI笔记
date: 2021-05-13 11:36:28
tags: Element-UI
---

#### elementUI表格合并单元格

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