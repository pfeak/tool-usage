# npm 镜像源修改

## 0. 查看源

命令：`npm config get registry`

```shell
➜ npm config get registry
https://registry.npmjs.org/
```

## 1. 换源

命令：`npm config set registry [源地址]`

淘宝源地址：https://registry.npm.taobao.org

```shell
➜ npm config set registry https://registry.npm.taobao.org
```

原始源地址：https://registry.npmjs.org/

```shell
➜ npm config set registry https://registry.npmjs.org/
```

