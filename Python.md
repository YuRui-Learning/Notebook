# Json

### 写入数据

    json_file_path = 'label_with_distance/result.json'
    json_file = open(json_file_path, mode='w')
    
    save_json_content = []
    for img_name in namelist:
        result_json = {
            "image_name": img_name}
        save_json_content.append(result_json)
    
    json.dump(save_json_content, json_file, indent=4)

### 读取数据

```
import json

with open('label_with_count/01/results.json') as user_file:
    file_contents = user_file.read()
d = json.loads(file_contents)
countnum = d[0]['countNum']
```

### 读json和csv综合id给到索引位置

```
import json
import os
import pandas as pd

save_dir_path = 'label_with_count'

df = pd.read_csv("label_with_count.csv")
ground_truth =  df.to_dict()

write_file = { 'id':[],'person':[],'groun_truth':[],'count_kpt':[],'count_bbox':[] }

for trace_id in os.listdir(save_dir_path):
    trace_id_dir = os.path.join(save_dir_path, trace_id)
    new_result = os.path.join(trace_id_dir, 'results.json')
    old_result = os.path.join(trace_id_dir, 'result.json')
    # 解析json
    with open(new_result) as user_file:
        file_contents = user_file.read()
    dict_new = json.loads(file_contents)
    with open(old_result) as user_file:
        file_contents = user_file.read()
    dict_old = json.loads(file_contents)

    print(trace_id_dir)
    for num in range(len(dict_new)): # n个人
        print('num',num)
        for i in range(len(ground_truth['id'])):
            if ground_truth['id'][i] == trace_id:
                # 根据id找到具体值
                # print(ground_truth[str(num)][i])
                # print(dict_new[num]['countNum'])
                # print(dict_old[num]['countNum'])
                write_file['id'].append(trace_id)
                write_file['person'].append(num)
                write_file['groun_truth'].append(ground_truth[str(num)][i])
                write_file['count_kpt'].append(dict_old[num]['countNum'])
                write_file['count_bbox'].append(dict_new[num]['countNum'])


def dic_to_csv(dic_data):
    pd.DataFrame(dic_data).to_csv('Output.csv')

dic_to_csv(write_file)
```

# 终端输入

```
from sys import stdin
for line in stdin:
	op,user_id,username,score = line.split('_ ')

```

# Pandas

字典写csv

```
pd.DataFrame(dic_data).to_csv('Output.csv')
```





# 地址

### 当前地址

```
import os
print (os.getcwd())#获得当前目录
```

### 地址拼接

因为在读数据时候会有不同数据地址不一样，比如一个目录下多个文件夹所以会需要在循环中每次更新中间一个路径就需要用到字符串拼接，其用path方法拼接，中间用 ’/‘区分，比如下列，rope_skipping_count是个文件夹，其trace_id_dir是子目录每个放数据文件夹名字，在该目录下有两个csv。所以每次读取每个csv时候都需要对其进行分别读取，所以按照如下操作。

```
data_path = os.path.join('rope_skipping_count', trace_id_dir)
person_data = os.path.join(data_path, 'person.csv')
rope_data = os.path.join(data_path, 'rope.csv')
```





# 计时



```
import time
start = time.time()
end = time.time()
running_time = end-start
print('time cost : %.5f sec' %running_time)
```

# 进度条

```text
from tqdm import tqdm
for i in tqdm(range(10000)):
    ...
```



# Parser

```text
import argparse 

parser = argparse.ArgumentParser(description='parser example')
parser.add_argument('--seed', default=1, type=int, help='Random seed')
parser.add_argument('--lr', default=0.1, type=float, help='learning rate')
parser.add_argument('--datapath', default='../../dataset/', type=str, help='dataset path')
parser.add_argument('--resume', action='store_true', help='resume from checkpoint')

args = parser.parse_args()
print('1: ', args.lr)
print('2: ', args.resume)
print('3: ', args)
```

# 数学统计

### 均值滤波加数学统计

