---
 typora-copy-images-to: ..\Images
---



# SpringBoot注解

## 1.@SpringBootApplication

### 1.1 基石

```java
/*
* Spring Boot项目的基石
创建SpringBoot项目后会自动在主类上加上
*/
@SpringBootApplication
public class SpringSecurityJwtGuideApplication {
      public static void main(java.lang.String[] args) {
        SpringApplication.run(SpringSecurityJwtGuideApplication.class, args);
    }
}
```

### 1.2 复合注解的构成

它可以看作是**@configuration , @EnableAutoConfiguration,@CompontentScan**注解的集合

```java
package org.springframework.boot.autoconfigure;
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = {
  @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
  @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
   ......
}

package org.springframework.boot;
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {

}
```

#### 1.2.1三个注解的作用

- @EnableAutoConfiguration:启动SpringBoot的自动配置机制
- @ComponentScan:扫描被@Component{@Service,@Controller}注解的Bean，注解默认会扫描该类所在的包下所有的类。
- @Configuration：允许在Spring上下文中注册额外的Bean或导入其它配置类

## 2.Spring Bean 相关

### 2.1@Autowired

自动导入对象到类中，被注入进的类同样要被Spring容器管理比如：Service类注入到Controller类中

```java
@Service
public class UserService {
  ......
}

@RestController
@RequestMapping("/users")
public class UserController {
   @Autowired
   private UserService userService;
   ......
}
```



### 2.2 @Component，@Repository，@Service，@controller

我们一般使用==@Autowired==注解让Spring容器帮我们自动装配bean。要想把类标识成可用于`@Autowired`注解自动装配的bean的类，可以采用以下注解实现：

- `@Component`: 通用的注解，可标注任意类为Spring组件。如果一个Bean 不知道属于哪一个层，可以使用`@Component`注解标注
- `@Repository`：对应持久层即Dao层，主要用于数据库相关操作
- `@Service`：对应服务层，主要涉及一些复杂的逻辑，需要用到Dao层
- `@Controller`:对应Spring MVC控制层，主要用户接受用户请求并调用Service层返回数据给前端页面

### 2.3 @RestController



`@RestController`注解是`@Controller`和`@ResponseBody`的合集，表示这是个控制器bean，并且是将函数的返回值直接填入HTTP的响应体中，是REST风格的控制器。

单独使用`@Controller`不加`@ResponseBody`的话一般使用在要返回一个视图的情况，这种情况属于比较传统的Spring MVC的应用，对应于前后端不分离的情况。`@Controller`+`@ResponseBady`返回JSON或XML形式数据

关于`@RestController` 和 `@Controller`的对比，请看这篇文章：

