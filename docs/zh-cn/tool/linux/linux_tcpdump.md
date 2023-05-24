# tcpdump 命令使用

tcpdump——dump the traffic on a network。

根据使用者的定义对网络上的数据包进行截获的包分析工具。 tcpdump 可以将网络中传送的数据包的 “头” 完全截获下来提供分析。它支持针对网络层、协议、主机、网络或端口的过滤，并提供 and、or、not 等逻辑语句来帮助你去掉无用的信息。

## 0. 安装

`apt install tcpdump`

## 1. 参数介绍

|          参数           | 作用                             | 示例                        |
| :---------------------: | :------------------------------- | :-------------------------- |
|         -v，-vv         | 完整解码后 protocol 输出         | tcpdump -v                  |
|           -i            | 指定网卡（不指定则抓取所有网卡） | tcpdump -i eth0             |
|          host           | 指定包含 IP                      | tcpdump host 127.0.0.1      |
|           net           | 指定包含网段                     | tcpdump net 192.168.1.0/24  |
|          port           | 指定包含端口                     | tcpdump port 22             |
| udp，tcp，icmp，arp，ip | 指定各种协议                     | tcpdump udp                 |
|        src host         | 指定数据包【源 IP】              | tcpdump src host 127.0.0.1  |
|        dst host         | 指定数据包【目的 IP】            | tcpdump dst host 127.0.0.1  |
|        src port         | 指定数据包【源端口】             | tcpdump src port 22         |
|        dst port         | 指定数据包【目的端口】           | tcpdump dst port 22         |
|           -w            | 指定抓取数据包保存文件           | tcpdump -w ./data.cap       |
|           -c            | 指定数据包抓取个数后退出         | tcpdump -w ./data.cap -c 10 |
|           -r            | 指定读取数据包文件               | tcpdump -r ./data.cap       |
|           and           | 与                               | tcpdump port 21 and port 22 |
|           not           | 或                               | tcpdump not port 22         |
|           or            | 非                               | tcpdump port 21 or port 22  |



## 2. 命令使用

抓取指定 IP 数据包

```shell
tcpdump -v host 127.0.0.1
```

抓取指定网卡 UDP 数据保存到文件

```shell
tcpdump -v -i eth0 host 127.0.0.1 and udp -w ./data.cap -c 10
```

抓取源 127.0.0.1 且目的端口 22 或源 192.168.1.55 且目的端口 80

```shell
tcpdump -v -i eth0 \( src host 127.0.0.1 and dst port 22\) or \( src host 192.168.1.55 and dst port 80 \)
```
