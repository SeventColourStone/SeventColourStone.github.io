# 代码生成器


## 单表

单表默认后端代码是生成在`admin`应用下，前端代码是生成在`adminUi`应用下，对应的项目基目录是`app/admin`以及`app/adminUi`


单表代码生成器需要传入表名`$table_name`，可选传入`$app` ,`$module`,默认`$app=admin`,`$module='bussiness'`。

如按默认提供表名则会在特定位置下生成对应的代码：
当您需要使用代码生成器生成的表为`$table_name=test_info`,
则生成的对应目录树如下：

### 目录树

```
├───app
│   │───admin
│   │   │───controller
│   │   │   └───api
│   │   │       └───business
│   │   │           └───TestInfoController.php //控制器
│   │   │───service
│   │   │   └───business
│   │   │       └───TestInfoService.php    //服务层       
│   │   │───mapper
│   │   │   └───business
│   │   │       └───TestInfoMapper.php  //mapper
│   │   │───model
│   │   │   └───business
│   │   │       └───TestInfo.php  //model
│   │   │───validate
│   │   │   └───business
│   │   │       └───TestInfoValidate.php   //验证器层
│   │   │
│   │───adminUi
│   │   │───controller
│   │   │   └───business
│   │   │       └───TestInfoController.php   //前端控制器，仅做html的下发
│   │   │           
│   │   │───view
│   │   │   └───business
│   │   │       └───testInfo
│   │   │           └───index.html   //前端列表视图层        
│   │   │           └───edit.html    //前端编辑视图层       
│   │   │           └───add.html     //前端添加视图层      
│   │   │
│   │   │
│   │   │

```


传入的`module`可以使用 `. / \ ` 分割，系统兼容多种方式输入

如：`$module = "bussiness.test"` 会自动转换为路径 `bussiness/test`,
对应在项目基目录下的路径则是`app/admin/controller/api/business`，其他类推。



## 接口规范

stoneAdmin 维护一套半前后端分离的admin前端可视化，为何是半，因为只是用后端做一组action的渲染html，剩下的全部交与 layui+layer做展示。
这意味着可以无缝的调整成或vue、或react等前后端分离的开发方案，您可以按需的选用。

> 之后会推出前后端的分离方案，未完待续。



对应生成的前端访问接口 url
会对路由做容错处理，支持小驼峰，下划线，中划线路由访问
```
/ui/dis/sss/sdsd/testInfo/index
/ui/dis/sss/sdsd/test_info/index
/ui/dis/sss/sdsd/test-info/index


/ui/dis/sss/sdsd/testInfo/add
/ui/dis/sss/sdsd/test_info/add
/ui/dis/sss/sdsd/test-info/add


/ui/dis/sss/sdsd/testInfo/edit
/ui/dis/sss/sdsd/test_info/edit
/ui/dis/sss/sdsd/test-info/edit
```

 




默认存在固定的接口

- index (列表)
- recycle (回收站列表)
- save (新增)
- read (读取)
- update (更新)
- delete (单个或批量加入回收站)
- realDelete (单个或批量真实删除用户 （清空回收站）)
- recovery (单个或批量恢复在回收站的用户)



### index 接口




可传请求参数select，默认会过滤表内不存在的字段名，您也可使用 `field_name as new_field_name` 重定义字段名