[@Controller+@ResponseBady的对比](<https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485544&idx=1&sn=3cc95b88979e28fe3bfe539eb421c6d8&chksm=cea247a3f9d5ceb5e324ff4b8697adc3e828ecf71a3468445e70221cce768d1e722085359907&token=1725092312&lang=zh_CN&scene=21#wechat_redirect>)

### 2.4 @Scope

声明Spring Bean的作用域 ， 使用方法：

```java
@Bean
@Scope("singleton")
public Person personSingleton() {
    return new Person();
}
```

四种常见的SpringBean的作用域：

- **singleton**:唯一Bean实例，Spring中的Bean默认都是单例的。
- **prototype**：每次请求时都会创建一个新的Bean实例
- **request**：每一次HTTP请求都会产生一个新的bean，该bean仅在当前HTTP request内有效
- **session**：每一次HTTP请求都会产生一个新的Bean，该Bean仅在当前HTTP session内有效



### 2.5 Configuration

一般用来声明配置类，可以使用`@Component`注解替代 ，不过使用`@Configuration`注解声明配置类更加语义化。

```java
@Configuration
public class AppConfig {
    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl();
    }

}
```



## 3. 处理常见的HTTP请求类型

### 3.1 HTTP请求类型

- **GET**：请求从服务器获取特定资源。举个例子：GET/users（获取所有用户信息）

- **POST**：在服务器上创建一个新的资源。

- **PUT**：更新服务器上的资源（客户端提供更新后的整个资源）。 PUT /users/12

- **DELETE**：从服务器删除特定的资源。 DELETE / user/12

- **PARTCH**：更新服务器上的资源（客户端提供更改的属性，可以看做是部分更新），使用的比较少

  

### 3.2 GET请求

@GetMapping("users")<==>@RequestMapping(value="/users" , method=RequestMethod.GET)

```java
@GetMapping("/users")
public ResponseEntity<List<User>> getAllUsers() {
 return userRepository.findAll();
}
```



### 3.3 POST请求

@PostMapping("users")<==>@RequestMapping(value="/users" , method=RequestMethod.POST)

关于`@RequestBody`注解的使用，在下面的“前后端传值”这块会讲到。

```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@Valid @RequestBody UserCreateRequest userCreateRequest) {
 return userRespository.save(user);
}
```



### 3.4PUT请求

@PutMapping("/users/{userid}")<===>@RequestMapping(value="/users/{userid}",method=Request.PUT)

```java
@PutMapping("/users/{userId}")
public ResponseEntity<User> updateUser(@PathVariable(value = "userId") Long userId,
  /**
  	校验数据格式
  */
  @Valid @RequestBody UserUpdateRequest userUpdateRequest) {
  ......
}
```



### 3.5 DELETE

`@DeleteMapping("/users/{userId}")`等价于`@RequestMapping(value="/users/{userId}",method=RequestMethod.DELETE)`

```java
@DeleteMapping("/users/{userId}")
public ResponseEntity deleteUser(@PathVariable(value = "userId") Long userId){
  ......
}
```



### 3.6 PATCH

一般实际项目中，我们都是 PUT 不够用了之后才用 PATCH 请求去更新数据。

```java
@PatchMapping("/profile")
  public ResponseEntity updateStudent(@RequestBody StudentUpdateRequest studentUpdateRequest) {
        studentRepository.updateDetail(studentUpdateRequest);
        return ResponseEntity.ok().build();
    }
```

## 4. 前后端传值

掌握前后端传值的正确姿势，是你开始CRUD的第一步



### 4.1 @PathVariable 和 @ RequestParam

 `@PathVariable`用于获取路劲参数 ， `@RequestParam`用于获取查询参数。

```java
@GetMapping("/klasses/{klassId}/teachers")
public List<Teacher> getKlassRelatedTeachers(
         @PathVariable("klassId") Long klassId,
         @RequestParam(value = "type", required = false) String type ) {
...
}
```

如果我们请求的 url 是：`/klasses/{123456}/teachers?type=web`

那么我们服务获取到的数据就是：`klassId=123456,type=web`。

### 4.2 @RequestBody

用于读取**Request**请求（可能是**POST**，**GET**，**PUT**，**DELETE**，**PATCH**请求）的body部分并且**Content-Type**为**application/json**格式的数据，接收到数据之后会自动将数据绑定到Java对象上去。系统会使用**HttpMessageConverter**或者自定义的**HttpMessageConverte**r将请求中的body中的json字符串转换为java对象。

我们用一个简单的例子来演示一下基本使用：---我们有一个注册的接口

```java
@PostMapping("/sign-up")
public ResponseEntity signUp(@RequestBody @Valid UserRegisterRequest userRegisterRequest) {
  userService.save(userRegisterRequest);
  return ResponseEntity.ok().build();
}
```

`UserRegisterRequest`对象：

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class UserRegisterRequest {
    @NotBlank
    private String userName;
    @NotBlank
    private String password;
    @FullName
    @NotBlank
    private String fullName;
}
```

我们发送 post 请求到这个接口，并且 body 携带 JSON 数据：

```java
{"userName":"coder","fullName":"shuangkou","password":"123456"}
```

这样我们的后端就可以直接把 json 格式的数据映射到我们的 `UserRegisterRequest` 类上。

![img](F:\大二下学期内容\JAVA\JavaWeb\Images\640.png)

👉 需要注意的是：**一个请求方法只可以有一个@RequestBody，但是可以有多个@RequestParam和@PathVariable**。如果你的方法必须要用两个 `@RequestBody`来接受数据的话，大概率是你的数据库设计或者系统设计出问题了！

## 5.读取配置信息

**很多时候我们需要将一些常用的配置信息比如阿里云 oss、发送短信、微信认证的相关配置信息等等放到配置文件中。**

**下面我们来看一下 Spring 为我们提供了哪些方式帮助我们从配置文件中读取这些配置信息。**

我们的数据源`application.yml`内容如下：：

```properties
wuhan2020: 2020年初武汉爆发了新型冠状病毒，疫情严重，但是，我相信一切都会过去！武汉加油！中国加油！

my-profile:
  name: Guide哥
  email: koushuangbwcx@163.com

library:
  location: 湖北武汉加油中国加油
  books:
    - name: 天才基本法
      description: 二十二岁的林朝夕在父亲确诊阿尔茨海默病这天，得知自己暗恋多年的校园男神裴之即将出国深造的消息——对方考取的学校，恰是父亲当年为她放弃的那所。
    - name: 时间的秩序
      description: 为什么我们记得过去，而非未来？时间“流逝”意味着什么？是我们存在于时间之内，还是时间存在于我们之中？卡洛·罗韦利用诗意的文字，邀请我们思考这一亘古难题——时间的本质。
    - name: 了不起的我
      description: 如何养成一个新习惯？如何让心智变得更成熟？如何拥有高质量的关系？ 如何走出人生的艰难时刻？
```



### 5.1 @values(）常用

使用@Value("${property}")读取比较简单的配置信息：

```java
@Value("${wuhan2020}")
String wuhan2020;
```

### 5.2 @ConfigurationProperties(常用)

通过`@ConfigurationProperties`读取配置信息并与bean绑定

```java
@Component
@ConfigurationProperties(prefix = "library")
class LibraryProperties {
    @NotEmpty
    private String location;
    private List<Book> books;

    @Setter
    @Getter
    @ToString
    static class Book {
        String name;
        String description;
    }
  省略getter/setter
  ......
}
```

你可以像使用普通的 Spring bean 一样，将其注入到类中使用。



### 5.3 PropertySource(不常用)

`@PropertySource`读取指定properties文件

```java
@Component
@PropertySource("classpath:website.properties")

class WebSite {
    @Value("${url}")
    private String url;

  省略getter/setter
  ......
}
```

[10 分钟搞定 SpringBoot 如何优雅读取配置文件？](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247486181&idx=2&sn=10db0ae64ef501f96a5b0dbc4bd78786&chksm=cea2452ef9d5cc384678e456427328600971180a77e40c13936b19369672ca3e342c26e92b50&token=816772476&lang=zh_CN&scene=21#wechat_redirect)

## 6 参数校验

**数据的校验的重要性就不用多说了，即使在前端对数据进行校验的情况下，我们还是要对传入后端的数据再进行一次校验，避免用户直接绕过浏览器通过一些HTTP工具直接向后台请求一些违法数据。**

**JSR(Java Specification Requests）** 是一套 JavaBean 参数校验的标准，它定义了很多常用的校验注解，我们可以直接将这些注解加在我们 JavaBean 的属性上面，这样就可以在需要校验的时候进行校验了，非常方便！

校验的时候我们实际用的是 **Hibernate ==Valid==ator** 框架。Hibernate Validator 是 Hibernate 团队最初的数据校验框架，Hibernate Validator 4.x 是 Bean Validation 1.0（JSR 303）的参考实现，Hibernate Validator 5.x 是 Bean Validation 1.1（JSR 349）的参考实现，目前最新版的 Hibernate Validator 6.x 是 Bean Validation 2.0（JSR 380）的参考实现。

SpringBoot 项目的 spring-boot-starter-web 依赖中已经有 hibernate-validator 包，不需要引用相关依赖。如下图所示（通过 idea 插件—Maven Helper 生成）：

![img](F:\大二下学期内容\JAVA\JavaWeb\Images\640-1588853619594.png)

[如何在 Spring/Spring Boot 中做参数校验？你需要了解的都在这里！](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485783&idx=1&sn=a407f3b75efa17c643407daa7fb2acd6&chksm=cea2469cf9d5cf8afbcd0a8a1c9cc4294d6805b8e01bee6f76bb2884c5bc15478e91459def49&token=292197051&lang=zh_CN&scene=21#wechat_redirect)

👉 需要注意的是：**所有的注解，推荐使用 JSR 注解，即javax.validation.constraints，而不是org.hibernate.validator.constraints**

### 6.1 一些常用的字段验证的注解

- `@NotEmpty` 被注解的字符串的不能为努力了也不能为空
- `@NotBlank` 被注解的字符串非null，并且必须包含一个非空字符
- `@Null` 被注解的元素必须为null
- `@Null` 被注释的元素必须不能为NULL
- `@AssertTrue` 被注释的元素必须为true
- `@AssertFalse` 被注释的元素必须为false
- `@Pattern（regex，flag）` 被注释的元素必须符合指定的正则表达式
- `@Email` 被注释的元素必须是Email格式
- `@Min（Value）`被注释的元素必须是一个数字，它的值必须大于等于指定的最小值
- `@Max（value）` 被注释的元素必须是一个数字，它的值必须小于等于指定的最大值
- `@DecimalMin(value)`被注释的元素必须是一个数字，其值必须大于等于指定的最小值
- `@DecimalMax(value)` 被注释的元素必须是一个数字，其值必须小于等于指定的最大值
- `@Size(max=, min=)`被注释的元素的大小必须在指定的范围内
- `@Digits (integer, fraction)`被注释的元素必须是一个数字，其值必须在可接受的范围内
- `@Past`被注释的元素必须是一个过去的日期
- `@Future` 被注释的元素必须是一个将来的日期
- ......



### 6.2 验证请求体（RequestBody）

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class Person {

    @NotNull(message = "classId 不能为空")
    private String classId;

    @Size(max = 33)
    @NotNull(message = "name 不能为空")
    private String name;

    @Pattern(regexp = "((^Man$|^Woman$|^UGM$))", message = "sex 值不在可选范围")
    @NotNull(message = "sex 不能为空")
    private String sex;

    @Email(message = "email 格式不正确")
    @NotNull(message = "email 不能为空")
    private String email;

}
```

我们在需要验证的参数上加上了`@Valid`注解，如果验证失败，它将抛出`MethodArgumentNotValidException`。

```java
@RestController
@RequestMapping("/api")
public class PersonController {

    @PostMapping("/person")
    public ResponseEntity<Person> getPerson(@RequestBody @Valid Person person) {
        return ResponseEntity.ok().body(person);
    }
}
```

### 6.3 验证请求参数(Path Variables 和 Request Parameters)

​	**一定一定不要忘记在类上加上 Validated 注解了，这个参数可以告诉 Spring 去校验方法参数。**

```java
@RestController
@RequestMapping("/api")
@Validated
public class PersonController {

    @GetMapping("/person/{id}")
    public ResponseEntity<Integer> getPersonByID(@Valid @PathVariable("id") @Max(value = 5,message = "超过 id 的范围了") Integer id) {
        return ResponseEntity.ok().body(id);
    }
}
```

[如何在 Spring/Spring Boot 中做参数校验？你需要了解的都在这里！](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485783&idx=1&sn=a407f3b75efa17c643407daa7fb2acd6&chksm=cea2469cf9d5cf8afbcd0a8a1c9cc4294d6805b8e01bee6f76bb2884c5bc15478e91459def49&token=292197051&lang=zh_CN&scene=21#wechat_redirect)

## 7. 异常

​	`@ControllerAdvice`:使一个类成为异常处理器

例如：

```java
@ControllerAdvice
public class MyExceptionHandler{
    @ResponseBody
    @ExceptionHandler(...Exception.class)
    /*
    *自适应效果
    */
    public Map<String,Object> Exception(Exception e){
        Map<String,Object> map = new Map<>(); 
        return map;
    }
    
     public String Exception(Exception e){
        Map<String,Object> map = new Map<>(); 
         map.put("xxx","xxx");
        return "forward:/error";
    }
}
```



![1588905007530](F:\大二下学期内容\JAVA\JavaWeb\Images\自适应.png)

# SpringBoot

## Servlet的定制和切换

1.修改和server有关的配置（EmbeddedServletContainerCustomizer）

```properties
server.tomcat. xxx
```

2.编写一个**EmbeddedServletContainerCustomizer xxxxxxCustomizer**）：嵌入式的Serlvet容器的定制器，来修改Servlet容器的配置

![1588905836305](F:\大二下学期内容\JAVA\JavaWeb\Images\Servlet.png)







## 错误消息定制

![1588904055690](F:\大二下学期内容\JAVA\JavaWeb\Images\错误消息定制.png)

![Java技术路线](https://github.com/Relyonyou/ImgCloud/master/Img/Java技术路线.png)