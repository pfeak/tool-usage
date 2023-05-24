# nc 命令使用

## 1. 命令安装

Centos: `yum install nc`

Ubuntu: `apt install netcat`

Mac: `brew install netcat`

## 2. 命令使用

nc 监听某端口

```bash
nc -lkvv 9999

# 参数
# -l 监听模式
# -k 持续监听（保持套接字打开，连接多个链接）
# -v 输出详情
# -vv 输出更加详细的信息
```

nc 探测远程端口

```bash
nc -vz 192.168.1.7 8000

# 参数
# -v 输出详情
# -z 零 I/O 模式（用于扫描）
```