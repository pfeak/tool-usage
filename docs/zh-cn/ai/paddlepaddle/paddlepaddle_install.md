# PaddlePaddle + CUDA + cuDNN

## 1 基础配置

显卡：GeForce RTX 3080Ti

CPU：amd64 架构

系统：Win10

Python：3.10.2

## 2 主要参考

PaddlePaddle 快速安装：https://www.paddlepaddle.org.cn/install/quick?docurl=/documentation/docs/zh/install/pip/windows-pip.html

cuDNN 安装：https://docs.nvidia.com/deeplearning/cudnn/install-guide/

## 3 安装目标

CUDA 版本：**11.6**

cuDNN 版本：**8.4.0**

PaddlePaddle 版本：**2.3.2**

> 注意：PaddlePaddle 2.4 + CUDA 11.7 + cuDNN 8.4.1 安装后出现各种异常，尝试后无果，最终采用以上版本

## 4 步骤

1. 更新显卡驱动到最新，查看支持 CUDA 版本高于等于 11.6
2. 安装 CUDA
3. 安装 cuDNN
4. 安装 PaddlePaddle

## 5 安装 CUDA

1. CUDA 官网下载：https://developer.nvidia.com/cuda-toolkit-archive

2. 下载 `CUDA Toolkit 11.6.2 (March 2022)`

3. 开始安装，选择自定义，安装所有组件
4. 一路顺利安装完成（中途最好别做其他事）

## 6 安装 cuDNN

1. cuDNN 官网下载（简单注册一个账号）：https://developer.nvidia.com/rdp/cudnn-archive
2. 下载 `Download cuDNN v8.4.0 (April 1st, 2022), for CUDA 11.x`
3. 下载后解压文件到 CUDA 安装对应的目录
4. 下载安装 Zlib，参考 [Zlib 安装指南](https://docs.nvidia.com/deeplearning/cudnn/install-guide/#install-zlib-windows)

## 7 安装 PaddlePaddle

1. 适当位置创建项目文件夹，进入该文件夹
2. 创建虚拟环境 `python -m venv venv`，激活虚拟环境 `source ./venv/bin/activate`
3. 更新 pip 到最新 `pip install --upgrade pip`
4. 安装 PaddlePaddle：`python -m pip install paddlepaddle-gpu==2.3.2.post116 -f https://www.paddlepaddle.org.cn/whl/windows/mkl/avx/stable.html`

## 8 测试环境

在安装 PaddlePaddle 的激活虚拟环境 venv 下，创建 python 脚本如下：

```python
import paddle

paddle.utils.run_check()
```

执行后显示 `PaddlePaddle is installed successfully!` 说明安装成功

# PaddlePaddle + CUDA + cuDNN

## 1 基础配置

显卡：GeForce RTX 3080Ti

CPU：amd64 架构

系统：Win10

Python：3.10.2

## 2 主要参考

PaddlePaddle 快速安装：https://www.paddlepaddle.org.cn/install/quick?docurl=/documentation/docs/zh/install/pip/windows-pip.html

cuDNN 安装：https://docs.nvidia.com/deeplearning/cudnn/install-guide/

## 3 安装目标

CUDA 版本：**11.6**

cuDNN 版本：**8.4.0**

PaddlePaddle 版本：**2.3.2**

> 注意：PaddlePaddle 2.4 + CUDA 11.7 + cuDNN 8.4.1 安装后出现各种异常，尝试后无果，最终采用以上版本

## 4 步骤

1. 更新显卡驱动到最新，查看支持 CUDA 版本高于等于 11.6
2. 安装 CUDA
3. 安装 cuDNN
4. 安装 PaddlePaddle

## 5 安装 CUDA

1. CUDA 官网下载：https://developer.nvidia.com/cuda-toolkit-archive

2. 下载 `CUDA Toolkit 11.6.2 (March 2022)`

3. 开始安装，选择自定义，安装所有组件
4. 一路顺利安装完成（中途最好别做其他事）

## 6 安装 cuDNN

1. cuDNN 官网下载（简单注册一个账号）：https://developer.nvidia.com/rdp/cudnn-archive
2. 下载 `Download cuDNN v8.4.0 (April 1st, 2022), for CUDA 11.x`
3. 下载后解压文件到 CUDA 安装对应的目录
4. 下载安装 Zlib，参考 [Zlib 安装指南](https://docs.nvidia.com/deeplearning/cudnn/install-guide/#install-zlib-windows)

## 7 安装 PaddlePaddle

1. 适当位置创建项目文件夹，进入该文件夹
2. 创建虚拟环境 `python -m venv venv`，激活虚拟环境 `source ./venv/bin/activate`
3. 更新 pip 到最新 `pip install --upgrade pip`
4. 安装 PaddlePaddle：`python -m pip install paddlepaddle-gpu==2.3.2.post116 -f https://www.paddlepaddle.org.cn/whl/windows/mkl/avx/stable.html`

## 8 测试环境

在安装 PaddlePaddle 的激活虚拟环境 venv 下，创建 python 脚本如下：

```python
import paddle

paddle.utils.run_check()
```

执行后显示 `PaddlePaddle is installed successfully!` 说明安装成功