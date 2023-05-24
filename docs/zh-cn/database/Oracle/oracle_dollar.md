# Oracle `v$`、`gv$`、`x$`、`wrh$` 之间区别

常见 Oracle 查询表（视图）许多带有 `v$`、`gv$`、`x$`、`wrh$` 等前缀，区别如下：

| 前缀 | 代表含义                          |
| ---- | --------------------------------- |
| V$   | 针对某个实例的视图                |
| GV$  | 全局视图，针对多个实例环境        |
| X$   | GV$ 视图的数据来源，Oracle 内部表 |
| V_$  | V$ 同义词                         |
| GV_$ | GV$ 同义词                        |

可用 `V$FIXED_VIEW_DEFINITION` 视图查询到 `V$` 与 `GV$` 视图的定义。



## 视图授权

将 `v$mystat` 授权给用户 `myuser`：`grant select on v_$mystat to myuser;`

> 注意 v$mystat 会报错，因为 `v$` 是 `v$` 同义词，这里需要直接授予查询权限



## 重要的动态性能视图

v$session

v$mystat

v$sesstat

v$statname

v$sysstat

v$sql

v$sql_plan

v$sql_plan_statistics

v$sql_workarea



## 参数

[1] [Oracle 数据库中 `V$`、`GV$`、`X$`、`V$`、`GV$` 之间的关系说明](https://blog.csdn.net/seagal890/article/details/82832024)