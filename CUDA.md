# 非root安装cuda和cudnn

下载对应的[CUDA](https://developer.nvidia.com/cuda-downloads)和[CUDNN](https://developer.nvidia.com/rdp/cudnn-download)

## 安装cuda

比如下载：cuda_11.2.2_460.32.03_linux.run

先建立`/home/wry/CUDA/CUDA11.2`文件，在它下面创建`mylib`文件

```sh
sh cuda_11.2.2_460.32.03_linux.run
```

等待几分钟，跳出图形化界面

除了`CUDA Toolkit`前面有`×`，表示勾选，其他的都回车取消`×`

点击进入`Options`

点击进入`Toolkit Options`

将所有的`x`都去掉

点击`Change Toolkit Install Path `，修改路径为`/home/wry/CUDA/CUDA11.2/`

点击done退出

点击进入`Library install path (Blank for system default)`，修改路径为`/home/wry/CUDA/CUDA11.2/mylib`

点击done退出

点击Install安装

等待几分钟，跳出Summary表示OK

更改环境变量

```sh
vim ~/.bashrc
```

在结尾添加（注意大小写）：

```sh
export CUDA_HOME="/home/wry/CUDA"

export PATH="$CUDA_HOME/CUDA11.2/bin:$PATH" 
export LD_LIBRARY_PATH="$CUDA_HOME/CUDA11.2/lib64:$CUDA_HOME/CUDA11.2/mylib/lib64:$LD_LIBRARY_PATH"
```

退出后输入激活环境：

```sh
source ~/.bashrc
```

验证：

```sh
nvcc -V
```



## 安装CUDNN

下载的安装包现在本地解压一遍变成tar，再传到服务器

解压tar

```sh
tar -xf cudnn-linux-x86_64-8.5.0.96_cuda11-archive.tar
```

进入cudnn文件，复制文件

```sh
cd cudnn-linux-x86_64-8.5.0.96_cuda11-archive.tar

cp ./include/cudnn*.h /home/wry/CUDA/CUDA11.2/include
cp ./lib/libcudnn* /home/wry/CUDA/CUDA11.2/lib64
chmod a+r /home/wry/CUDA/CUDA11.2/include/cudnn*.h /home/wry/CUDA/CUDA11.2/lib64/libcudnn*
```

完成！