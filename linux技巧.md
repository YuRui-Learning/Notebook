

## 系统状况

### 进程

top查看进程，按M按内存排序，按P按CPU占用排序，Q退出

ps -aux | grep **** 查该类所有进程kill PID

kill -9 pid强制杀

### 硬存

df -h

### 内存

free -h

docker stats看容器的运存

### 当前目录大小

du -sh du -ch（详细结果）

### 软链

```bash
ln -s <source> <destination> 
```

### 网络连接

netstat -nt

### 根用户权限

sudo su

### 密码

sudo passwd root 

### 历史记录

history 2000条操作记录

### 版本更新

sudo apt-get update
sudo apt-get upgrade
sudo apt update

### 安装

apt-get install

pip install 

## 显卡

### GPU

nvidia -smi

nvidia -smi -l 实时查看GPU

### cuda

nvcc -V 

### 型号

lspci | grep VGA

## 文件

### 增删改查

Linux下 ls查看目录，windows下是dir

cat .txt 查看文件

more * 呈现一部分 空格下一页，b上一页，q退出，less命令类似

head -n xxx查看前n行内容，tail -n xxx 查看尾n行内容

ag 全局查找

tree dir 目录结构
rm -r dir
rm *.txt

### 文件权限

r读 w写 x移动

chmod +x -x +r -r +w -w

sudo chmod -R 777 {对应文件夹名称}/

### 文件检索

find /path/to/directory/ -name '*.py'

grep xxx 如果存在xxx就标出

ag xxx 搜索包含xxx的行

wc 统计行数，单词数，字节数 -l行数 -w单词数 -c字节数

tree 展示当前目录下的目录结构

cut 分割一行内容

sort将stdin内容按照字典序排序

xargs 将stdin数据变成命令参数

### 压缩

tar -zcvf ttt.tar.gz tmp/*

### 解压

unzip *.zip

tar -xf *.tar.gz

tar -zxvf *.tar.gz

## 应用

### vim

chmod +x .sh 添加权限

### git

git reset --hard HEAD^ 回退一个版本，^表示版本个数

git log：分支变换情况

git reflog 分支切换过程

### weget

weget https可以下载一个数据或者文件

### 视频

windows同步播放

sudo apt-get install ffmpeg

ffmpeg -y -i input.mp4 -c:v libx264 -c:a aac -strict experimental -tune fastdecode -pix_fmt yuv420p -b:a 192k -ar 48000 output.mp4

### MD5

md5sum获取md5哈希值

### 实时调用

Watch -n 0.5 shell命令

### 文件比较

diff xxx yyy



## 环境变量

env查看环境遍历

echo $DISPLAY 输出值

unset DISPLAY 删除环境变量

export DISPLAY=:0.0 设置环境变量
