### Nginx总结

因为onlineEducation项目存在多个服务，若在前端中配置多个请求地址很麻烦，所以需要将前端请求地址统一改成Nginx，由Nginx来进行请求转发到每个服务。

1、Nginx官网下载压缩包，解压后放到本地目录，在目录下打开cmd窗口，执行nginx.exe启动，停止命令建议使用nginx.exe -s quit。

​      执行启动命令时可能会存在80端口被占用的情况，这种情况自行百度解决。

2、Nginx配置：nginx目录下的conf文件夹下的nginx.conf文件。

3、配置Nginx转发规则：http模块中添加

~~~conf
	server {
        listen       9001;//对外暴露的端口
        server_name  localhost;//主机
		
		location ~ /eduservice/ {//匹配规则，~表示正则匹配，路径中包含eduservice则请求8001端口
			proxy_pass http://localhost:8001;
		}
		
		location ~ /eduoss/ {
			proxy_pass http://localhost:8002;
		}
	}
~~~