```
import pandas as pd
import time
df = pd.read_csv("../09/results.csv")
df=df[df.apply(np.sum,axis=1)!=0]
sneakers_1 = df['0'].loc[~(df['0']==0)]
def ava_filter(x, filt_length):
    N = len(x)
    res = []
    for i in range(N):
        if i <= filt_length // 2 or i >= N - (filt_length // 2):
            temp = x[i]
        else:
            sum = 0
            for j in range(filt_length):
                sum += x[i - filt_length // 2 + j]
            temp = sum * 1.0 / filt_length
        res.append(temp)
    return res


def denoise( x, n, filt_length):
    start = time.time()
    for i in range(n):
        res = ava_filter(x, filt_length)
        x = res
    end = time.time()
     running_time = end-start
    print('time cost : %.5f sec' %running_time)
    return res

input_list = list(sneakers_1[250:])
filt_list =  denoise(input_list,len(input_list),3)
```



# method

### classmethod

```python3
class Data_test2(object):
    day=0
    month=0
    year=0
    def __init__(self,year=0,month=0,day=0):
        self.day=day
        self.month=month
        self.year=year

    @classmethod
    def get_date(cls, string_date):
        #这里第一个参数是cls， 表示调用当前的类名
        year,month,day=map(int,string_date.split('-'))
        date1=cls(year,month,day)
        #返回的是一个初始化后的类
        return date1

    def out_date(self):
        print "year :"
        print self.year
        print "month :"
        print self.month
        print "day :"
        print self.day
```

这样的好处就是你以后重构类的时候不必要修改构造函数，只需要额外添加你要处理的函数

在已写好初始类的情况下，想给初始类再新添功能，不需要改初始类，只要在下一个类内部新写一个方法，方法用@classmethod装饰一下即可。

```python3
# 初始类：
class Data_test(object):
    day=0
    month=0
    year=0
    def __init__(self,year=0,month=0,day=0):
        self.day=day
        self.month=month
        self.year=year

    def out_date(self):
        print "year :"
        print self.year
        print "month :"
        print self.month
        print "day :"
        print self.day

# 新增功能：
class Str2IntParam(Data_test):
    @classmethod
    def get_date(cls, string_date):
        #这里第一个参数是cls， 表示调用当前的类名
        year,month,day=map(int,string_date.split('-'))
        date1=cls(year,month,day)
        #返回的是一个初始化后的类
        return date1

# 使用：
r = Str2IntParam.get_date("2016-8-1")
r.out_date()

# 输出：
year :
2016
month :
8
day :
1
```

新增的功能get_date，初始类Data_test不需要改变，在Str2IntParam类里面修改就好了，Str2IntParam继承Data_test。

# Ancoda

#### 创建虚拟环境

conda create --name tensorflow python=3.6

#### 查看创建的虚拟环境

conda info --envs

#### 激活虚拟环境

conda activate tensorflow

#### 离开当前虚拟环境

conda deactivate

#### 当前环境下载新的库

conda install tensorflow==1.15.0

#### 删除虚拟环境

conda env remove --name Koopman

# 解释器位置

python

import sys

print(sys.executable/)

# 库安装

## pycocotools

ERROR: Failed building wheel for pycocotools
subprocess-exited-with-error
legacy-install-failure
Encountered error while trying to install package.
![在这里插入图片描述](https://img-blog.csdnimg.cn/6164caedd16346ccb37f6f5d3121f2ae.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA6bih5Lid57Gz57q_,size_20,color_FFFFFF,t_70,g_se,x_16)

pip install pycocotools-windows -i https://pypi.tuna.tsinghua.edu.cn/simple

下载一下压缩包

[下载](https://link.csdn.net/?target=https%3A%2F%2Fpan.baidu.com%2Fs%2F1nWQdPRtGwNnOO2DkxRuGuA)  密码：i5d7

然后把压缩包里面的![img](https://img-blog.csdnimg.cn/b9bc4da348c9471fb2fed1c076c5fe8b.png)移动到你自己环境（Anaconda或者其他)中，比如我的是Anaconda的bin在Bigdata里面

最终还是要装个visual studio 2022估计是编译需要，很离谱，

![img](https://img-blog.csdnimg.cn/86bab471ddba4cff8c13126506365ffd.png)