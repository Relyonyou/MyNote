```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:p="http://www.springframework.org/schema/p" xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!-- 使用扫描机制扫描控制器类，控制器类都在controller包及其子包下 -->
    <context:component-scan base-package="controller" />
    <mvc:annotation-driven />
    <!-- annotation-driven用于简化开发的配置，注解DefaultAnnotationHandlerMapping和AnnotationMethodHandlerAdapter -->
    <!-- 使用resources过滤掉不需要dispatcherservlet的资源（即静态资源，例如css、js、html、images）。
        在使用resources时必须使用annotation-driven，否则resources元素会阻止任意控制器被调用 -->
    <!-- 允许css目录下的所有文件可见 -->
    <mvc:resources location="/css/" mapping="/css/**" />
    <!-- 允许html目录下的所有文件可见 -->
    <mvc:resources location="/html/" mapping="/html/**" />
    <!-- 允许css目录下的所有文件可见 -->
    <mvc:resources location="/images/" mapping="/images/**" />
    <!-- 完成视图的对应 -->
    <!-- 对转向页面的路径解析。prefix：前缀， suffix：后缀 -->
    <bean
        class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/" />
        <property name="suffix" value=".jsp" />
    </bean>
</beans>
```