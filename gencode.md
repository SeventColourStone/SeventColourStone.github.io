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
├───gencodeBackup //备份的原文件代码
│   │───app
│   │   │───admin
│   │   │───adminUi

```


传入的`module`可以使用 `. / \ ` 分割，系统兼容多种方式输入

如：`$module = "bussiness.test"` 会自动转换为路径 `bussiness/test`,
对应在项目基目录下的路径则是`app/admin/controller/api/business`，其他类推。

>生成业务代码文件时会判断当前代码内是否存在该文件，存在则会备份到项目根目录下`gencodeBackup`，并按日期如`20220327`生成文件夹，接着完整复制原文件到目标日期文件夹下，（注意：相同的文件只会拷贝最初的一次，多次调整表结构或代码生成器功能后并不会覆盖日内最初的备份代码）
>意味着您可以在当天全使用代码生成器微调生成逻辑后再根据改动业务使用代码比对工具恢复您的自定义业务改动。


## 命名规则

表注释必须，注释简洁，以名词描述最好，如使用“测试表”则会移除表字
表字段如果使用`is_*`、`status`字段则默认生成的table列表是switch组件，并可以表格内执行启停操作，
如表内存在`status`字段，代表是否启用该`row`数据，所有检索都会忽略该`row`为未启用的数据，（区别于加入回收站）您可以选择按需使用。




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

 
## 命令行运行

```

php .\webman stone:curd --table external_system_api --module test 一键生成所有的curd代码逻辑

php .\webman stone:gen   一键把基础表结构加入代码生成器，即可低代码可视化的做代码改动




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

