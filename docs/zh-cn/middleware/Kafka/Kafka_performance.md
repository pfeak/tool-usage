# Kafka 性能压力测试

## 1. 测试方法

使用 kafka 自带脚本进行压力测试

## 2. 测试工具

1. kafka 自带压力测试脚本
2. Offset explorer（kafka 数据查看工具，协助压力测试数据查看）

## 3. 测试命令

> 注意：首先需要 `cd` 到 kafka 目录

### 写入压力测试命令

```shell
./bin/kafka-producer-perf-test.sh --topic performance_test --num-records 30000000 --record-size 100 --throughput -1 --producer-props bootstrap.servers=192.168.1.7:9092
```

参数解释：

| 参数             | 功能                                | 样例                               | 样例说明                |
| :--------------- | :---------------------------------- | ---------------------------------- | ----------------------- |
| --topic          | 指定写入 topic                      | --topic test                       | 指定写入 test topic     |
| --num-records    | 指定写入数据条目数                  | --num-records 100                  | 指定总共写入 100 条数据 |
| --record-size    | 指定每条数据大小（字节）            | --record-size 1000                 | 指定每条数据 1000 字节  |
| --throughput     | 写入限速（必填，设置 -1 不做限制）  | --throughput 300000                | 限制写入速度 30W eps    |
| --producer-props | 配置 bootstrap.servers,client.id 等 | bootstrap.servers=192.168.1.7:9092 | 指定写入 server 地址    |

### 读取压力测试命令

```shell
./bin/kafka-consumer-perf-test.sh --topic performance_test --messages 10000000 --threads 1 --bootstrap-server 192.168.1.7:9092
```

参数解释

| 参数               | 功能                  | 样例                                | 样例说明             |
| ------------------ | --------------------- | ----------------------------------- | -------------------- |
| --topic            | 指定读取 topic        | --topic test                        | 读取 test topic      |
| --messages         | 指定读取数据条目数    | --messages 100000                   | 消费 10W 数据        |
| --threads          | 指定线程数（默认 10） | --threads 1                         | 开启 1 个线程        |
| --bootstrap-server | 指定 server 地址      | --bootstrap-server 192.168.1.7:9092 | 指定读取 server 地址 |


