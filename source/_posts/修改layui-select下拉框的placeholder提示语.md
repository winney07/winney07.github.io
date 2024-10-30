---
title: 修改layui-select下拉框的placeholder提示语
date: 2019-09-14 15:45:23
tags:
- CSS
categories: 
- CSS
---
### 使用option

HTML：

```
<div class="layui-form-item">
    <label class="layui-form-label">账号：</label>
    <div class="layui-input-block">
        <select name="account" lay-filter="account">
            <option value="">请选择账号</option>
        </select>
    </div>
</div>
```

> `<option value="">请选择账号</option>` ，value值为空

如图所示：

![使用option加上placeholder.png (395×188) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/blog/layui-select/使用option加上placeholder.png)

### 使用定位元素模拟placeholder

> ”所属项目“默认不选择。”账号“下拉框的数据，是根据所选的”所属项目“进行动态渲染。
>
> 因”所属项目“默认不选择，”账号“初始化时没有下拉框列表数据。需求还要求不显示可选项，也就是`<option value="">请选择账号</option>` 也不显示。

```
<div class="layui-form-item">
    <label class="layui-form-label">账号：</label>
    <div class="layui-input-block">
        <select name="account" lay-filter="account">
        </select>
    </div>
</div>
```

1. 如果不加option选项，下拉框默认样式如下图所示：

   ![select框没有选项时初始化样子.png (389×180) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/blog/layui-select/select框没有选项时初始化样子.png)

   > 项目中使用的是layui是`v2.5.6 `版本。而更换版本，可能会带来其他影响，而且layui也停更了。

2. 所以使用定位元素覆盖掉默认的`placeholder`

   HTML:

   ```
   <div class="layui-form-item">
       <label class="layui-form-label">账号：</label>
       <div class="layui-input-block" id="account-select">
           <div class="account-placeholder">请选择账号</div>
           <select name="account" lay-filter="account"></select>
       </div>
   </div>
   ```

   CSS：

   ```
   #account-select{
       position: relative;
   }
   #account-select .account-placeholder {
       position: absolute;
       left: 3px;
       top: 3px;
       z-index: 10;
       padding-left: 8px;
       height: 32px;
       line-height: 32px;
       width: 184px;
       pointer-events: none;
       color: rgb(117, 117, 117);
       background-color: #fff;
   }
   ```

   ![定位元素模拟placeholder0.png (390×214) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/blog/layui-select/定位元素模拟placeholder0.png)

   ![定位元素模拟placeholder.png (376×389) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/blog/layui-select/定位元素模拟placeholder.png)

3. `select`框初始化时设置为`disabled`

   > 如上图所示，使用了定位元素挡住了默认的placeholder，但是还是会显示”没有选项“这一项。
   >
   > 所以干脆初始化时，将`select`框初始化时设置为`disabled`

   HTML：

   ```
   <div class="layui-form-item">
       <label class="layui-form-label">账号：</label>
       <div class="layui-input-block" id="account-select">
           <div class="account-placeholder">请选择账号</div>
           <select name="account" lay-filter="account" disabled></select>
       </div>
   </div>
   ```

#### 其他细节处理

1. 点击下拉框时，弹出”需要选择所属项目“的提示语

   ```
   // 点击账号下拉框
   layui.$("#account-select").on('click', '.layui-form-select', function(){
       var project = layui.$('[name="project"]:checked').val();
       if(!project) {
           layer.msg('需选择所属项目', {time: 1000});
       }
   })
   ```

2. 向下箭头为禁用的样式，修改为正常样式：

   ```
   #account-select .layui-select-disabled .layui-edge{
       border-top-color: #c2c2c2;
   }
   ```

3. 鼠标放在select框上，是禁止图标，然而鼠标移到下拉框的向下箭头，光标显示为小手；

   如图所示：

   ![鼠标移到下拉框的向下箭头-显示小手.png (339×129) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/blog/layui-select/鼠标移到下拉框的向下箭头-显示小手.png)

   解决：

   ```
   #account-select .layui-select-disabled .layui-edge{
       cursor: not-allowed;
   }
   ```

4. 选择”所属项目“时，追加对应的数据，同时需要去除`select`框的`disabled`属性，以及隐藏模拟`placeholder`的定位元素

   ```
   // 渲染 select 框的数据
    function renderSelectData(dataList) {
       var selectElem = layui.$('select[name="account"]');
       selectElem.empty(); // 清空原有选项
       selectElem.append('<option value="">请选择账号</option>');
   
       // 添加新的选项
       layui.$.each(dataList, function(index, item) {
           var optionElem = layui.$('<option>');
           optionElem.val(item.value);
           optionElem.text(item.name);
           selectElem.append(optionElem);
       });
   
       layui.form.render('select'); // 重新渲染 select 框
   }
   var accountList = {
       "1": [
           { value: 1, name: '项目AAA_account1'},
           { value: 2, name: '项目AAA_account2'},
           { value: 3, name: '项目AAA_account3'},
       ],
       "2": [
           { value: 4, name: '项目BBB_account1'},
           { value: 5, name: '项目BBB_account2'},
       ]
   }
   // 监听单选框
   form.on('radio(project)', function(data){
       // 渲染账号下拉列表
       renderSelectData(accountList[data.value]);
   
       layui.$('select[name="account"]').removeAttr('disabled');
       form.render('select');
       layui.$('.account-placeholder').hide();	// 隐藏模拟的placeholder
   });
   ```

   最终效果：

   ![鼠标移上显示禁止图标效果.png (347×274) (raw.githubusercontent.com)](https://raw.githubusercontent.com/winney07/Images/main/blog/layui-select/鼠标移上显示禁止图标效果.png)

