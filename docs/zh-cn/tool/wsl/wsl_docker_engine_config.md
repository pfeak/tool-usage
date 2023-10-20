# WSL docker engine

docker 与 wsl 结合程度还是很不错的，但经常遇到拉取 docker 需要换源的问题。

可以直接在 windows 中 docker desktop 直接配置，连同 wsl docker engine 一齐修改。

## 修改 docker engine 配置

替换 `docker desktop => Settings => Docker Engine` 配置如下：

```json
{
  "builder": {
    "gc": {
      "defaultKeepStorage": "20GB",
      "enabled": true
    }
  },
  "experimental": false,
  "insecure-registries": [
    "hub.miaoyun.net.cn:8888"
  ],
  "registry-mirrors": [
    "https://0b27f0a81a00f3560fbdc00ddd2f99e0.mirror.swr.myhuaweicloud.com",
    "https://ypzju6vq.mirror.aliyuncs.com",
    "https://registry.docker-cn.com",
    "http://hub-mirror.c.163.com",
    "https://docker.mirrors.ustc.edu.cn"
  ]
}
```
