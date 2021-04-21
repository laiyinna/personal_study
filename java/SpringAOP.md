### SpringAOP动态代理

1、自定义注解实现AOP：可实现对接口操作的日志记录

​	a、自定义注解：

~~~java
        package com.atguigu.eduservice.annotation;

        import java.lang.annotation.*;

        /**
         * @author SuSu
         * @version 1.0
         * @date 2021/4/21 20:24
         */
        //@Target注解说明自定义的注解可作用在哪些地方
        @Target({ElementType.PARAMETER,ElementType.METHOD})
        //@Retention作用是定义被它所注解的注解保留多久
        @Retention(RetentionPolicy.RUNTIME)
        @Documented
        public @interface EduLog {

            /**
             * 要执行的操作类型比如：add操作
             * @return
             */
            public String operationType () default "";

            /**
             * 要执行的具体操作比如：添加用户
             * @return
             */
            public String operationName () default "";
        }
	b、编写切面：
        package com.atguigu.eduservice.aspect;

        import com.atguigu.eduservice.annotation.EduLog;
        import com.atguigu.eduservice.service.EduLogService;
        import org.aspectj.lang.JoinPoint;
        import org.aspectj.lang.ProceedingJoinPoint;
        import org.aspectj.lang.annotation.Around;
        import org.aspectj.lang.annotation.Aspect;
        import org.aspectj.lang.annotation.Pointcut;
        import org.aspectj.lang.reflect.MethodSignature;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.stereotype.Component;

        import java.lang.reflect.Method;

        /**
         * @author SuSu
         * @version 1.0
         * @date 2021/4/21 20:36
         */
        @Component
        @Aspect
        public class EduLogAspect {

            @Autowired
            private EduLogService eduLogService;

            //定义Controller切点
            @Pointcut("execution(* com.atguigu.eduservice.controller..*.*(..))")
            public void controllerAspect(){

            }


            /**
             * 环绕增强
             * @Return void
             * @Author suyuanyuan
             * @Date 20:42 2021/4/21
             * @Param @param joinPoint
             */
            @Around("controllerAspect()")
            public void around(JoinPoint joinPoint) {
                System.out.println("==========开始执行controller环绕通知===============");
                try {
                    //获取注解
                    Method proxyMethod = ((MethodSignature) joinPoint.getSignature()).getMethod();
                    Method targetMethod = joinPoint.getTarget().getClass().getMethod(proxyMethod.getName(), proxyMethod.getParameterTypes());
                    EduLog myTag = targetMethod.getAnnotation(EduLog.class);
                    String operationType = myTag.operationType();
                    String operationName = myTag.operationName();
                    try {
                        //让目标方法执行
                        ((ProceedingJoinPoint) joinPoint).proceed();
                    } catch (Throwable throwable) {
                        throwable.printStackTrace();
                    }
                    System.out.println(operationType + "-----" + operationName);

                } catch (Exception e) {
                    e.printStackTrace();
                }
                System.out.println("==========结束执行controller环绕通知===============");
            }
        }

	c、将自定义的注解添加在需要代理的方法上即可

~~~