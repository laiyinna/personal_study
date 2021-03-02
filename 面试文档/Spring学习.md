#### Spring学习

**1、Spring中获取某个Bean的beanName：**

​	该类增加beanName属性，实现BeanNameAware接口，重写BeanNameAware的setBeanName方法，将该方法的参数赋值给beanName属性。

**2、ApplicationContext和BeanFactory区别：**

​	ApplicationContext：继承了BeanFactory接口，更高级，提供了更多的功能，在Spring容器启动时实例化bean，预加载：

​						国际化；

​						统一的资源文件访问方式；

​						提供在监听器中注册bean事件；

​						同时加载多个配置文件；

​	BeanFactory：IOC容器，用来管理bean，依赖注入和控制反转。提供了简单的容器功能，只提供了实例化对象和拿对象的功能，默认懒加载。

​	ApplicationContext 包含 BeanFactory 的所有特性，通常推荐使用前者。但是也有一些限制情形，比如移动应用内存消耗比较严苛，在那些情景中，使用更轻量级的 BeanFactory 是更合理的。然而，在大多数企业级的应用中，ApplicationContext 是你的	首选。

**3、常用注解：**

​	@Lazy(false/true)：懒加载。

​	@DependsOn：控制Spring加载顺序，若A类中依赖了B，B先于A被初始化，则可以在A类上加这个注解，告诉容器B先被初始化。

​	@Scope("singleton")：singleton-单例；prototype-每次获取bean的时候会创建新实例；request-每次HTTP请求都会创建新的bean；

**4、BeanDefinition：Bean定义对象**：

​	这个类包含了Spring容器初始化bean的属性，beanClass、是否懒加载、加载顺序、作用域、注入模型、是否首先加载等。

**5、Spring-Mybatis原理：**

​	在Spring中，dao层的Mapper接口如何被实例化：在java中接口不能被实例化，但是在用Spring框架中我们的Mapper没有被实现但却可以被实例化进而调用CRUD方法，是因为在初始化Springbean时Mapper被JDK动态代理生成了代理类。