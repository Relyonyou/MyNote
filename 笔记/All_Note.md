# All

- 了解到VPS搬瓦工
- 宝塔应用服务器的部署
- LIMP

- git 

	配置信息 config  ssh_config
	
	端口:20   443

## 3.16

### Github项目

- 1.JavaGuide: 一份涵盖大部分 Java 程序员所需要掌握的核心知识。
- 2.CS-Notes: 技术面试必备基础知识
- 3.advanced-java: 涵盖高并发、分布式、高可用、微服务
- 4.miaosha:秒杀系统设计与实现
- 5.architect-awesome:后端架构师技术图谱
- 6.toBeTopJavaer:Java工程师成神之路
- 7.technology-talk:Java生态圈常用技术
- 8.JavaFamily：互联网一线大厂面试指南
- 9.JCSprout：处于萌芽的Java核心知识库
- 10.fullstack-tutorial:全栈学习
- 11.JGrowing:Java 成长路线，但学到不仅仅是 Java
- 12.3y:从Java基础、JavaWeb基础到常用的框架再到面试题都有完整的教程，几乎涵盖了Java后端必备的知识点
- 13.interview_internal_reference:2019年最新总结，阿里，腾讯，百度，美团，头条等技术面试题目，以及答案，专家出题人分析汇总。
- 14.effective-java-3rd-chinese:Effective Java中文版（第3版），Java 四大名著之一，本书一共包含90个条目，每个条目讨论Java程序设计中的一条规则。这些规则反映了最有经验的优秀程序员在实践中常用的一些有益的做法。
- 15.《OnJava8》：又名《Java编程思想》第5版， Java 四大名著之一。

《Java工程师面试突击第一季》：链接:https://pan.baidu.com/s/1wQNloOiviOLc6jlXGBtSjA 密码:srgn

### 其它

- https 证书
- 三次握手
- sql优化
- rqd
- hashmap
- 自旋

## 3.17

#### 微服务(牵一发而动全身---监控)

每一个功能元素最终都是一个可独立替换的服务

单元互联可通过Http交流

#### 网关 - 权限控制

#### 服务治理--监控接口调用

#### 链路追踪

#### 熔断、服务降级、限流

#### 中间件

#### SpringBoot

以前在部署到服务器上需要将Java程序打成war包,现在有了Spring Boot可直接打成jar包
负载均衡 并发能力 同一内容十几个服务器 

## 3.18

#### 学习SpringBoot

1.端口号被占用如何解决
netstat -ano | findstr 8080
taskkill /pid xxxx /f

2.Springboot的web开发中static和templates

##2020/3/19

centos 开放端口号

小程序端和服务器端


##到底怎么才是对的,

先把技术拓宽了,然后往深研究
还是怎么的呢

decision:

learn Java deeply 

from now on



## 3.22

n|=n>>>2;//n=n|(n>>>2)=1000100|0010001=1010101
...
看出规律来了吧，右移多少位，就把最高位右边的第x位设置为1；

第二次，就把两个为1的右边xx位再设置为1；

第n次，就把上一步出现的1右边xxxx位置为1；//xxx随便写写，意会

这样执行完，原来是1000000，变成了1111111，最后加1，就变成2的整数次方数了。

HashSet    检查重复:

第一道关:HashCode    散列地址 若散列地址相同,则比较equals的值
第二道关:equals   若equals的值相同,Hashset就不让加入操作成功
==与equals的区别

==是判断两个变量或实例是不是指向同一个内存空间 equals是判断两个变量或实例所指向的内存空间的值是不是相同
==是指对内存地址进行比较 equals()是对字符串的内容进行比较
==指引用是否相同 equals()指的是值是否相同


hash()

红黑树

## 3.23

### 电脑激活:

使用软件:	脚本之家 下载激活之家

电脑屏幕出现黑边 : 分辨率

Docker 容器 独立运行于host的内核

VM 虚拟机

dockerfile : 描述docker镜像

由一行行命令组成

和宿主机相隔离

## 3.24

工具
git & svn
maven & gradle
**Intellij IDEA常用插件：**

