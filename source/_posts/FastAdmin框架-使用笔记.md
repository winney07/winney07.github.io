---
title: FastAdmin框架-使用笔记
date: 2020-07-24 19:25:00
tags:
- FastAdmin框架
categories: 
- 工作笔记
- FastAdmin框架
---

### 在FastAdmin动态追加bootstrap-select下拉列表
{% asset_img css1.png %}
```
<select data-rule="required" class="form-control selectpicker" data-live-search="true" name="row[admin_role_name]" data-url="" data-query-name=""> </select>

注：data-live-search="true"是添加可以模糊搜索功能
```

关键代码：
```
define(['jquery', 'bootstrap', 'backend', 'table', 'form'], function ($, undefined, Backend, Table, Form) {
    var Controller = {
      ......
      ......
      add: function () {
            //关键代码：（要引入）
            require(['bootstrap-select', 'bootstrap-select-lang']);

            //渲染下拉框
            var renderselect = function (select, data, defaultOpt) {
                if(defaultOpt && data.length>0) {
                    var opt = '<option value="">' + defaultOpt + '</option>';
                }
                var html = [opt] || [];
                for (var i = 0; i < data.length; i++) {
                    html.push("<option value='" + data[i] + "'>" + data[i] + "</option>");
                }
                $(select).html(html.join(""));
                $(".selectpicker").selectpicker('refresh');
                return select;
            };

           $("select[name='row[server_id]']").change(function () {
                var admin_id = $("select[name='row[admin_id]']").val();
                var app_id = $("select[name='row[app_id]']").val();
                var server_id = $("select[name='row[server_id]']").val();

                $.ajax({
                    url: '/admin/boon/resource/role_name_lise',
                    data: {admin_id: admin_id, app_id: app_id, server_id: server_id},
                    type: 'get',
                    dataType: 'json',
                    success: function (data, textStatus, xhr) {
                        var list = data.data.list;

                        renderselect($("select[name='row[admin_role_name]']"), list, "请选择测试角色名");
                        renderselect($("select[name='row[player_role_name]']"), list, "请选择玩家角色名");
                    }
                });
           });
            
           $("select[name='row[admin_id]'], select[name='row[app_id]']").change(function () {
               console.log("dianji")
               var list = [];
                renderselect($("select[name='row[admin_role_name]']"), list);
                renderselect($("select[name='row[player_role_name]']"), list);
           }); 
      });
    }
```
