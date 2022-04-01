# 快速开始


```bash
git clone git@github.com:SeventColourStone/StoneAdmin.git

```

## 初始化项目

* 创建mysql 数据库 stone
* 导入项目目录下`sql/stone.sql`文件，`config/database.php` 下配置数据库账密
* 项目强依赖redis，您需要在 `config/redis.php` 配置 redis 账密


# 启动

## window系统开发
```phpregexp
//支持文件热更新，您可以自定义文件后缀后再windows.php文件内修改侦听的文件后缀名，如您使用其他的模板引擎
php windows.php

```

## linux系统
```phpregexp
//开发环境
php start.php

//生产发布后台常驻
php start.php start -d
```


# 其他

> 未完待续