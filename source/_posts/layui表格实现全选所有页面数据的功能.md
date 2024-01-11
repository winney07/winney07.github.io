---
title: layui表格实现全选所有页面数据的功能
date: 2022-08-10 11:21:22
tags:
- layui
categories: 
- layui
---

### layui表格中的复选框

在实现全选所有页面的数据之前，先看一下layui表格中的复选框能实现的功能。

HTML：

```
<table id="testTable" lay-filter="testTable"></table>
```

JavaScript：

```
layui.use(['table', 'jquery', 'form'], function () {
    var table = layui.table
        , form = layui.form
        , $ = layui.jquery
        , list = []
        , selectedIds = [];     // 存放已选中行的id数组

    function getRandomName() {
        var letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
        var name = '';
        for (var i = 0; i < 5; i++) {
            name += letters.charAt(Math.floor(Math.random() * letters.length));
        }
        return name;
    }

    for (var i = 1; i <= 100; i++) {
        list.push({ id: i, name: getRandomName(), score: Math.floor(Math.random() * 1000) + 1 });
    }


    table.render({
        elem: '#testTable'
        , data: list
        , page: true    // 开启分页
        , limit: 10
        , cols: [[
            // { checkbox: true }
            { type:'checkbox' }
            , { field: 'id', title: 'ID' }
            , { field: 'name', title: '用户名' }
            , { field: 'score', title: '评分' }
        ]]
        , done: function (res) {
            // console.log(res);
        }
    });


    // 监听table复选框的选择事件
    table.on('checkbox(testTable)', function (obj) {
        // console.log(obj);           // 当前行的一些常用操作集合
        // console.log(obj.checked);   // 当前是否选中状态
        // console.log(obj.data);      // 选中行的相关数据
        // console.log(obj.type);      // 如果触发的是全选，则为：all，如果触发的是单选，则为：one

        // var selectedData;   // 选中行的相关数据
        // selectedData = table.checkStatus('testTable').data;
        // selectedIds = selectedData.map(item => item.id);
        // // 进行排序
        // selectedIds.sort(function (a, b) {
        //     return a - b;
        // });

        selectedIds = table.checkStatus('testTable').data.map(item => item.id).sort(function (a, b) {
            return a - b;
        });   

        console.log('selectedIds');
        console.log(selectedIds);

    });

});
```

在表格中，添加复选框：在`cols`中添加`{ checkbox: true }`或`{ type:'checkbox' }`

获取选中行的数据：`table.checkStatus('testTable').data;`

> 这里使用sort，是为了方便看数据，如果没有这个要求，可以不加。

![layui-table-checkbox1.png (1216×508) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/layui-笔记/layui-table-checkbox1.png)

![layui-table-checkbox2.png (1117×506) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/winney07.github.io/layui-笔记/layui-table-checkbox2.png)

> 如果需求中，按表头的复选框进行全选的时候需要获取到所有页面的数据。根据上面的展示，layui表格中默认的复选框的全选，获取不到所有页面的数据。

### layui表格中表头的复选框实现全选所有页面的数据-多次操作

完整代码：

```
layui.use(['table', 'jquery', 'form'], function () {
    var table = layui.table
        , form = layui.form
        , $ = layui.jquery
        , list = []
        , temp = []     // 当前页的数据
        , selectedIds = [];     // 存放已选中行的id数组

    function getRandomName() {
        var letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
        var name = '';
        for (var i = 0; i < 5; i++) {
            name += letters.charAt(Math.floor(Math.random() * letters.length));
        }
        return name;
    }

    for (var i = 1; i <= 100; i++) {
        list.push({ id: i, name: getRandomName(), score: Math.floor(Math.random() * 1000) + 1 });
    }

    table.render({
        elem: '#testTable'
        , data: list
        , page: true //开启分页
        , limit: 10
        , cols: [[
            { checkbox: true }
            , { field: 'id', title: 'ID' }
            , { field: 'name', title: '用户名' }
            , { field: 'score', title: '评分' }
        ]]
        , done: function (res) {
            // 切换页面时，获取当前页的数据
            temp = res.data.map(function (item) {
                return item.id;
            })
        }
    });

    // 监听table复选框的选择事件
    table.on('checkbox(testTable)', function (obj) {
        if (obj.type === 'all') {	// 表头的全选复选框
            if (obj.checked) {	// 选中状态
                for (var i = 0; i < temp.length; i++) {
                    var valueToAdd = temp[i];
                    // 检查 arr 数组是否已经包含当前值，如果没有则追加
                    if (!selectedIds.includes(valueToAdd)) {
                        // 追加
                        selectedIds.push(valueToAdd);
                    }
                }
            } else {	// 未选中状态
                // 减去
                selectedIds = selectedIds.filter(function (item) {
                    return !temp.includes(item);
                });
            }

        } else {	// 每行上的复选框
            if (obj.checked) {	// 选中状态
                // 追加
                selectedIds.push(obj.data.id);
            } else {	// 未选中状态
                // 减去
                var index = selectedIds.indexOf(obj.data.id);
                selectedIds.splice(index, 1);
            }
        }

        // 进行排序
        selectedIds.sort(function (a, b) {
            return a - b;
        });
    });

});
```

`这里代码没有进行优化和封装，是为了大家更方便地看清它的逻辑`

`难点`：

全选时，怎么去记住不同页面中的数据，如何实现追加数据和减去数据的过程。

刚好在`done`中可以获取到渲染当前页的数据。

```
done: function (res) {
    // 切换页面时，获取当前页的数据
    temp = res.data.map(function (item) {
        return item.id;
    })
}
```

`缺点与不足`:需要每页都要点一次表头的全选复选框，不能一步到位。

