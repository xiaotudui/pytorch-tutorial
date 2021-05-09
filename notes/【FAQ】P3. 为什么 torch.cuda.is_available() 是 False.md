# 【FAQ】P3. 为什么 torch.cuda.is_available() 是 False

## 为什么 torch.cuda.is_available() 是 False

` torch.cuda.is_available() `，这个指令的作用是看，你电脑的 GPU 能否被 PyTorch 调用。

如果返回的结果是 False，可以按照以下过程进行排查。

1、确认你的 GPU，是否支持 CUDA（是否支持被 PyTorch 调用）

首先，确定你的显卡型号，是否是 NVIDIA 显卡。可以从 任务管理器 或者 设备管理器来查看显卡的型号。

![](https://pic.superbed.cn/item/5dc694908e0e2e3ee9ce69bf.png)

之后，去 [官网](https://www.geforce.com/hardware/technology/cuda/supported-gpus) 看，如果其中有你的显卡型号，则说明你的显卡是支持被 PyTorch 调用的。

（绝大多数的 NVIDIA 显卡都是支持的）

**如果没有 NVIDIA 显卡的话，也没有关系。CPU 就已经足够了，而且你会在后面的教程看到，对于小型网络，CPU 速度更快（窃喜）**

2、打开命令行，输入 `nvidia-smi`，查看自己的 `Driver Version` 

![](https://pic.superbed.cn/item/5dc67d868e0e2e3ee9cc1135.png)

我们教程中安装的 PyTorch 1.3 + CUDA 9.2 版本，要求电脑的显卡驱动大于396.26。

像我截图中的驱动版本为430.86，大于396.26。

**如果你的驱动版本小于396.26，请用各种驱动管理软件或者软件管家，去升级你的显卡驱动。当然，更推荐去官网，下载对应的最新驱动。**

3、下载最新驱动。在 [官方网站](https://www.nvidia.com/Download/index.aspx?lang=cn) 选择相应的显卡型号，操作系统，其他默认。其中的 Notebooks 是指笔记本。

![](https://pic.superbed.cn/item/5dc690038e0e2e3ee9ce0be1.png)

之后，点击搜索，下载最新驱动后，进行安装即可。

4、检查驱动版本。安装完最新的驱动后，可以再次在命令行窗口输入 `nvidia-smi`，查看最新的版本是否安装成功。

5、打开 Anaconda Prompt，输入 `conda activate pytorch`，再输入 `python`，进入 python 环境。

在 python 环境中，输入 `import torch`, 之后输入 `torch.cuda.is_available`，查看返回的结果是否是 True。

## 使用 Conda 下载 PyTorch 速度太慢了，怎么办？

1、(玄学办法) 早上下载安装，感觉早上的时候，下载的速度明显变快。

2、从本教程最顶端的百度云处，下载这两个文件。（这两个文件是适用于 pytorch1.3 + cuda9.2 + windows）

![](https://pic.superbed.cn/item/5dc691618e0e2e3ee9ce258e.png)

将这两个下载好的文件，放在 Anaconda 安装出的 pkgs 文件夹下。

![](https://pic.superbed.cn/item/5dc691c08e0e2e3ee9ce31a3.png)

之后打开 Anaconda Prompt，输入 `conda activate pytorch`。

之后，输入以下指令：` conda install --use-local pytorch-1.3.0-py3.6_cuda92_cudnn7_0.tar.bz2 ` 和 ` conda install --use-local cudatoolkit-9.2-0.tar.bz2`，即可使用下载的包进行安装。

---

## 我的大本营

[学会这三个排版原则，你就能超过80%人的排版](http://mp.weixin.qq.com/s?__biz=MzIxNDEwMzg3Mw==&mid=501968870&idx=1&sn=400094c6e5709a14fddcd2deba09d866&chksm=0fb36dc838c4e4dea98f3cde1ff717bea67e4e1ebda40b064cd33e9ef259fa19eba45117e1e4#rd)

[你想过将你的人生游戏化吗？](http://mp.weixin.qq.com/s?__biz=MzIxNDEwMzg3Mw==&mid=501968679&idx=1&sn=e90c796b3bfb7d901be333cd86199e56&chksm=0fb36d0938c4e41fbac4a459907029cc1d4855fba1a172af93d2f185b7dab9bf30c51ac72d41#rd)

[用游戏的思路激励自己](http://mp.weixin.qq.com/s?__biz=MzIxNDEwMzg3Mw==&mid=501968703&idx=1&sn=c1fa79d8b13ab7fae11ea0d72b80e4d3&chksm=0fb36d1138c4e407a625fea5211f50083dbdfa5dde2eb1d179e18c8de0c36e3f3eaab35377f2#rd)

寻找有趣或更有效率的事、工具和教程

![](https://ae01.alicdn.com/kf/H20c6f97f5b1540cabe93eb3d55f17bcdw.jpg)