# Pod 获取节点 IP

开发中经常有需求：获取部署 node 节点的真实 IP。

在 k8s 中可以通过 downward 将所在 node 节点的 IP 以**环境变量**的形式暴露了给 pod。

## 用法

```yaml
environment:
  - name: MY_NODE_HOST_IP
    valueFrom:
      fieldRef:
        fieldPath: status.hostIP
```

## 其他

除了 node ip，其他的信息也同样可以获取，例如 node name、pod id、metadata labels、cpu limit、memory limit。

## 参考

[1] [kubernetes Downward API](https://kubernetes.io/zh-cn/docs/concepts/workloads/pods/downward-api/)
