# stress 压力测试工具

stress 是 Linux 的压力测试工具，可以对 CPU、Memory、IO、disk 进行压力测试。

区别于 ab、JMeter 等针对网络、协议的压测工具，stress 主要针对的是设备 CPU、内存、IO、磁盘。

## 优缺点

优点：安装、使用简单，快速验证需求

缺点：无法指定消耗具体百分比资源

## 安装

Ubuntu:

```shell
sudo apt install stress
```

CentOS:

```shell
sudo yum install stress
```

## 使用

```shell
Usage: stress [OPTION [ARG]] ...
 -?, --help         show this help statement
     --version      show version statement
 -v, --verbose      be verbose
 -q, --quiet        be quiet
 -n, --dry-run      show what would have been done
 -t, --timeout N    timeout after N seconds
     --backoff N    wait factor of N microseconds before work starts
 -c, --cpu N        spawn N workers spinning on sqrt()
 -i, --io N         spawn N workers spinning on sync()
 -m, --vm N         spawn N workers spinning on malloc()/free()
     --vm-bytes B   malloc B bytes per vm worker (default is 256MB)
     --vm-stride B  touch a byte every B bytes (default is 4096)
     --vm-hang N    sleep N secs before free (default none, 0 is inf)
     --vm-keep      redirty memory instead of freeing and reallocating
 -d, --hdd N        spawn N workers spinning on write()/unlink()
     --hdd-bytes B  write B bytes per hdd worker (default is 1GB)

Example: stress --cpu 8 --io 4 --vm 2 --vm-bytes 128M --timeout 10s

Note: Numbers may be suffixed with s,m,h,d,y (time) or B,K,M,G (size).
```

## 示例

2 个 cpu 计算 60 秒退出

```shell
stress --cpu 2 --timeout 60
```

2 个进程分配内存，每次分配 1GB，100秒后释放，100秒后退出

```shell
stress --vm 2 --vm-bytes 1G --vm-hang 100 --timeout 100s
```

## 参考

[Linux性能优化（一）——stress压力测试工具 ](https://blog.51cto.com/quantfabric/2593578)