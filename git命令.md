#### 本地上传文件

首先需要git init进入初始化，不然没法使用git命令。

#### clone

Git clone https的命令或者ssh 命令，ssh需要对应地址的密码。
git clone -b 分支名HerculesSDK/dev/yurui/yolov8   HerculesSDK/dev/xuzhiyu/develop

#### 连接远程

![image-20230504104011233](C:\Users\yurui\AppData\Roaming\Typora\typora-user-images\image-20230504104011233.png)

git remote -v 查看remote中的内容，origin对应
git remote add origin git@ github.con:你的gihub名字/你的仓库名.git，https内容应该也可以
git remote -v 验证remote中的内容，origin对应
git remote rm origin  删除git内origin所有内容

#### push

git add . 进入目录添加git缓存区域
git commit -m "logs"添加备注
git status 查看缓存内容

此时表示远程主机不存在需要提交的分支, 因此提交的同时需要新建分支，
"-u" 参数能够自动在本地分支和远程分支建立关联，以后只需，git push 即可！而且如果说远程并没XXX 该分支，通过这个命令还会自动创建该分支
git push -u origin HerculesSDK/dev/xuzhiyu/develop:HerculesSDK/dev/yurui/yolov8 
$ git push -u origin HerculesSDK/dev/yurui/yolov8:HerculesSDK/dev/yurui/yolov8_substitute
此时表示远程主机存在需要提交的分支, 因此只需要提交即可

#### 分支

Git checkout -b <分支名称> 创建本地新分支 HerculesSDK/dev/yurui/yolov8
Git checkout <分支名称> 切换分支