- Maven Helper 
- FindBugs-IDEA 
- 阿里巴巴代码规约检测
- GsonFormat  
- Maven Helper
- Lombok plugin
- Free Mybatis plugin

### Linux命令:

大体上就是增删改查

网络管理

文件传输

如何给Github的单独文件添加注释
分别添加注释
$ git add text/text1.txt
$ git commit -m "text1"
$ git add text/text2.txt
$ git commit -m "text2"
$ git push origin master

## 4.4

- 先考程序员->软件设计师

### 案例题目：学生健康打卡

主要技术栈：

- 微信小程序
- SpringBoot
- Mybatis
- RabbitMQ
- Redis
- Druid
- MySQL

### 基础知识要求：

- JAVA
- Linux
- 小程序端
  - 小程序开发开发环境（回复：）
  - 小程序登录功能（回复：）
  - 用户身份识别功能（回复：）

- Git项目管理
- 绑定用户身份功能
- 提交上报表单功能
- 最新表单数据功能
- 解除绑定功能
- 定位功能
- 消息提醒功能
- 发布上线

- Java后端
  - Intelli IDEA工具介绍
  - SpringBoot框架搭建
  - 集成mybatis
  - 集成Ehcache缓存
  - 集成Redis
  - 实现用户登录
  - Git项目管理
  - 集成参数校验框架
  - 集成异常处理
  - 集成shiro权限管理
  - 实现表单保存
  - Jmeter压力测试
  - Redis缓存
  - 集成RabbitMQ
  - 增加验证码
  - 服务器优化（Nginx）
  - 实现负载均衡
  - 在组件下面写内容
  - application.properties||application.yml   

**autoconfig -----自动装配**

注解可以出现派生注解和复合注解

一定要记得XxxxProperties类的含义是：封装配置文件中相关属性；
XxxxAutoConfiguration类的含义是：自动配置类，目的是给容器中添加组件。

而其他的主方法启动，则是为了加载这些五花八门的XxxxAutoConfiguration类。

application-{profile}.properties  ----可配置多个环境



### **JDK各个版本的新特性**


Java -jar 启动jar包 ctrl+c 停止

SpringBoot的组件具体是指什么


ctrl+n  快速启动搜索

### SpringBoot的精髓

想用什么 并且 如果SpringBoot 有什么 就用自动配置类添加组件 
 并且 可以 在application.properties中指定一些属性的信息，并且版本SpringBoot已经帮你处理好了

debug:可显示自动配置的信息

### 什么是日志

SpringBoot日志


来记录一些系统的运行时信息；日志框架  

		 日志门面  						 日志实现
		选择SLF4J							Logback（选择）	
		放弃JCL ， lboss-logging			JUL     Log4j2   Log4j|

SpringBoot选择SLF4J+Logback			


因为Spring，等等的日志都不一样

所有需要统一进行替换 ， 替换成中间包-----一种包含原有的框架里所包含的内容----达到狸猫换太子的形式

-----从而达到统一配置日志SLF4J+Logback	


## 4.5

logback|log4j2-spring.xml -----可配置使用的环境环境

idea 可以生成maven树

dependency ----exclude 排除

webjars引入jar


thymeleaf


${} ---OGNL表达式


例：<h1>你好</h1>
转义显示的是原始的字符串
不转义显示的是大标题


视图解析器 

懒加载

注册到容器中:@Bean @Component


jsr303错误代码

### Java反射机制

当程序主动使用某个类时，如果该类还没有被加载到内存中，
则系统会通过加载、连接、初始化这三个步骤对该类进行初始化



WebMvcConfigurationAdapter 在spring boot 2.0被废弃以后，
可以使用系提供的类：WebMvcConfigurationSupport，来替换之前的WebMvcConfigurationAdapter 。6


国际化 切换语言 
语言 区域 

### thymeleaf语法


		<!--引入jquery-->
	
		<dependency>
	        <groupId>org.webjars</groupId>
	        <artifactId>jquery</artifactId>
	        <version>3.3.1</version>
	    </dependency>

<!--引入bootstrap-->
<dependency>
            <groupId>org.webjars</groupId>
            <artifactId>bootstrap</artifactId>
            <version>4.0.0</version>
        </dependency>