### layui表格中表头的复选框实现全选所有页面的数据-一次全选

使用渲染表格时的`templet`和`title`，手动创建复选框，不使用table默认添加复选框的方法`（{ type:'checkbox' }）`添加复选框。

完整代码：

```
layui.use(['table', 'jquery', 'form'], function () {
    var table = layui.table
        , form = layui.form
        , $ = layui.jquery
        , list = []
        , selectedIds = [];     // 存放已选中行的id数组

    function getRandomName() {
        var letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz';
        var name = '';
        for (var i = 0; i < 5; i++) {
            name += letters.charAt(Math.floor(Math.random() * letters.length));
        }
        return name;
    }

    for (var i = 1; i <= 100; i++) {
        list.push({ id: i, name: getRandomName(), score: Math.floor(Math.random() * 1000) + 1 });
    }

    var adTable = {
        /* 
        * 获取表格当前页码
        * @param key：缓存中pages的key值
        * @param data：填充表格的数据数组
        * @param limit：每页显示条数
        */
        getPageCur: function(key, data, limit) {
            var cur,    // 当前页码
                obj = JSON.parse(localStorage.getItem("pages")),    // 缓存中的pages对象
                totalPage = Math.ceil(data.length/limit);   // 总页数
            // 存在缓存变量pages
            if(obj) {
                // 缓存中是否有当前表格的页码记录（没有该页码记录，重置为1）
                cur = obj[key] ? obj[key] : 1;
            } else {
                // 不存在缓存变量pages
                cur = 1;
            }
            // 总页数小于当前页码（解决表格删除最后一页最后一条数据)
            if(totalPage < cur) {
                cur = 1;
            }
            return cur;
        }
        /*
        * 设置当前表格页码
        * @param key：key值
        * @param val：value值
        */
        , setPageCur: function(key, val) {
            // 使用对象缓存，是因为有些页面有多层页面，记住多个页面的页码
            var pages = JSON.parse(localStorage.getItem("pages")) || {};  // 缓存中pages对象
            pages[key] = val;   // 设置页码
            pages = JSON.stringify(pages);  
            localStorage.setItem("pages", pages);     // 重新放到缓存中
        }
    }

    var page_curr = adTable.getPageCur("testTable", list, 10);   // 10是分页的limit值
    table.render({
        elem: '#testTable'
        , data: list
        , page: {
            curr: page_curr
            , limit: 10
        }
        , cols: [[
            {
                field: 'checkbox', title: '<input type="checkbox" id="checkAll" lay-filter="checkAll" lay-skin="primary">', width: 66, templet: function (res) {
                    return '<input type="checkbox" class="rowCheck" data-id="' + res.id + '" lay-filter="rowCheck" lay-skin="primary">';
                }
            }
            , { field: 'id', title: 'ID' }
            , { field: 'name', title: '用户名' }
            , { field: 'score', title: '评分' }

        ]]
        , done: function (res, curr, count) {
            // 重置表格的样式
            if(selectedIds.length > 0) {
                // 根据已选selectedIds集合，修改复选框的样式（表头的复选框针对所有行数据，layui框架的全选只针对当前页）
                selectedIds.map(function(item) {
                    $('.layui-table input[data-id="'+ item +'"]').prop('checked', true);
                })
                // 重新渲染
                form.render('checkbox');
            }

            // 记录当前页面
            adTable.setPageCur("testTable", curr);
        }
    });

    // 监听表格中表头全选复选框的选择事件
    form.on('checkbox(checkAll)', function (data) {
        if (!list.length) {
            $('input[lay-filter="checkAll"]').prop('checked', false);
        }
        // 是否全选
        var isAllChecked = data.elem.checked ? true : false;

        // 是否被选中
        if (isAllChecked) {
            selectedIds = list.map(function (item) {
                return item.id;
            })
        } else {
            selectedIds = [];
        }

        console.log(selectedIds);

        // 更新表格中的复选框样式
        $('.rowCheck').prop('checked', isAllChecked);
        form.render('checkbox');
    });

    // 监听表格中的复选框
    form.on('checkbox(rowCheck)', function (data) {
        var isChecked = data.elem.checked	// 是否被选中
            , isAllChecked = false		// 是否全选
            , _id = $(data.elem).data("id");// 当前项的id

        if (isChecked) {
            // 追加
            selectedIds.push(_id);
            isAllChecked = (selectedIds.length == list.length) ? true : false;
        } else {
            // 减去
            var index = selectedIds.indexOf(_id);
            selectedIds.splice(index, 1);

            isAllChecked = false;
        }
        // 进行排序
        selectedIds.sort(function (a, b) {
            return a - b;
        });

        console.log('selectedIds');
        console.log(selectedIds);

        // 更新全选复选框的样式
        $('#checkAll').prop('checked', isAllChecked);
        form.render('checkbox');

    });
});
```

`说明`：

1. 获取页面当前页码的方法`adTable.getPageCur`，大家可以根据自己的实际情况来实现。因为这里有多个表格，所以我放在pages对象中，不同的表格，根据表格名称来缓存对应的页码。

2. 难点和关键代码：

   ```
   {
       field: 'checkbox', title: '<input type="checkbox" id="checkAll" lay-filter="checkAll" lay-skin="primary">', width: 66, templet: function (res) {
           return '<input type="checkbox" class="rowCheck" data-id="' + res.id + '" lay-filter="rowCheck" lay-skin="primary">';
       }
   }
   ```

   1. `title`属性一定要配置。
   2. `.rowCheck`一定要记得配置对应的id：` data-id="' + res.id + '"`



`如果有问题，可以留言联系。`
