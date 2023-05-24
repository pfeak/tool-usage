# Kubernete 使用

## 1. 节点

查看所有节点

```shell
kubectl get nodes
```

查看所有节点与标签

```shell
kubectl get nodes --show-labels
```

## 2. 标签

添加 label

```shell
kubectl label nodes <node-name> <label-key>=<label-value>
# 示例
kubectl label nodes mynode mylabel=true
kubectl label nodes mynode mylabel=hello
```

修改 label

```shell
kubectl label nodes <node-name> <label-key>=<label-value> --overwrite
```

删除 label

```shell
kubectl label nodes <node-name> <label-key>-
# 示例
kubectl label nodes mynode mylabel-
```
