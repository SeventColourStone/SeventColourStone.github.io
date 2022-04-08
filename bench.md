# 性能压测

## 无db读写操作 

纯 hello world输出 测试
- 环境：
- CPU AMD 3600是6核12芯
- 内存 3200频率8G*2
- PHP 8.1.4（x64）
- tp6
- 运行命令 php think run
- 测试命令 `ab -c 10 -n 100 http://127.0.0.1:8000/`
- 多次 平均55 最高60


- webman 1.3.4
- 运行命令 php start.php start
- 测试命令 `ab -c 10 -n 100 http://127.0.0.1:8000/` 
- 多次 平均6K多


> 无数据库操作：webmann性能是tp6的120倍

## 数据库读操作

> 数据库单条find查询：webman+illuminate/database 是tp6的80倍
就算不做缓存，不优化数据库，配置稍微好点的云端mysql也能满足基本业务了。
纯文字输出的rps平均值，TP6是50+ | tp6+worker插件是1k慢降到120|webman是6k
链接数据库单条有索引find主键的rps tp6是50+ | webman是4k