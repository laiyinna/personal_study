### java基础

1、整数（以什么开头）：二进制0b、八进制0、十六进制0x

2、Tomcat安装可能遇到的问题：

​	a、java环境变量没有配置

​	b、闪退问题：需要配置兼容性

​	c、乱码问题：配置文件中设置

3、网站输入网址是如何访问的：

​	a、检查本机的C:\Windows\System32\drivers\etc里的hosts文件下有没有输入的域名的映射；

​		有，直接返回对应的ip地址；

​		没有，去DNS服务器上找，找到返回ip。找不到就找不到，能咋滴。

4、HTTP

​	4.1、 相关概念

​	HTTP(超文本传输协议)是一个简单的请求--响应协议，它通常运行在TCP上。

​	HTTP/1.0：客户端可以与web服务器连接后，只能获得一个web资源，断开连接。

​	HTTP/1.1：客户端可以与web服务器连接后，可以获得多个web资源。

​	4.2、HTTP请求

​	客户端发请求到服务器。

​	a、请求行：请求方式(GET、POST、HEAD、DELETE、PUT、TRACT)

​		GET：一次请求能够携带的参数比较少，大小有限制，会在浏览器地址栏显示数据内容，不安全，但高效。

​		POST：一次请求能够携带的参数没有限制，大小没有限制，不会在浏览器地址栏显示数据内容，安全，但不高效。

​	4.3、HTTP响应

​	服务器响应给客户端。

​	状态码：

​		200：请求响应成功

​		3XX：请求重定向(重新到给定的新地址)

​			请求转发url不会发送变化，重定向会发生变化。

![1614491295980](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1614491295980.png)

​		4XX：找不到资源

​		5XX：服务器代码错误

5、Cookie会话：分为有状态会话和无状态会话。

​	有状态会话：访问一个网站，下次访问浏览器知道你访问过，称之为有状态会话。

​	5.1、保存会话的两种技术

​		cookie：客户端技术；session：服务器技术，利用这个技术可以保存用户的会话信息，可以把信息放在session中。