**IDEA**

**CTRL+F9重新编译s**



**crud**是指在做计算处理时的增加(Create)、读取(Retrieve)、更新(Update)和删除(Delete)几个单词的首字母简写。
**crud**主要被用在描述软件系统中数据库或者持久层的基本操作功能。



**CodeGlance插件功能消失：  CTRL+shift+G		恢复/隐藏**

## 4.8


Java基础：

	不熟练的：
	
		IO ， 反射 
		
	Google 
	----插件
		Octotree

## 4.12

PostMapping = RequestMapping(method=RequestMethod.POST)     GET Delete



devtool




如果路径改变，可以在路径前面直接加一个/




MyBatis 替代JDBC   持久化   ORM		Object  Relational Mapping    Pers对象 Person表  俩者间的映射关系



**配置MyBatis**

environments : 中 environment和id值选择环境

ctrl +  o   浏览全部方法

MyBatisUtil工具类


	<!-- 输入和输出得参数都只可以有一个 
		 如果想传入多个值，可以用集合，或者POJO类代替
	
	<insert id="addperson" >
		insert into person (id,age,name) values(#{},#{},#{},#{})
	</insert>
	<delete id="delstudentbyid" parameterType="int " >
		delete from person where personid= #{}
	</delete>
	<update id="UpPerson" parameterType="com.cody.entity.Person">
		update person set personname =#{personname} , personid=#{personid} , personage=#{personage}
	</update>
	<select id="queryPersonByid" parameterType="int" resultType="com.cody.entity.Person">
		select * from person where id = #{personid}
	</select>
		-->
		
		<!-- namespace:改mapper.xml映射文件的唯一标识 -->
		
	<!-- parameterType：输入参数的类型 resultType：返回结果值得类型 -->
	<!-- remarkremark -->


?	
	<!-- remarkremark -->
	<!-- 通过environments中的environment的ID值可指定运行环境 -->


?	
	<!-- 数据源类型：
				UNPOOLWED：传统的jdbc模式
				POOLED：
				JNDI：TomCat内置的数据库连接池
			
			 -->


?			 
?			 
			 <!-- 配置数据库信息 -->


?			 
?			 
	封装数据库{
	
	xxxx (String sql , XX xx){


?	
?	
		if(sql.equals("XXXX")){
			调用XXXX方法（）{
				String statement = "com.cody.entity.PersonMappers." + sql;
			
			}
		
		}


?		
	MyBatis的接口名的全类名和xxxmapper.xml的namespace的值一样    ---------------很妙


?	
	事务只针对于DML，


?	
?	
	eclipse中只识别INTEGER，不能识别integer


?	
?	
## 4.13

简单类型（8+1个String）写'${Value}'--原样输出  #{}---任意值----自动加单引号----表示是个常量
	复习SQL注入！
	
	
支持级联属性

Map<String ， Object>



mapper映射 -> mapper接口 -> mapper测试

Key和占位符一样即可成功 



### 存储过程

create or replace procedure queryCountPersonByXXXWithProcedure(gName in varchar , scount out number)
as
begin
select count(1) into scount from person where xxxcolumn = gname
end;
/




SQL的存储过程函数  ----- 相当于函数
create or replace procedure queryCountPersonByXXXWithProcedure(gName in varchar , scount out number)



创建一个存储函数：  函数名(参数名 in/out 参数类型 )
create or replace procedure  XXXXXXXXX(参数名 in/out 参数类型
对应Mybatis
存储过程的输入函数值必须是Map的形式
{
		<!-- 通过调用存储过程 实现查询 -->
			CALL queryCountByXXXWithProcedure(
				 #{gName,jdbcType=VARCHAR,mode=IN},
				 #{scount.jdbvType=INTEGER,mode=OUT}
			)
		}



**切记JDBC的增删改都需要commit**

HaspMap<>  like    a[0][]  一个二维数组的一行





类的属性严格区分大小写



**懒加载：**<行内的:select="  里面可以是同一个文件里的内容嘛？直接写ID还是？
  ">

  


  内存到硬盘会序列化

  序列化 是将内容从内存放到硬盘中去


  触发二级缓存的时机，session.closed

  二级缓存共用一个namespace ， 若有多个xxx.xml的文件的namespace值相同，则产生的Mapper公用一个对象


  LUR


  数据库的元数据


  日志级别：DEBUG,INFO,WARN,ERROR

  

  增删改可以有返回值在接口里面更改

###   **MyBatis逆向工程:** 

  1.引用jar包
  2.配置generator.xml
  3.根据Java模板类一键生成

  |没有生成conf.xml
  |逆向工程的模糊查询需要加上%%

  Criteria

  没有加参数

  There is no getter for property named 'stuid' in 'class java.lang.Integer'_百度搜索 

  


  mapperProxy->代理对象


  boundSql：将SQL和参数值进行绑定

  

###  Hander 控制器 


  四大处理器Handler

  i. StatementH
  i..ResultSet
  i...ParameterHandler
  i....Type

 b 
 Java ---1.8 新特性 

 AR逆向工程
 只需要继承一个父类

 MyBatis MP(MyBatis-Plus) 

 引入分页插件都是引入插件在<plugins>里声明<plugin/>


在Spring中需要在Bean对象中引入
<bean>
<properties name="plugins"/> 
<list><bean class="XXXXXXXXXXXX"/></list>
</bean>


 JavaBean:Fieldname
		对应
数据库：字段名字：column

例如：stuName对应stu_id

### 包装类和基本类型

这种直接把int变为Integer的赋值写法，称为自动装箱（Auto Boxing）
反过来，把Integer变为int的赋值写法，称为自动拆箱（Auto Unboxing）
自动拆箱与装箱
final class Integer extends Number implements Comparable<Integer>
动态代理（Dynamic Proxy）



### 首先来看什么是编译形语言，什么又是解释形语言？

?    编译型语言：把做好的源程序全部编译成二进制代码的可运行程序。
?	然后，就可以直接运行这个程序。执行速度快，效率高，依靠编译器，跨平台性稍差。
?    解释型语言：把已经做好的源程序，翻译一句，执行一句，直到结束。执行速度慢，
?	效率低，依靠编译器，跨平台性稍好。
?    下面来总结一下大家的观点：
?    （1）第一个观点认为Java是编译型语言，因为Java程序想要运行，那么第一步就
?	是要使用Javac进行编译。没有经过编译的.java文件，是没办法运行的

    （2）那么第二个观点则是认为Java是解释型语言，Java经过编译之后，仍然需要
    JVM的解释执行，Javac将Java源文件编译成.class文件，然后通过JVM的解释执行。
    
    综合上面两个观点来看，Java似乎既有编译型语言的特点，又有解释型语言的特点，
    也没有看到哪本权威的书籍上认定Java就是哪一种类型的语言。姑且认为是半编译型半解释型吧。


**面向过程 ：**面向过程性能比面向对象高。 因为类调用时需要实例化，开销比较大，比较消耗资源，
所以当性能是最重要的考量因素的时候，比如单片机、嵌入式开发、Linux/Unix等一般采用面向过程开发。

----》》
这个并不是根本原因，面向过程也需要分配内存，计算内存偏移量，Java性能差的主要原因并不是因为
它是面向对象语言，而是Java是半编译语言，最终的执行代码并不是可以直接被CPU执行的二进制机械码。

而面向过程语言大多都是直接编译成机械码在电脑上执行，并且其它一些面向过程的脚本语言性能也并
不一定比Java好。




引用数据类型包括：类、接口类型、数组类型、枚举类型、注解类型，字符串型。
java另一大数据类型为基本数据类型，其包括包括数值型，字符型和布尔型。

 

 SELECT [ALL|DISTINCT] select_expr FROM -> WHERE -> GROUP BY [合计函数] -> HAVING -> ORDER BY -> LIMIT

 

 IntelliJ IDEA行设置选中行,选中代码块颜色

### HashMap

 这篇应该主要想说：如果想要正确的使用 key，即可以内容相同，但不一定是同一个对象，
 所以具有相同内容的不同对象 查询返回的value应该是相同的；如果我们使用自己定义的类作为key，
 但没有定义合理的equals()方法，那么即使两个对象内容一样，
 也不会被认定为同一个key，进而查询到的value就会不同，
 这不符合key的特点，所以必须要有合理的equals()方法，同理hashCode()方法也是一样。

 通过key计算索引的方式就是调用key对象的hashCode()方法，它返回一个int整数。
 HashMap正是通过这个方法直接定位key对应的value的索引，继而直接返回value。

* 相同的输入一定有相同的输出
* 不同的输入可能有相同的输出
* 好的hash加密一定是碰撞概率低的
*
有static的不能直接调用没有static的
*
通过类名可以直接调用static的方法

### 自我感受：

静态相当于一个共有属性，属于类，可以通过类名直接可以调用，类级别的，非静态为方法

类有的，对象自然有
对象有的，类不一定有

stringbuffer:比string更强大的原因是
1.string 每次想要更新值的时候，不是在原有的基础上更改的，
而是直接开辟新的内存空间，这样，如果像是在循环过程中更改的话，极大可能会造成内存的浪费
2.stringBuffer每次更新是在同一块内存中做更改 obj.append("");
任何类型遇到字符串都会转换为字符串
多态时：父类与子类之间的转换
1.从小到大：自动转换
2.从大到小，强制 转换

类-----单一继承多实现接口

接口可以实现多继承，但是只是特例，Java中是单一继承的
*
	接口 = 实现类
	父类 = 子类
*

Java中只有值传递


基本类型的值传递在传入方法中是不改变原值的，而引用类型的值是会改变的，
引用类型的值是存放在JVM的堆中，好比一个电视，有好几个遥控器一样


JDK1.7以前常量池放在方法区中，以后都放在堆中


/*  
                函数式接口，有且只有一个抽象方法
                @FunctionalInterface
            */
			
			
## 5.2
在搭建SpringBoot+mybatis时遇到：Cannot determine value type from string 'xxxxxx'

解决方法：POJO类缺少无参构造的方法，----有效
The server time zone value '?й???????' is unrecognized or represents more than one time


原因是时区不对
字面翻译应该是时区不一致
在application.properties中加上?serverTimezone=Asia/Shanghai
即可


mapper接口和xml文件关联时，没有找到xml文件
解决方法：
在pom.xml文件的build标签中加入下面这段话即可
 <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.xml</include>
                </includes>
            </resource>
        </resources>
		
		
## 5.14

Json在任意平台都可以传输

/**
* 前缀的形式
*/
 private String prefix = "tool/build";


 ## 5.23
 在 Java 中定义一个不做事且没有参数的构造方法的作用？
Java 程序在执行子类的构造方法之前，如果没有用 super()来调用父类特定的构造方法，
则会调用父类中“没有参数的构造方法”。因此，如果父类中只定义了有参数的构造方法，
而在子类的构造方法中又没有用 super()来调用父类中特定的构造方法，则编译时将发生错误，
因为 Java 程序在父类中找不到没有参数的构造方法可供执行。
解决办法是在父类里加上一个不做事且没有参数的构造方法。

对象相等指的是内存中的东西相等
对象的引用相等指的是指向的内存地址相等

## 5.26
跳表
从上面的对比中可以看出，
链表虽然通过增加指针域提升了自由度，
但是却导致数据的查询效率恶化。
特别是当链表长度很长的时候，对数据的查询还得从头依次查询，这样的效率会更低。
跳表的产生就是为了解决链表过长的问题，通过增加链表的多级索引来加快原始链表的查询效率。
这样的方式可以让查询的时间复杂度从O(n)提升至O(logn)。


栈管运行，堆管存储。则虚拟机栈负责运行代码，而虚拟机堆负责存储数据。

## 7.11

### **请求转发：**

浏览器告诉A：“我想处理这个请求”
A响应浏览器：“我可以处理这个请求”---路径不改变

### **重定向：**

浏览器告诉A：“我想处理这个请求”
A响应浏览器：“我不可以处理这个请求，B可以处理”
浏览器去找B ---路径改变

### **调通小程序的前后端：**

小程序通过url：“localhost:8080/Nsd_market”

servlet中的WebServlet("/LoginValidateServlet")
相当于controller中的@requestmapping("映射");