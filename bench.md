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