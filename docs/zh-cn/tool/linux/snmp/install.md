# SNMP 安装

本篇记录如何安装和使用，各种概念请自己查阅。

## 1 环境

系统: centOS

## 2 安装

```shell
yum install net-snmp net-snmp-utils
systemctl start snmpd
```

## 3 配置

只有开放权限的 oid 才可以被请求。

### 3.1 SNMP

修改文件 `/etc/snmp/snmpd.conf` 后重启 `systemctl restart snmpd`

例如，开放部分 oid

```
####
# Third, create a view for us to let the group have rights to:
# Make at least  snmpwalk -v 1 localhost -c public system fast again.
#       name           incl/excl     subtree         mask(optional)
view    systemview    included   .1.3.6.1.2.1.1
view    systemview    included   .1.3.6.1.2.1.25.1.1
view    systemview    included   .1.3.6.1.2.1.25.4.2
view    systemview    included   .1.3.6.1.2.1.25.6.3
view    systemview    included   .1.3.6.1.2.1.2.1.0
view    systemview    included   .1.3.6.1.2.1.2.2
view    systemview    included   .1.3.6.1.2.1.25.2
```

### 3.2 SNMP trap

修改文件 `/etc/snmp/snmptrapd.conf`

## 4 测试

如果 A 服务器部署 snmp、snmp trap，对比 B 服务器来说需要**主动**采集 snmp，**被动**收集 snmp trap。

### 4.1 snmpwalk

请求 snmp v2

```shell
snmpwalk -v 2c -c public 127.0.0.1:161 .1.3.6.1.2.1.2.1.0
```
> -v 版本，可选 1, 2c, 3  
> -c 指定 community

请求 snmp v3

```shell
snmpwalk -v 3 -u simulator -l authPriv -a MD5 -A "yourauthkey" -x DES -X "yourprivatekey" 127.0.0.1:161 .1.3.6.1.2.1.2.1.0
```

> -v 版本  
> -u security name  
> -l 安全等级，可选 noAuthNoPriv|authNoPriv|authPriv  
> -a 身份认证协议，可选 MD5|SHA|SHA-224|SHA-256|SHA-384|SHA-512  
> -A 身份认证协议密码  
> -x 加密协议，可选 DES|AES|AES-192|AES-256  
> -X 加密协议密码

### 4.2 snmptrap

snmptrap 只能请求发送 162 端口

```
snmptrap -v 2c -c public 127.0.0.1 '' 1.3.6.1.2.1.1.5 0 s "my-computer"
```

> -v 版本，可选 1, 2c, 3  
> -c 指定 community  
> '' Enterprise OID 表示 trap 来源，这里为空代表没有来源  
> 0  代表 trap 特殊事件，这里设置 0  
> "my-computer" 代表 trap 值
