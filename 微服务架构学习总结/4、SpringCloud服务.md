# SpringCloud服务

------

​	1、**RestTemplate是一个基于Http协议的工具类，可以利用这个类，以http协议发送请求到指定的某个web服务器中，在SpringCloud中可以利用这个类**

​	      **来访问服务提供者。例：**

```java
	   RestTemplate res = new RestTemplate();//建议交给Spring管理

	   ResponseEntity<String> result = res.getForEntity(String url,String.class);
```

​	2、Eureka注册中心：**服务的注册与发现**

​	       服务注册：**将服务所在主机、端口、版本号、通信协议等信息登记到注册中心**

​	       服务发现：**服务消费者向注册中心请求已经登记的服务列表，然后等到某个服务的主机、端口、版本号、通信协议等信息，从而实现对具体服务的调用**

​	3、Eureka和Zookeeper的比较

​	       **一个分布式系统不可能同时满足C(一致性)、A(可用性)、P(分区容错性)，分区容错性是必须的。**

​	       **Zookeeper保证的是一致性和分区容错性，Eureka保证的是可用性和分区容错性。**

​	       在Zookeeper中，当主节点宕机时，剩余节点会进行选举，但选举可能会需要一定的时间(默认是30S)，在这段时间内会导致整个Zookeeper集群不可用，注册服务瘫痪，难以容忍。

​	       Eureka各个节点都是平等的不会出现这个问题，但是有可能会发生数据不一致的情况，因为Eureka没有保证数据的一致性，优先保证了高可用性。

​	4、Eureka是什么？

​	       **Eureka是一个基于Rest的服务，主要包括服务注册和服务发现，主要用来搭建服务注册中心(C-S架构)。**不管是服务消费者还是服务提供者都属于Eureka的客户端。

​	       维护人员可以根据Eureka服务端来监控各个微服务。



