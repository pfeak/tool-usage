# GVM

Golang 版本管理器。

GitHub: https://github.com/moovweb/gvm

## 1 安装

### 1.1 依赖安装

```bash
sudo apt-get install curl git mercurial make binutils bison gcc build-essential
```

### 1.2 GVM安装

**bash**

```shell
bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
```

**zsh**

```bash
zsh < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
```

## 2 使用

### 2.1 安装 Golang

安装指定版本 Golang（-B 只安装二进制文件）

```shell
gvm install go1.8.3 -B
gvm use go1.4 [--default]
```

> Go 1.5+ 从工具链删除 C 编译器（Go 编译器取而代之），所以为了编译 Go1.5+ 需要安装 Go1.4。

### 2.2 列出 Golang 版本

列出已安装版本

```shell
gvm list
```

列出可安装版本

```shell
gmv listall
```

### 2.3 卸载 GVM

完全删除 gvm 与所有已安装 Go 版本

```shell
gvm implode
```

