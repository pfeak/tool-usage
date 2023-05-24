# Docker 指定数据存放位置

## 1 遇到问题

如果按照默认安装，docker 数据存在系统磁盘 `/` 根目录，**导致磁盘空间很快满了**，经常要清理 docker 镜像、容器。

## 2 解决办法

指定数据存放位置。

## 3 步骤

1. 停止 docker 服务：`systemctl stop docker`

2. 创建目标 docker 数据存放文件夹：`mkdir -p /home/docker/lib`

3. 迁移现有 docker 数据：`rsync -avz /var/lib/docker /home/docker/lib/`

4. 修改 system 启动配置（不存在则创建）

	```shell
	vi /etc/systemd/system/docker.service.d/my-docker-service.conf
	```
	
5. 添加内容如下（旧版本使用 `--graph` 新版本替换为 `--data-root`）

   ```shell
   [Service]
   ExecStart=
   ExecStart=/usr/bin/dockerd --data-root=/home/pfeak/docker/lib/docker
   ```

6. 重启 docker 并设置开机自启

   ```shell
   systemctl daemon-reload
   systemctl restart docker
   systemctl enable docker
   ```

7. 查看数据位置是否已更改为目标文件夹：`docker info | grep 'Docker Root Dir'`

8. 查看之前镜像是否存在：`docker images`

9. （可选）删除旧数据：`rm -rf /var/lib/docker`

## 参考

[1] [Docker更改默认存储路径](https://www.cnblogs.com/answerThe/p/12582106.html)

[2] [修改 docker Root Dir 的三种方法](https://blog.csdn.net/lhuang0813/article/details/123005016)