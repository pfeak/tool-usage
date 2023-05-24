# Elasticsearch 简单使用



## 1. 基础查询

### 1.1  _cat 查询基础信息

* 某索引分片分布 `GET _cat/shareds/index-name?v`
* 所有索引 `GET _cat/indices?v` （加 `v` 返回带 title）



## 2. 进阶查询

### 2.1 Cluster（集群）

* 集群状态 `GET _cluster/health`



### 2.2  Mapping（数据结构）

* 查看索引 mapping `GET index-name/_mapping?pretty`
* 添加索引 mapping 字段 `POST index-name/_mapping/doc?pretty`



### 2.3 Index（索引）

* 关闭索引 `POST index-name/_close`
* 打开引 `POST index-name/_open`
* 某索引信息 `GET index-name/_stats`



### 2.4 Document（文档）

* 增加 Document `POST my_index_001/_doc/`

  ```sql
  POST my_index_001/my_type/
  {
  "name": "Jim",
  "age": 18
  }
  ```

* 获取 Document `GET my_index_001/_doc/index-id`

* 修改 Document `PUT my_index_001/_doc/index-id/_update`

  ```sql
  PUT my_index_001/_doc/index-id/_update
  {
    "doc": {"age": 20}
  }
  ```

* 删除 Document `DELETE my_index_001/_doc/index-id`



### 2.5 Search（搜索查询）

* 基础查询 `GET index-name/_doc/_search`

  ```sql
  GET my_index_001/_doc/_search
  {
    "query": {
      "match_all": {}
    }
  }
  ```

* 指定查询数量（这种方法最大 10000）`size`

  ```sql
  GET my_index_001/_doc/_search
  {
    "query": {
      "match_all": {}
    },
    "size": 2
  }
  ```
  
* 指定查询位 `from`

  ```sql
  GET my_index_001/_doc/_search
  {
    "query": {
      "match_all": {}
    },
    "from": 10,
    "size": 100
  }
  ```

* 条件查询

  参考 [ES条件查询、排序](https://blog.csdn.net/zhoushimiao1990/article/details/104052376)。

