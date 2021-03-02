#### Docker学习

1、启动Docker：systemctl start docker

2、设置开机自启：systemctl enable docker

3、下载镜像：docker pull 镜像名称:版本

4、查看Docker中的镜像：docker images

5、启动Docker中的镜像：docker run -p 3306:3306 --name mysql \

​					  -v /mydata/mysql/log:var/log/mysql \

​					  -v /mydata/mysql/data:var/lib/mysql \

​					  -v /mydata/mysql/conf:/ect/mysql \

​					  -e MYSQL_ROOT_PASSWORD=root \

​					  -d mysql:5.7

​				参数说明：

​					 -p 3306:3306：将容器的3306端口映射到主机的3306端口

​					 -v /mydata/mysql/log:var/log/mysql：将日志文件夹挂载到主机

​					 -v /mydata/mysql/data:var/lib/mysql：将默认数据文件夹挂载到主机

​					 -v /mydata/mysql/conf:/ect/mysql：将配置文件夹挂载到主机

​					 -e MYSQL_ROOT_PASSWORD=root：初始化root用户的密码

​					 -d mysql:5.7：-d指的是以后台方式运行。mysql:5.7指的是哪一个镜像启动的实例

6、查看docker正在运行中的容器：docker ps

7、进入docker容器内部：docker exec -it 容器id/容器names /bin/bash

8、查看mysql安装位置：whereis mysql

9、ifconfig命令无效：先cd /sbin，再ls看下是否安装了ifconfig命令，若没有则yum install net-tools