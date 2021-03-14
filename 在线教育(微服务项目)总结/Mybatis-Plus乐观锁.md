### Mybatis-Plus乐观锁

##### 1、乐观锁：针对一种特定问题的，解决方案。解决某些问题。

​	主要解决：

​		丢失更新问题。如果不考虑事务隔离性会产生几种读问题。

​		a、脏读；b、不可重复读；c、幻读

​		乐观锁为了解决写问题：丢失更新问题(并发)

​	主要适用场景：当要更新一条记录的时候，希望这条记录没有被别人更新，也就是说实现线程安全的数据更新。

​	**乐观锁实现方式：**

​		取出记录时，获取当前version；

​		更新时，带上这个version；

​		执行更新时， set version = newVersion where version = oldVersion；

​		如果version不对，就更新失败。

##### 2、乐观锁实现方式

​	a、数据库表字段增加version字段，实体类增加version属性，并添加@Version注解。

​	b、配置乐观锁插件。

~~~java
	@Configuration
	@MapperScan("com.atguigu.mpdemo.mapper")
	public class MyBatisPlusConfig {
    	//乐观锁插件
    	@Bean
    	public OptimisticLockerInterceptor optimisticLockerInterceptor() {
        	return new OptimisticLockerInterceptor();
    	}
	}
~~~



​		b、不可重复读

​		c、幻读