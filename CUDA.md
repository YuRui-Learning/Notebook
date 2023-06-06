### 检测

#### 显卡

nvidia-smi

### 配置

#### cuda

sudo vim ~/.bashrc

```bash
export PATH="/usr/local/cuda-11.3/bin:$PATH"
export LD_LIBRARY_PATH="/usr/local/cuda-11.3/lib64:$LD_LIBRARY_PATH"
```

然后重启服务

source ~/.bashrc

检测 nvcc -V

![image-20230530160842491](C:\Users\yurui\AppData\Roaming\Typora\typora-user-images\image-20230530160842491.png)