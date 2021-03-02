### Nginx学习

#### 1、安装

​		创建文件：vim /etc/yum.repos.d/nginx.repo

​		查找Nginx包：yum list nginx

​		安装命令：yum -y install nginx

​		关闭防火墙：chkconfig iptables off（永久生效）service iptables stop（重启失效）

​		开启防火墙：chkconfig iptables on（永久生效）service iptables start（重启失效）

#### 2、linux命令：

​		按tab没有补全的问题：yum -y install bash-com* vim