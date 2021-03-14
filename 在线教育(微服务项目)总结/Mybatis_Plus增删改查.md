### Mybatis_Plus增删改查

##### 1、Mybatis_Plus做update操作：

~~~java
	userMapper.updateById(user);
~~~

##### 2、Mybatis_Plus做insert操作：

~~~java
	userMapper.insert(user);
~~~

​	insert操作若id是自动增长的话，在添加数据之后想拿到自动生成的id值，需要在XML的inser块中增加useGeneratedKeys="true" keyProperty="id"这个配置，其中keyProperty后边就是主键字段不一定非是id，

​	Mybatis-Plus好像默认是返回的我记得。

​	添加这个配置后，执行完插入操作会将主键返回给你的实体类。

##### 3、Mybatis_Plus做select操作：

~~~java
	//根据id进行查询
	userMapper.selectById(7L);
	//多个id的批量查询
	userMapper.selectBatchIds(Arrays.asList(1L, 2L, 3L));
~~~

##### 4、Mybatis_Plus做delete操作：

~~~java
	userMapper.deleteById(1L);
~~~

##### 5、Mybatis_Plus实现逻辑删除：

​	a、表中增加是否删除字段，实体类增加这个属性并添加@TableLogic注解和@TableField(fill = FieldFill.INSERT) 注解。注意字段不能使用数据库关键字如delete。

​	b、自动填充处理类中添加这个字段insert的默认值。

~~~java
		this.setFieldValByName("deleted", 0, metaObject);
~~~

​	c、application.properties 加入配置。

~~~properties
        mybatis-plus.global-config.db-config.logic-delete-value=1
        mybatis-plus.global-config.db-config.logic-not-delete-value=0
~~~

​	d、逻辑删除后，在查询多条或者全部数据时，Mybatis-Plus自动查出未被逻辑删除的数据。若想查全部数据则需要自己写SQL语句进行查询。

### 补充

##### 1、若数据库中存在创建时间和修改时间，可利用Mybatis-PLus的自动填充功能为其赋值，不需要再利用set方法进行赋值。使用方法为：

​	a、在实体类进行自动填充的属性上添加注解。

~~~java
	@TableField(fill = FieldFill.INSERT)
    private Date createTime;
    @TableField(fill = FieldFill.INSERT_UPDATE)
    private Date updateTime;
~~~

​	b、自定义类并在类上添加@Component注解交给Spring管理，实现接口MetaObjectHandler实现接口里的方法(insertFill、updateFill)。

~~~java
    @Component
    public class MyMetaObjectHandler implements MetaObjectHandler {
        private static final Logger LOGGER = LoggerFactory.getLogger(MyMetaObjectHandler.class);
        @Override
        public void insertFill(MetaObject metaObject) {
            //参数1：属性名称；参数2：当前时间；参数3：元数据
            this.setFieldValByName("createTime",new Date(),metaObject);
            this.setFieldValByName("updateTime",new Date(),metaObject);
        }

        @Override
        public void updateFill(MetaObject metaObject) {
            this.setFieldValByName("updateTime", new Date(), metaObject);
        }
    }
~~~

