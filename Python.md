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



# 地址

### 当前地址

```
import os
print (os.getcwd())#获得当前目录
```



# 计时



```
import time
start = time.time()
end = time.time()
running_time = end-start
print('time cost : %.5f sec' %running_time)
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