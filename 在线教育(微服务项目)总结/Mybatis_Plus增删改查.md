### Mybatis_Plus增删改查

##### 1、Mybatis_Plus做update操作：

~~~java
	userMapper.updateById(user);
~~~

##### 2、Mybatis_Plus做insert操作：

~~~java
	userMapper.insert(user);
~~~





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

