# Oracle 角色创建、授权

登录 sys 用户，授权角色权限有时候 system 权限不够。

## 1 创建角色

在 CDB 中创建角色（这个角色访问各种视图，实现性能监测）

```sql
CREATE ROLE c##view_role;
```

## 2 授权角色

基础权限：

```sql
-- 登录权限
grant create session to c##view_role;
```

视图权限：

```sql
-- 访问各类视图权限
grant select on v_$sqlarea to c##view_role;
grant select on v_$session to c##view_role;
grant select on v_$process to c##view_role;
grant select on v_$database to c##view_role;
grant select on v_$instance to c##view_role;
grant select on dba_free_space to c##view_role;
grant select on dba_data_files to c##view_role;
```

AWR权限：

```sql
grant select on dba_hist_snapshot to c##view_role;
grant execute on dbms_workload_repository to c##view_role;
```

## 2 授权角色给用户

创建用户

```sql
create user c##viewer identified by 123456;
```

授权角色给用户

```sql
GRANT c##view_role to c##viewer;
```

## 4 取消权限、删除角色、删除用户

取消权限 grant 改成 revoke

```sql
revoke select on v_$sqlarea from view_role;
```

删除角色

```sql
drop role c##view_role;
```

删除用户

```sql
drop user c##viewer;
```

