# Oracle 连接、用户创建



## 1 连接数据库

（容器内）连接数据库（任选其一）

```shell
sqlplus / as sysdba
sqlplus sys/<your_password>@<your_SID> as sysdba
sqlplus system/<your_password>@<your_SID>
sqlplus pdbadmin/<your_password>@<your_PDBname>
```

（容器外）连接数据库（通过 SID/service_name、用户名、密码、IP、PORT）

```shell
# 1. 查询 SID 或 service name
## 查询 SID (instance_name 就是 SID)
select instance_name from v$instance;
## 查询 service name
show parameter service;

# 2. 查看用户列表
select user

# 3. 修改用户名密码
## alter user [用户名] identified by [新密码];
alter user system identified by 123456;
```



## 2 用户创建

创建用户及设置密码

```sql
create user [用户名] identified by [用户密码];
# 例如: 
create user c##app identified by 123456;
```

> 注意：创建普通用户的用户名，需要携带前缀 c## 或 C##，否则会报错 `ORA-65096: invalid common user or role name`
>
> 详见 [ORACLE 12C创建用户时出现“ORA-65096: INVALID COMMON USER OR ROLE NAME”的错误](https://www.freesion.com/article/4270299625/)

修改用户密码

```sql
alter user [用户名] identified by [用户密码];
# 例如：
alter user c##app identified by 234567;
```

撤销用户

```sql
drop user c##app;
```



## 3 创建不带 C## 的用户

如果希望创建不带 `C##` 前缀的用户，需要切换容器到 PDB。

Oracle 容器分为 CDB 与 PDB。

查看当前容器

```sql
show con_name;
```

查看可拔插容器 PDB

```sql
show pdbs;
```

切换 PDB

```sql
-- ORACLPDB1 是 PDB 容器名
ALTER SESSION SET container=ORACLPDB1;
```

切换 CDB

```sql
ALTER SESSION SET container=CDB&ROOT;
```



## 参考

[1] [oracle 创建用户并授权](https://blog.csdn.net/duan196_118/article/details/114027273)

[2] [Oracle_用户、角色知识](https://blog.csdn.net/weixin_41668007/article/details/115739310)



