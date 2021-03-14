### Mybatis-Plus分页

1、配置类中注入分页插件

~~~java
    /**
     * 配置类
     * @author SuSu
     * @version 1.0
     * @date 2021/3/14 14:16
     */
    @Configuration
    @MapperScan("com.atguigu.mpdemo.mapper")
    public class MyBatisPlusConfig {
        //乐观锁插件
        @Bean
        public OptimisticLockerInterceptor optimisticLockerInterceptor() {
            return new OptimisticLockerInterceptor();
        }
        //分页插件
        @Bean
        public PaginationInterceptor paginationInterceptor() {
            return new PaginationInterceptor();
        }
    }
~~~

2、编写分页代码

~~~java
	public void testSelectPage() {
        //new Page<>(1,5)第一个参数为当前页，第二个参数为每页显示的记录数
        Page<User> page = new Page<>(1,5);
        userMapper.selectPage(page, null);
        //得到每页数据的list集合
        page.getRecords().forEach(System.out::println);
        //获取当前页
        System.out.println(page.getCurrent());
        //得到当前总共多少页
        System.out.println(page.getPages());
        //每页显示的记录数
        System.out.println(page.getSize());
        //当前表中的总记录数
        System.out.println(page.getTotal());
        //是否有下一页
        System.out.println(page.hasNext());
        //是否有上一页
        System.out.println(page.hasPrevious());
    }
~~~

