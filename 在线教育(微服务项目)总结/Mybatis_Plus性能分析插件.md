### Mybatis_Plus性能分析插件

##### 1、插件作用：

​	用于输出每条SQL语句及其执行时间。用于分析SQL性能执行分析，开发环境使用，超过指定时间停止运行。有助于发现问题。在3.2版本之后移除了这个插件，建议使用第三方插件。	

##### 2、配置插件：

​	a、参数说明：

​		maxTime：SQL执行最大时长超过自动停止。

​		format：SQL是否格式化，默认false。

​	b、在 配置类中配置

~~~java
    @Bean
    @Profile({"dev","test"})// 设置 dev test 环境开启
    public PerformanceInterceptor performanceInterceptor() {
        PerformanceInterceptor performanceInterceptor = new PerformanceInterceptor();
        performanceInterceptor.setMaxTime(100);//ms，超过此处设置的ms则sql不执行
        performanceInterceptor.setFormat(true);
        return performanceInterceptor;
    }
~~~

