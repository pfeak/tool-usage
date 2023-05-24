# nice/renice 命令使用

Linux内核将资源公平地分配给各个进程。

大部分进程启动时的优先级是相同的，因此 Linux 内核会公平地进行调度。

如果想让一个 CPU 密集型的进程运行在较低优先级，那么你就得事先配置好调度器，通过 `nice`、`renice` 命令。



## 1. nice/renice

用的比较多的是 `renice`，很少情况会临时使用 `nice`。

`nice` 值越大，权限越小，-20最大，19最小。

**查看 nice 值**

```shell
# ps 参数说明
# -a 参数：查看所有
# -e 参数：同 -a，展示所有没有控制端的进程
# -o 参数：类似于 format，指定显示 cmd、pid、nice
ps -aeo cmd,pid,nice
```

**renice 根据 pid 提权**

```shell
# renice -n [nice 值] [pid]
renice -n -20 6552
```

**nice 临时使用**

```shell
# 临时使用 nice 防止资源占用过多
# nice -n [nice 值] [正常命令&参数]
nice -n 10 tar xf xxxx.tar.gz
```

## 2. 参考

[1] [使用 nice、cpulimit 和 cgroups 限制 cpu 占用率](https://linux.cn/article-4742-1.html)

[2] [提升sshd的nice权限](https://www.cnblogs.com/dinghc/p/13161265.html)
