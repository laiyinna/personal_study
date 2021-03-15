### git命令总结

1、查看、修改用户名

​	**git config user.name**

​	**git config --global user.name "username"**

2、查看、修改邮箱

​	**git config user.email**

​	**git config --global user.email "email"**

3、生成.git文件夹用于git管理

​	在需要添加.git文件的目录下打开git命令窗口执行：**git init**

4、生成SSH密钥

​	**ssh-keygen -t rsa -C "email"**

5、查看远程库信息

​	**git remote -v**

6、删除关联的origin的远程库

​	**git remote rm origin**

7、建立远程连接

​	**git remote add origin 远程仓库地址**

8、克隆项目

​	**git clone git远程SHH地址**

​	在这里我克隆的时候，密钥是配置了的，但是克隆还是报错：

		The authenticity of host 'github.com (52.74.223.119)' can't be established.
​	RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
​	Are you sure you want to continue connecting (yes/no)?
​	Host key verification failed.
​	fatal: Could not read from remote repository.

​	Please make sure you have the correct access rights
​	and the repository exists.

​	出现这个问题的原因是本地少了**know_host**文件，Are you sure you want to continue connecting (yes/no)?这里**输入yes就可以，不要直接回车**。

9、git第一次提交项目到远程仓库

​	a、git init

​	b、建立连接：git remote add origin 远程仓库地址

​	c、文件添加到git暂存：git add .或者git add 文件名

​	d、提交，引号内为提交备注：git commit -m "first commit"

​	e、推送至master分支：git push -u origin master