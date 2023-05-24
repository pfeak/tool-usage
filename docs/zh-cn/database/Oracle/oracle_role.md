# Oracle 角色及用户

数据库启动需要角色身份 SYSDBA/SYSOPER。

同一主机使用 IPC 连接数据库，登录任何用户都可拥有 as sysdba 和 as sysoper。



## 1 sys 与 system 用户区别

oracle 内部有两个建好的用户：sys、system。用户可直接登录 system、sys 操作。

* sys 具有**最高权限**，只能通过 **sysdba** 模式登录数据库，拥有 SYSDBA、SYSOPER 权限
* system 拥有 **dba** 权限（没有 SYSDBA 权限），只能用 **normal** 模式登录数据，平常一般用该账号管理数据库



## 2 dba 与 sysdba 区别

sysdba 是管理 oracle 实例的，它的存在不依赖于整个数据库完全启动，只要实例启动，他就存在，以 sysdba 身份登录，装载数据库，打开数据库。

只有数据库完全启动后，dba 角色才有存在的基础。



## 3 SYSDBA 与 SYSOPER 权限区别

SYSOPER 是数据库操作员权限，sysoper 主要用来启动、关闭数据库。

* SYSOPER 登陆后用户是 "PUBLIC"
* 权限包括：
  * 打开数据库（STARTUP，ALTER DATABASE，OPEN/MOUNT/OPEN），服务器（CREATE SPFILE，etc）
  * 关闭数据库
  * 备份数据库
  * 恢复数据库 RECOVERY
  * 日志归档 ARCHIVELOG
  * 会话限制 RESTRICTED SESSION

SYSDBA 是数据库管理员权限，是最高的系统权限。

* 任何具有 SYSDBA 角色登陆后用户是 "SYS"
* 管理功能、创建数据库以及 "SYSOPER" 所有权限



## 参考

[1] [Oralce 中 sys 和 system 用户的区别](http://t.zoukankan.com/chengeng-p-10232780.html)

