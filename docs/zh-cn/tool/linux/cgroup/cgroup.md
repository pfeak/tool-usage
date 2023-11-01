# CGroup

CGroup 一般也被称为“cgroups”，是 control groups 的简称。

CGroup 机制的功能就是对 linux 的一组进程进行包括 CPU、内存、磁盘 IO、网络等在内的资源使用进行限制、管理和隔离。

## 1 功能

* **限制资源的使用**：如划定内存等资源的使用上限，对文件系统的缓存进行限制等
* **优先级控制**：如让进程以低优先级被 CPU 调度等；
* **审计和统计**：例如统计 CPU 使用的比例等
* **挂起、恢复进程执行**

## 2 子系统

CGroup 通过子系统限制进程组资源，查看子系统挂载：

```shell
➜  ~ mount -t cgroup
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/cpu type cgroup (rw,nosuid,nodev,noexec,relatime,cpu)
cgroup on /sys/fs/cgroup/cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpuacct)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/net_cls type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_prio)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/rdma type cgroup (rw,nosuid,nodev,noexec,relatime,rdma)
```

`type` 类型 `cgroup` 说明是 `v1`，如果是 `cgroup2` 则是 `v2`

|子系统|功能|
|::|::|
|cpuset|可以为 cgroups 中的进程分配单独的 cpu 节点或者内存节点|
|cpu|主要限制进程的 cpu 使用率|
|cpuacct|可以统计 cgroups 中的进程的 cpu 使用报告|
|blkio|可以限制进程的块设备 io|
|memory|可以限制进程的 memory 使用量|
|devices|可以控制进程能够访问某些设备|
|freezer|可以挂起或者恢复 cgroups 中的进程|
|net_cls|可以标记 cgroups 中进程的网络数据包，然后可以使用 tc 模块（traffic control）对数据包进行控制|
|perf_event|用于控制与性能事件相关的资源管理|
|net_prio|这个子系统用来设计网络流量的优先级|
|hugetlb|这个子系统主要针对于HugeTLB系统进行限制，这是一个大页文件系统|
|pids|用于限制在 cgroup 内部创建的进程的数量|
|rdma|用于控制 RDMA（远程直接内存访问）相关资源的使用|

## 3 实验

系统：Ubuntu 22.04.2TLS  
CPU：4核  
内存：32G

### 3.1 通过隔离组限制 cpu 使用率

#### 3.1.1 编写 golang 程序消耗 cpu 资源

```go
package main

import (
	"runtime"
)


func ExhaustCpu(c int) {
    // 获取 cpu 数, 预留一个避免系统卡死
	numCPU := runtime.NumCPU()
	if c.CPU == numCPU {
		numCPU -= 1
	} else if c.CPU < numCPU {
		numCPU = c.CPU
	} else {
		numCPU -= 1
	}

    // 修改多 cpu 并行
	runtime.GOMAXPROCS(numCPU)

	for i := 0; i < numCPU; i++ {
		go func() {
			timer := time.NewTicker(time.Second)
			for {
                // 消耗 cpu
			}
		}()
	}

    // 阻塞避免退出
	select {}
}

func main() {
	ExhaustCpu(3)
}
```

使用 top 查看 cpu 消耗 `300%`，因为使用了 3 个 CPU（4 核一共 `400%`）。

注意这里留一个 CPU 避免系统卡死。

#### 3.1.2 隔离组限制 CPU 资源

创建隔离组，会在 `/sys/fs/cgroup/cpu/test_limit` 下自动生成一系列文件。

```shell
cd /sys/fs/cgroup/cpu
mkdir test_limit
cd test_limit
```

限制隔离组资源，`cpu.cfs_quota_us` 负责分配每 100 微秒隔离组可使用 cpu 时间，所以 `20%` 就是 `20*1000`

```shell
# 限制该组进程 CPU 总利用率到 20%
echo 20000 > /sys/fs/cgroup/cpu/test_limit/cpu.cfs_quota_us

# 添加需要被限制的 pid
echo 5644 >> /sys/fs/cgroup/cpu/test_limit/cgroup.procs
```

在 top 中可以看见使用率已经控制在 `20%`，而且是以进程为单位。

## 参考

[1] [一文图解｜cgroup 设计分析（Docker底层技术）](https://www.bilibili.com/read/cv19111232/)
[2] [Linux 进程资源限制 -- CGroup 的机制与用法](https://cloud.tencent.com/developer/article/2118809)
