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

docker kill 强制杀

docker rm xx 删除容器

docker rmi xxx 删除镜像

sudo docker run --name video_1 -p 8022:22 --ipc=host --gpus all -it -v /d/Ray_code/04-13/HerculesModel:/home/sport/src aicregistry.azurecr.cn/video_school:v2.0.4 /bin/bash

其中需要修改的只有—name 后面数据，然后宿主机地址映射至容器地址，其中容器地址不需要注意，随意写目录就行，因为理解不深刻，导致我以为是到映像所在目录，浪费了很多时间，之后在pycharm中设置时候因为该映像目录进入需要root权限，导致无法执行

#### ssh和vim更新docker内部版本

每次进入新的容器中，应该需要ssh，vim等都更新下

apt-get update

apt-get install openssh-server

apt-get install vim

然后 docke

后启动service ssh restart 即为启动ssh服务

#### 本地映射docker内部

docker cp 本地文件的路径 container_id:<docker容器内的路径>

example

宿主线
/home/sport/label_with_distance
docker容器
/tmp/pycharm_project_453/src/data/standing_long_jump
docker cp /home/sport/label_with_count d25356fac679:/tmp/pycharm_project_453/src/data/rope_skiping

#### docker 导出

docker export docker_id > *.tar

#### docker 扩容

1、df -h 查看磁盘空间

2、df -hl /var/lib/docker 查看docker所在目录空间大小

3、vim /usr/lib/systemd/system/docker.service

#在ExecStart=/usr/bin/dockerd 后面增加--data root /home/docker_data，注:/home/docker_data 需要自己创建 docker_data为我指定的存储空间

4、重启docker

systemctl daemon-reload

systemctl enable docker

5、查看配置   
docker info | grep -i "docker root dir"

#### docker 导入

docker load失败

![image-20230519102122371](C:\Users\yurui\AppData\Roaming\Typora\typora-user-images\image-20230519102122371.png)

报错：open /home/docker_file/tmp/docker-import-251271253/TensorRT-8.0.1.6/json: no such file or directory

![image-20230519102153669](C:\Users\yurui\AppData\Roaming\Typora\typora-user-images\image-20230519102153669.png)

cat video1.tar | docker import - video即可

并且如果docker ps -a 中没有，但是docker images中有，说明没启动，需要想办法启动

docker run -itd video1:latest /bin/bash （video1:latest是PEPOSITORY:TAG）

sudo docker run --name video_1 -p 8022:22 --ipc=host --gpus all -it -v /d/Ray_code/04-13/HerculesModel:/home/sport/src aicregistry.azurecr.cn/video_school:v2.0.4 /bin/bash

#### docker显示问题

因为docker更多是一个服务端，不涉及web端展示，所以在docker内部去做显示需要通过x11调用本地的显示接口大致配置方法如下

[(101条消息) Docker容器图形界面显示（运行GUI软件）的配置方法_docker gui_Codename-NC的博客-CSDN博客](https://blog.csdn.net/ericcchen/article/details/79253416)

在主机中

sudo apt-get install x11-xserver-utils

xhost +

启动服务 提示 access control disabled，clients can connect from any host

启动docker 时候多加这几句话

 -v /tmp/.X11-unix:/tmp/.X11-unix \           #共享本地unix端口

 -e DISPLAY=unix$DISPLAY \                    #修改环境变量DISPLAY

 -e GDK_SCALE \                             

 -e GDK_DPI_SCALE \

进入docker 后可以用ubuntu下小时钟做测试

echo $DISPLAY  # 会显示显示的端口 可能是unix...可能不对

如果要查看

cd ~/

xauth list

xauth add 对应unix:10

添加的话，用以下

export DISPLAY=:0.0 # 这个可以显示

sudo apt-get install xarclock       *#安装这个小程序* 

xarclock          *#运行，如果配置成功，会显示出一个小钟表动画*

#### docker重启

docker exec -it 0a730021d87e /bin/bash

curl http://baidu-ide.bj.bcebos.com/platform/script/install-agent.sh | bash -s -- -g ddf7001c-8e17-47cf-8d09-2b15a77022f8 -c 5c64cf2571631fa5a278f64aba07ac61 -v 1.8.401.75.1.02 -p 48695

#### docker镜像管理

0a730021d87e -p 48695 个人开发机



### docker 管理

 5000  root 2023/07/13 18:58:43 docker images
 5001  root 2023/07/13 18:59:00 docker images | grep gt
 5002  root 2023/07/13 18:59:19 docker images | grep gt
 5003  root 2023/07/13 18:59:46 docker tag 
 5004  root 2023/07/13 18:59:53 docker images | grep gt
 5005  root 2023/07/13 19:00:36 docker tag registry.baidubce.com/datahub/gt_3d:2.0.1 registry.baidubce.com/datahub/shuyi:1.0.0
 5006  root 2023/07/13 19:00:43 docker images | grep shuyi
 5007  root 2023/07/13 19:03:06 docker run -itd -v /root/shuyi_dataset:/cfsdata2 --gpus=all --shm-size=312g --net=host --name=shuyi_1 registry.baidubce.com/datahub/shuyi:1.0.0 /bin/bash
 5008  root 2023/07/13 19:03:38 docker ps | grep shuyi
 5009  root 2023/07/13 19:04:18 docker ps
 5010  root 2023/07/13 19:04:31 docker ps -a
 5011  root 2023/07/13 19:05:12 docker ps | grep shuyi
 5012  root 2023/07/13 19:05:35 docker exec -it 1b7bdfe4f8a6 /bin/bash
 5013  root 2023/07/13 19:10:20 ls
 5014  root 2023/07/13 19:10:26 docker ps | grep shuyi
 5015  root 2023/07/13 19:11:46 history
