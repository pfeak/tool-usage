# PostgreSQL 用户/数据库 创建

#### 1. 进入 PostgreSQL

进入 PostgreSQL 命令： `psql -U root -d my_test_db`

```shell
bash-5.1# psql -U root -d my_test_db
psql (13.3)
Type "help" for help.

my_test_db=#
```

#### 2. 创建用户

创建用户命令：`create user [用户名] with password '[用户密码]';`

> 注意：
>
> 1.  要以英文分号结尾
> 2.  密码需要引号包裹
> 3.  用户名不能大写，密码可以

```shell
my_test_db=# create user myadmin with password 'mypassword';
CREATE ROLE
my_test_db=#
```

#### 3. 创建数据库

创建数据库命令：`create database [数据库名] owner [用户名];`

>注意：
>
>1. 要以英文分号结尾
>2. 需要使用已存在用户名作为数据库拥有者
>3. 数据库名不能大写

```shell
postgres=# create database mydatabase owner myadmin;
CREATE DATABASE
postgres=#
```

#### 4. 数据库授权

数据库授权命令（全部权限授予）：`grant all on database [数据库名] to [用户名];`

>注意：
>
>1. 要以英文分号结尾
>2. 需要使用已存在用户名作为数据库被授权者

```shell
postgres=# grant all on database mydatabase to myadmin;
GRANT
postgres=#
```

#### 5. 用户与数据库查看

查看所有数据库：`\l`

连接指定数据库：`\c [数据库名]`

查看当前连接的用户：`select * from current_user;`

查看所有用户名：`\du`
