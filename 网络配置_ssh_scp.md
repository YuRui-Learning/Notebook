### 网络配置

对于一台未知的主机连接网线后正常是可以直接上网的，但是因为公司中ip地址隐藏，如果子网网段不在区间内，就会无法连接网络，如果有规定的子网网段需要知道这个具体的地址。但是绝大部分会通过一种认证的方式去得到该值，默认操作系统为ubuntu

![image-20230512155217131](C:\Users\yurui\AppData\Roaming\Typora\typora-user-images\image-20230512155217131.png)

在安全中按照如下输入，其中Username为Yurui，password为开机密码，这里还存在一个问题，更改配置不会实时更新，开始一直变成默认为sport，是选择每次手动输入结果完成该步的。

完成认证后通过ifconfig得到其对应的ip地址，现在的ip地址为172.17.2.22，这个时候即可用scp完成对应操作。

但是还需要注意一下，现在是能进入内网，但是无法访问外网的东西，通过ifconfig可以看到docker0的ip地址为![1c6e5518-5d9e-4fc1-9e2f-1556de64cbb3](C:\Users\yurui\Documents\WXWork\1688856443429485\Cache\Image\2023-05\1c6e5518-5d9e-4fc1-9e2f-1556de64cbb3.jpg)

172.17.0.1和默认路由有冲突需要修改一下

一个是不能都在17下，需要修改/etc/docker/daemon.json，具体内容需要参如下， ...表示前面内容，需要放在一个大括号里面

{

   ....,

​     "registry-mirrors": [
​         "https://docs.docker.com"
​      ],
​     "bip": "172.18.3.2/16"
}

这个之后即是把docker默认的ip地址

sudo service docker restart

然后再用ifconfig即可得到改动的dockerip

### ssh

每次进入新的容器中，应该需要ssh，vim等都更新下

apt-get update

apt-get install openssh-server

apt-get install vim

然后 vim /etc/ssh/sshd_config

后启动service ssh restart 即为启动ssh服务

#### ssh连接问题

问题描述：开始是pycharm报bug：

Inconsistency detected by ld.so: ../sysdeps/x86_64/dl-machine.h: 541: elf_machine_rela_relative: Assertion `ELFW(R_TYPE) (reloc->r_info) == R_X86_64_RELATIVE' failed!

很离谱的bug，和之前有一次docker出问题一样，然后开始ssh连接的上，之后ssh root目录报bug：

kex_exchange_identification: read: Connection reset

就怎么样都连不上

然后看到这样的解决方案[(96条消息) 解决ssh登录问题kex_exchange_identification: read: Connection reset by peer_key_exchange_identification_yangluo1683的博客-CSDN博客](https://blog.csdn.net/yangluo1683/article/details/118907066)

和这样的解决方案[(96条消息) kex_exchange_identification: read: Connection reset by peer Connection reset by 10.180.xx.1 port 22_是二狗诶的博客-CSDN博客](https://blog.csdn.net/weixin_43938093/article/details/115773505)

然后拔插网线几次之后又恢复了，但是感觉这块逻辑很奇怪

1、mkdir -p /var/empty/sshd/etc

2、cd /var/empty/sshd/etc

3、ln -s /etc/localtime localtime

4、重启sshd服务
systemctl restart sshd
或者
/etc/init.d/sshd restart

### scp

scp命令需要在同一个子网网段内能够执行将一个ip内数据赋值到另外一个ip内具体命令

scp root@172.17.2.42:/video.tar sport@172.17.2.22:/home/sport

