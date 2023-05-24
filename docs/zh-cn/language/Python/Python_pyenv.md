# pyenv 安装与使用

## 1. 安装依赖
首先安装常用 Python 依赖库，不然编译好的 Python 没有对应功能

```shell
apt-get install libc6-dev gcc make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm openssl openssl
```

## 2. 安装 pyenv
```shell
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

写以下内容到 bash/zsh 默认文件

> 写到 `.zshrc` 之类的文件都可以

```shell
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init --path)"' >> ~/.profile
```

## 3. 离线下载 python
Pyenv 直接安装 python 比较慢，推荐用其他方式下载 python 安装包，具体操作如下：

```python
source ~/.zshrc
```

运行安装命令

```shell
# 执行 pyenv 安装指定版本 python
➜  ~ pyenv install 3.8.5
Downloading Python-3.8.5.tar.xz...
-> https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tar.xz
```

`ctrl+c` 取消通过 pyenv 下载 python。复制上面链接到浏览器，通过浏览器下载

```shell
https://www.python.org/ftp/python/3.8.5/Python-3.8.5.tar.xz
```

将下载好的 python 包放到指定位置，再次执行 pyenv

```shell
cd ~/.pyenv
mkdir cache
cp /path/to/python.tar.xz ./cache
pyenv install 3.8.5
```

## 4. 设置全局 python 版本

设置全局 Python 版本，注销生效

```shell
pyenv global 3.8.5
```

注销或重启电脑，查看全局 Python 版本

```shell
➜  ~ python -V                                  
Python 3.9.5
```

查看 pyenv 管理 python 版本

```
➜  ~ pyenv versions
  system
* 3.9.5 (set by /home/pfeak/.pyenv/version)
```
