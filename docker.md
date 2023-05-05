#### 拉取镜像

docker pull aicregistry.azurecr.cn/video_school:v2.0.4

docker login -u aicaliyun aicaliyun.azurecr.cn -p LdvBoGuYlUWFqSsm3vG/URUdgptPpJMi
docker login -u aicregistry aicregistry.azurecr.cn -p Uch8BCG5WO0GoMPI6S4MCJNA2d1t=L3x

#### 查看镜像内容

docker ps -a 查看启动镜像，其中-a是查看隐藏目录

docke images 查看所有镜像

#### 改动镜像

docker start xx 启动镜像，如果镜像是docker run进去的，就不需要start，如果有启动的镜像，应该需要关闭线程中执行镜像

docker stop xx 关闭镜像

docker attach xx 进入镜像所在内容中去

sudo docker run --name video_1 -p 8022:22 --ipc=host --gpus all -it -v /d/Ray_code/04-13/HerculesModel:/home/sport/src aicregistry.azurecr.cn/video_school:v2.0.4 /bin/bash

其中需要修改的只有—name 后面数据，然后宿主机地址映射至容器地址，其中容器地址不需要注意，随意写目录就行，因为理解不深刻，导致我以为是到映像所在目录，浪费了很多时间，之后在pycharm中设置时候因为该映像目录进入需要root权限，导致无法执行

#### ssh和vim更新docker内部版本

每次进入新的容器中，应该需要ssh，vim等都更新下

apt-get update

apt-get install openssh-server

apt-get install vim

然后 vim /etc/ssh/sshd_config

后启动service ssh restart 即为启动ssh服务

#### 本地映射docker内部

docker cp 本地文件的路径 container_id:<docker容器内的路径>

example

宿主线
/home/sport/label_with_distance
docker容器
/tmp/pycharm_project_453/src/data/standing_long_jump
docker cp /home/sport/label_with_count d25356fac679:/tmp/pycharm_project_453/src/data/rope_skiping

