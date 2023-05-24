# pip 使用

## 1. 工具描述

&emsp;&emsp;pip 是 Python 包管理工具，该工具提供了对Python 包的查找、下载、安装、卸载的功能。

&emsp;&emsp;Python 2.7.9 + 或 Python 3.4+ 以上版本都自带 pip 工具（**推荐通过 pyenv 安装 python，都会自带对应版本 pip**）。

&emsp;&emsp;pip 官网：https://pypi.org/project/pip/



## 2. 工具使用

pip 更新版本

```shell
pip install --upgrade pip
```



### 2.1 三方库下载与安装


pip 查看 python 库安装包列表（当前环境 python）

```shell
pip list
```

pip 下载三方库（pip install [包名]）

```shell
# 下载最新版
pip install uwsgi

# 下载指定版
pip install uwsgi==2.0.19.1
```

pip 卸载三方库

```shell
pip uninstall uwsgi
```

pip 指定临时下载源

```shell
# pypi 下载源有时候很慢，需要指定其他下载源
pip install uwsgi -i https://pypi.mirrors.ustc.edu.cn/simple

# 其他常用国内下载源
（1）阿里云 https://mirrors.aliyun.com/pypi/simple/
（2）豆瓣 https://pypi.douban.com/simple/
（3）清华大学 https://pypi.tuna.tsinghua.edu.cn/simple/
（4）中国科学技术大学 https://pypi.mirrors.ustc.edu.cn/simple/
（5）华中科技大学 https://pypi.hustunique.com/
```

pip 永久修改下载源

* **Windows**

  * 创建文件 C:\Users\Admin\AppData\Roaming\pip\pip.ini

  *  向 pip.ini 添加如下内容：
  ```ini
     [global]
     timeout = 6000
     index-url = http://mirrors.aliyun.com/pypi/simple
     trusted-host = mirrors.aliyun.com
  ```

* **Linux**
  * home 目录下如果没有就创建 .pip/pip.conf
  
  * 向 pip.conf 添加如下内容：
  
  ``` shell
  [global]
  timeout = 6000
  index-url = https://mirrors.aliyun.com/pypi/simple/
  [install]
  use-mirrors = true
  mirrors = https://mirrors.aliyun.com/pypi/simple/
  trusted-host = mirrors.aliyun.com  
  ```



### 2.2 项目管理

pip 导出 requirements.txt

```shell
pip freeze > requirements.txt

# cat requirements.txt
uWSGI==2.0.19.1

# 注意：
# 1. requirements.txt 中包含包名与版本号，不包含 python 版本；
# 2. requirements.txt 如果有些包只有报名没有版本号，则属于不规范的包管理，为了将来少走弯路，最好重新导出。
```

pip 安装 requirements.txt

```shell
pip install -r requirements.txt
```

