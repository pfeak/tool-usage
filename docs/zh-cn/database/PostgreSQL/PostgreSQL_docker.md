# PostgreSQL 环境搭建

本文介绍 `docker` 搭建 pg 环境的简便方法，存在安全性问题，使用前请认真考虑。

存在安全性问题包括 `docker-compose.yml` 中暴露用户名密码，登录容器内不用登陆就可以进入 pg 等等。

## 1. 搭建 PostgreSQL 环境

通过 `docker`、`docker-compose` 搭建 PostgreSQL 环境

```dockerfile
# cat docker-compose.yml
version: '3.8'
services:
 postgres:
  image: postgres:alpine
  container_name: mypg
  restart: always
  environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: 123456
      POSTGRES_DB: my_test_db
  ports:
    - 5432:5432
  volumes:
    - ./data:/var/lib/postgresql/data
```

通过 `docker-compose` 启动 `PostgreSQL` 容器并进入

```shell
# 启动容器
docker-compose up -d

# 进入容器
docker exec -it mypg /bin/bash
```

## 2. 数据库命令

**进入 PostgreSQL**： `psql -U root -d my_test_db`

```shell
bash-5.1# psql -U root -d my_test_db
psql (13.3)
Type "help" for help.

my_test_db=#
```

**查看帮助**：`\?`

**查看数据库列表**：`\l`

```shell
my_test_db=# \l
                              List of databases
    Name    | Owner | Encoding |  Collate   |   Ctype    | Access privileges 
------------+-------+----------+------------+------------+-------------------
 my_test_db | root  | UTF8     | en_US.utf8 | en_US.utf8 | 
 postgres   | root  | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0  | root  | UTF8     | en_US.utf8 | en_US.utf8 | =c/root          +
            |       |          |            |            | root=CTc/root
 template1  | root  | UTF8     | en_US.utf8 | en_US.utf8 | =c/root          +
            |       |          |            |            | root=CTc/root
(4 rows)
```

**连接数据库**：`\c my_test_db`

## 3. 其他配置详见

[1] [PostgreSQL中常见的14个用户安全配置](https://cloud.tencent.com/developer/article/1657615)
