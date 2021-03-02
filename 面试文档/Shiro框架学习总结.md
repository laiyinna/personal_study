# Shiro框架学习总结

## 	一、Shiro配置，基于配置类，java类上加@Configuration注解：

​			**1、Shiro三大核心组件：**a、**Subject**：即当前用户，所有Subject都要绑定到SecurityManager安全管理器上。

​			                                        b、**SecurityManager**：即所有Subject的管理者，Shiro框架的安全管理器，类似于SpringMVC里的DisPatcherServlet，用于拦截所有请求并进行处理

​							        c、**Realm**：用户的信息认证器和用户的权限认证器，可看做数据源，我们所定义的角色和权限都是从数据源中去获得的，用户名密码也是从Realm中

​							              获得的。

​			      **总结**：Shiro是通过Subject进行认证和授权的，Subject委托给SecurityManager去进行管理，SecurityManager从Realm中获取权限、角色等数据。

​			**2、其他组件：**a、**Authenticator：**认证器，负责主体认证，若用户觉得Shiro默认的认证不好，可自定义实现，需要认证策略，即什么情况算认证通过。 

​					        b、**Authrizer：**授权器，即访问控制器，控制用户能够访问应用中哪些功能。

​					        c、**CacheManag：**缓存控制器，用来管理用户、角色、权限等缓存，提高访问性能。

​					        d、**SessionManag：**用于管理Subject与应用之间交互的数据，管理session的生命周期。

​					        e、**SessionDAO：**用于会话的CRUD，比如想把Session放到redis中，可以实现自己的redisSessionDAO。

​					         f、**Cryptography：**密码模块，提供常见的加密组件。用于密码加密/解密。

​			**3、认证异常：**a、**UnknownAccountException:**找不到用户账号的异常。

​					        b、**IncorrectCredentialsException：**密码错误异常。

​			**4、登录登出流程：**a、页面传入的用户名密码封装到UsernamePasswordToken对象， UsernamePasswordToken token = new UsernamePasswordToken(username,password)。

​						       b、将a中的token对象传到Subject对象中，Subject.login(token)提交认证。

​						       	b1、委托给SecurityManager.login(Subject,token)执行认证，将realm数据获取到。

​					               	b2、委托给Authenticator认证器执行认证，doSingleRealmAuthentication(realm,token)。

​							       b3、通过token获取username，然后去找realm中是否存在username用户，若有，将用户数据包装成AuthenticationInfo对象返回，若没有返回null。

​							       b4、比对token中的密码跟info中的密码是否一致，若一致，表示登录成功，否则登录失败。

​						       c、调用Subject.logout()进行退出操作。 

​			**5、自定义实现Realm：**a、新建java类extends AuthorizingRealm类，并重写doGetAuthenticationInfo(AuthenticationToken token)和doGetAuthorizationInfo(PrincipalCollection principals)方法。

​							       ![1595858267683](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595858267683.png)

​							      b、重写getName()方法。

​							      c、配置ini文件，指定使用自定义Realm。![1595858542905](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595858542905.png)

​							      d、若密码加密需要做如下配置：![1595860053809](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595860053809.png)

​			**6、Shiro默认的过滤器：**a、**anon：**匿名拦截器，即不需要登录即可访问，一般用于静态资源过滤。

​								b、**authc：**表示需要认证(登录)才能使用。

​								c、**roles：**角色授权拦截器，验证用户是否拥有资源角色。

​								d、**perms：**权限授权拦截器，验证用户是否拥有资源权限。

​								e、**logout：**退出拦截器，主要属性redirectUrl：退出后重定向的地址。

​			**7、authc拦截器的作用：**a、**登录认证：**请求进来时，判断当前用户是否登录，若登录，放行，若没有登录则跳转到authc.loginUrl配置的路径。

​								b、**执行登录认证：**请求进来时，若请求路径为authc.loginUrl配置的路径时，若当前用户没有登录，authc拦截器会尝试获取请求中的账号跟密码值，然后比对

​								                               ini配置文件或realm中的用户列表，若比对正确直接执行登录操作，反之拋异常跳转到authc.loginUrl配置的路径。

​									**注意：**请求中的账号与密码必须固定为username和password，若改动必须指定，authc.usernameParam = xxx;authc.passwordParam = xxx。

​			8、**authc登录成功之后处理逻辑：**第一次发送请求，authc拦截器拦截请求，若发现当前用户没登录，则跳转到authc.loginUrl配置的路径同时保存当前请求路径，执行登录逻辑，登录成

​									       功之后，首先检查是否有保存url路径，如果有直接跳转到之前保存的路径，若没有则默认跳转到根路径。

## 	二、SpringBoot知识积累：

​			1、SpringBoot扫描持久层mapper文件：在启动类上添加注解@MapperScan("包路径")。

​			2、新增、删除、修改需要在service层添加@Transactional(propagation = Propagation.REQUIRED)注解来添加事务的特性。

​			3、vue触发点击事件的语法：按钮标签中添加@click属性，属性值为方法名称。

​			4、SpringBoot启动时扫描配置类：在启动类上添加@ServletComponentScan(basePackages = "包路径")

## 	三、其他：

​			**1、IDea变换编译级别：**

​				例：如本该编译没问题的地方报红线![1595742968166](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595742968166.png)



​				将图中的Error改为Warning，红线会消失。

​			**2、Mybatis逆向工程：**

​				配置文件：generatorConfig.xml(基于Mybatis逆向工程插件)；

​				数据库连接配置：![1595742435706](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595742435706.png)

​				生成的实体类及持久层包名：![1595742478627](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595742478627.png)

​				需要生产哪些表：![1595742544875](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595742544875.png)

​				本地jar包的位置：![1595742689726](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1595742689726.png)