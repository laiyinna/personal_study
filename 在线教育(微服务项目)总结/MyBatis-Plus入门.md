### MyBatis-Plus

##### 一、使用Mybatis-Plus

​	1、安装，引入依赖

~~~xml
    <dependency>
        <groupId>com.baomidou</groupId>
        <artifactId>mybatis-plus-boot-starter</artifactId>
        <version>3.4.2</version>
    </dependency>
~~~

​	2、新建实体类。

~~~java
	@Data
    public class User {
        private Long id;
        private String name;
        private Integer age;
        private String email;
    }
~~~

​	3、新建mapper接口并继承BaseMapper<T>，其中BaseMapper中的泛型为实体类。如User接口对应的Mapper应该为BaseMapper<User>。

~~~java
    public interface UserMapper extends BaseMapper<User> {
        
    }
~~~

​	4、启动类或者配置类上加@MapperScan注解，并配置包扫描的地址。

~~~java
    @SpringBootApplication
    @MapperScan("com.atguigu.mpdemo.mapper")
    public class MpdemoApplication {

        public static void main(String[] args) {
            SpringApplication.run(MpdemoApplication.class, args);
        }

    }
~~~

​	5、如果需要打印SQL日志，需要在properties文件中添加配置

~~~properties
	#mybatis日志
	mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
~~~

##### 二、主键策略

​	自动增长：AUTO INCREMENT

​	UUID：每次生成随机的唯一的值。

​	Redis生成ID：利用Redis的原子操作生成id

​	Mybatis-Plus自带策略：**Twitter的snowflake算法**生成19位ID

##### 三、Mybatis-Plus主键策略

​	在实体类的主键字段上添加注解@TableId(Type = IdType.XXX)

​	**注：**1、AUTO：自动增长

​	       2、INPUT：设置id值

​	       3、NONE：输入，无策略，需要自己设置

​	       4、UUID：随机唯一值

​	       5、ID_WORKER：Mybatis-Plus自带策略，会生成19位值，数字类型比如long类型，使用这种策略

​	       6、ID_WORKER_STR：Mybatis-Plus自带策略，会生成19位值，字符串类型，使用这种策略

![1615621851618](C:\Users\lenovo\AppData\Roaming\Typora\typora-user-images\1615621851618.png)