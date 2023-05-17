#### gpu

nvidia -smi

#### 进程

top查看进程
kill PID

##### 文件

Linux下 ls查看目录，windows下是dir

cat .txt 查看文件
ag 全局查找
tree dir 目录结构
rm -r dir
rm *.txt



#### vim

chmod +x .sh 添加权限

#### git

git reset --hard HEAD^ 回退一个版本，^表示版本个数

![image-20230501171544443](C:\Users\18423\AppData\Roaming\Typora\typora-user-images\image-20230501171544443.png)

git log：分支变换情况

git reflog 分支切换过程

#### 版本更新

sudo apt-get update
sudo apt-get upgrade
sudo apt update

#### 内存

df -h

#### 显卡

lspci | grep VGA

#### 密码

sudo passwd root 