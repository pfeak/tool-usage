# JuiceFS 客户端安装与挂载

**github**: https://github.com/juicedata/juicefs

## 1 安装

### 一键安装
一键安装脚本适用于 Linux 和 macOS 系统，会根据你的硬件架构自动下载安装最新版 JuiceFS 客户端。

```shell
# 默认安装到 /usr/local/bin
curl -sSL https://d.juicefs.com/install | sh -

# 安装到 /tmp 目录下
curl -sSL https://d.juicefs.com/install | sh -s /tmp
```

### juicefs+gluster

直接安装的 juicefs 客户端不支持挂载 glusterfs 存储，需要使用 JuiceFS 社区版代码编译客户端。

```shell
git clone https://github.com/juicedata/juicefs.git
cd juicefs
make juicefs.gluster
mv juicefs.gluster /usr/local/bin/juicefs
```

## 2 远程挂载

挂在远程JuiceFS存储

```shell
export REDIS_PASSWORD={juicefs_redis_password}
juicefs mount redis://:{redis密码}@{redis_host}:{redis_port}/1 /path/to/mountpoint
```

检查远程JuiceFS存储挂载情况

```shell
juicefs status redis://:{redis密码}@{redis_host}:{redis_port}/1
```
