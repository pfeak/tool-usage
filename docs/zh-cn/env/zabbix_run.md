# Zabbix 环境搭建（基于docker、docker-compose）

## 1 克隆项目

zabbix 项目的搭建 Dockerfile、docker-compose.yml 都在开源仓库里

```shell
git clone https://github.com/zabbix/zabbix-docker.git
```

## 2 切换分支

切换代码到特定 tag 分支

```shell
git checkout 5.0.18
```

## 3 修改时区

不同分支配置文件不同，修改 `web` 时区

```bash
PHP_TZ=Asia/Shanghai
```

## 4 docker-compose 启动

代码根目录下有很多 `yaml`，选择 `mysql` 或 `postgres` 启动 `docker-compose`

```shell
docker-compose -f docker-compose_v3_alpine_pgsql_latest.yaml up -d
```

>首次启动会拉取很多远程镜像，推荐科学上网挂代理

## 5 登录

初始账号 `Admin`，初始密码 `zabbix`。
