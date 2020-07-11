# SpringBoot整合mybatis2.0升级版

在前文[SpringBoot整合Mybatis](https://blog.csdn.net/qq_45077173/article/details/106064752)中简单的将SpringBoot和Mybatis整合了一下。在这里再次总结一下。

**技术栈：**

- SpringBoot
- Mybatis
- thymeleaf

## **项目结构**



![1594456427139](C:\Users\董鹏超\AppData\Roaming\Typora\typora-user-images\1594456427139.png)

### controller

**HelloController**:

```java
package com.test.sq1.controller;

import com.test.sq1.entity.Student;
import com.test.sq1.service.impl.StuServiceImpl;
import net.minidev.json.JSONObject;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.ModelAndView;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

@Controller
@RequestMapping("/student")
public class HelloController {
    @Autowired
    private StuServiceImpl service;

    /**
     * @methodname queryAll
     * @param m
     * @return String
     */
    @RequestMapping(value = "/queryAll",method = RequestMethod.GET)
    public String queryAll( Model m){
        List<Student> list = new ArrayList<>();
        list = service.queryAllStudent();

        /**
         * 添加到视图
         */
        m.addAttribute("list", list);
        return "index";
    }
    @RequestMapping(value = "DelStudent",method = RequestMethod.GET)
    public String delStudent( Model m,String id){
        boolean flag;
        flag=service.delStudent(id);
        if(flag){
            List<Student> list = new ArrayList<>();
            list = service.queryAllStudent();
            /**
             * 添加到视图
             */
            m.addAttribute("list", list);
        }
        return "redirect:queryAll";
    }

    @RequestMapping(value = "UpdStudent",method = RequestMethod.GET)
    public String updStudent(Model m,Student student){
        boolean flag;
        flag=service.updStudent(student);
        if (flag){
            List<Student> list = new ArrayList<>();
            list = service.queryAllStudent();
            /**
             * 添加到视图
             */
            m.addAttribute("list", list);
        }
        return "redirect:queryAll";
    }
    
    @RequestMapping(value = "insertStudent",method = RequestMethod.GET)
    public String insertStudent(Model m, Student student){
        boolean flag;
        flag=service.insertStudent(student);
        if(flag){
            List<Student> list = new ArrayList<>();
            list = service.queryAllStudent();
            /**
             * 添加到视图
             */
            m.addAttribute("list", list);
        }
        return "redirect:queryAll";
    }
    @ApiOperation("查询单个学生信息")
    @RequestMapping(value = "querySingleStudent",method = RequestMethod.GET)
    public String querySingleStudent(Model m, String stuId ){
            Student student = new Student();
        List<Student> list = new ArrayList<>();
            student= service.querySingleStudent(stuId);
        list.add(student);
        System.out.println(student);
            /**
             * 添加到视图
             */
            m.addAttribute("list", list);
        return "single";
    }
}

```

### Entity

**Student：**

```java
package com.test.sq1.entity;


public class Student {

    /**
     * StuID :
     * StuName :
     * StuAge :
     * StuGrade :
     * StuSex :
     */
    private String StuID;
    private String StuName;
    private String StuAge;
    private String StuGrade;
    private String StuSex;

    public String getStuID() {
        return StuID;
    }

    public void setStuID(String StuID) {
        this.StuID = StuID;
    }

    public String getStuName() {
        return StuName;
    }

    public void setStuName(String StuName) {
        this.StuName = StuName;
    }

    public String getStuAge() {
        return StuAge;
    }

    public void setStuAge(String StuAge) {
        this.StuAge = StuAge;
    }

    public String getStuGrade() {
        return StuGrade;
    }

    public void setStuGrade(String StuGrade) {
        this.StuGrade = StuGrade;
    }

    public String getStuSex() {
        return StuSex;
    }

    public void setStuSex(String StuSex) {
        this.StuSex = StuSex;
    }

    public Student() {
        super();
    }

    public Student(String stuID, String stuName, String stuAge, String stuGrade, String stuSex) {
        StuID = stuID;
        StuName = stuName;
        StuAge = stuAge;
        StuGrade = stuGrade;
        StuSex = stuSex;
    }

    @Override
    public String toString() {
        return "Student{" +
                "StuID='" + StuID + '\'' +
                ", StuName='" + StuName + '\'' +
                ", StuAge='" + StuAge + '\'' +
                ", StuGrade='" + StuGrade + '\'' +
                ", StuSex='" + StuSex + '\'' +
                '}';
    }
}

```

### mapper

**StuMapper:**

```java
package com.test.sq1.mapper;

import com.test.sq1.entity.Student;
import org.apache.ibatis.annotations.Mapper;

import java.util.List;

/**
 * @author Cody
 * @date 2020/7/2 - 18:20
 */
@Mapper
public interface StuMapper {
    /**
     * @methodname queryAllStudent
     * @param
     * @return java.util.List<com.test.sq1.entity.Student>
     */
    public List<Student> queryAllStudent();
    /**
     * @methodname querySingleStudent
     * @param stuId
     * @return com.test.sq1.entity.Student
     */
    public Student querySingleStudent (String stuId);
    /**
     * @methodname insertStudent
     * @param student
     * @return boolean
     */
    public boolean insertStudent(Student student);
    /**
     * @methodname UpdStudent
     * @param
     * @param student
     * @return boolean
     */
    public boolean UpdStudent(Student student);
    /**
     * @methodname DelStudent
     * @param
     * @param stuId
     * @return boolean
     */
    public boolean DelStudent(String stuId);
}

```

### Service

**StuService:**

```java
package com.test.sq1.service;
import com.test.sq1.entity.Student;
import java.util.List;

public interface StuService {
    /**
     * 查看所有学生信息
     *
     * @methodname queryAllStudent
     * @param
     * @return java.util.List<com.test.sq1.entity.Student>
     */
    public List<Student> queryAllStudent();
    /**
     *
     * @methodname querySingleStudent
     * @param
     * @param stuId
     * @return com.test.sq1.entity.Student
     */
    public Student querySingleStudent(String stuId);
    /**
     * @methodname insertStudent
     * @param
     * @param student
     * @return boolean
     */
    public boolean insertStudent(Student student);
    /**
     * @methodname updStudent
     * @param
     * @param student
     * @return boolean
     */
    public boolean updStudent(Student student);
    /**
     * @methodname delStudent
     * @param
     * @param stuId
     * @return boolean
     */
    public boolean delStudent(String stuId);
}

```

#### Impl

**StuServiceImpl:**

```java
package com.test.sq1.service.impl;

import com.test.sq1.entity.Student;
import com.test.sq1.mapper.StuMapper;
import com.test.sq1.service.StuService;
import org.springframework.stereotype.Service;

import javax.annotation.Resource;
import java.util.List;


@Service
public class StuServiceImpl  implements StuService {
    @Resource
    public StuMapper stuMapper;
    public StuServiceImpl(){
        super();
    }
    public StuServiceImpl(StuMapper stuMapper){
        this.stuMapper = stuMapper;
    }
    /**
     * @methodname queryAllStudent
     * @param
     * @return java.util.List<com.test.sq1.entity.Student>
     */
    @Override
    public List<Student> queryAllStudent(){
        return stuMapper.queryAllStudent();
    }
    /**
     * @methodname querySingleStudent
     * @param
     * @param stuId
     * @return com.test.sq1.entity.Student
     */
    @Override
    public Student querySingleStudent(String stuId){
        return stuMapper.querySingleStudent(stuId);
    }
    /**
     * @methodname insertStudent
     * @param
     * @param student
     * @return boolean
     */
    @Override
    public boolean insertStudent(Student student){
        return stuMapper.insertStudent(student);
    }
    /**
     * @methodname updStudent
     * @param
     * @param student
     * @return boolean
     */
    @Override
    public boolean updStudent(Student student){
        return stuMapper.UpdStudent(student);
    }
    /**
     * @methodname delStudent
     * @param
     * @param stuId
     * @return boolean
     */
    @Override
    public boolean delStudent(String stuId){
        return stuMapper.DelStudent(stuId);
    }
}

```

### Sq1Application

```java
package com.test.sq1;

import org.mybatis.spring.annotation.MapperScan;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
@MapperScan("com.test.sq1.mapper")
@SpringBootApplication
public class Sq1Application {

    public static void main(String[] args) {
        SpringApplication.run(Sq1Application.class, args);
    }

}

```

### 配置文件

#### StuMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!-- namespace:改mapper.xml映射文件的唯一标识并且必须和数据处理层的接口的路径相同-->
<mapper namespace="com.test.sq1.mapper.StuMapper">
    <!--   必须添加property属性 ，区别于是否加主键-->
    <resultMap id="Student" type="com.test.sq1.entity.Student">
        <id column="stu_id" property="StuID" javaType="String"></id>
        <result column="stu_name" property="StuName" javaType="String"></result>
        <result column="stu_age" property="StuAge" javaType="String"></result>
        <result column="stu_sex" property="StuSex" javaType="String"></result>
        <result column="stu_grade" property="StuGrade" javaType="String"></result>
    </resultMap>
    <insert id="insertStudent" parameterType="Student">
        insert into student values (#{stuID},#{stuName},#{stuAge},#{stuSex},#{stuGrade});
    </insert>
    <update id="UpdStudent" parameterType="Student" >
        update student set stu_grade = #{stuGrade} , stu_age=#{stuAge} where stu_id=#{stuID};
    </update>
    <delete id="DelStudent" parameterType="string" >
        delete from student where stu_id = #{stuID};
    </delete>
    <select id="queryAllStudent" resultType="Student" resultMap="Student">
        select * from student order by stu_id;
    </select>
    <select id="querySingleStudent" resultType="Student" resultMap="Student" parameterType="string">
        select * from student
        <trim suffixOverrides="and"  prefixOverrides="and" >
            <where>
                <if test="stu_id!=null">
                    stu_id=#{stuID};
                </if>
            </where>
        </trim>
    </select>
    <!--id的值必须和数据处理层的接口名一致-->
    <!--此处的User-->

</mapper>
```

#### application.yml

```yaml
server:
  port: 8080
spring:
  thymeleaf:
    cache: false # 关闭页面缓存
    encoding: UTF-8 # 模板编码
  datasource:
    url: jdbc:mysql://localhost:3306/demo?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
    password: 123456
    username: root
    driver-class-name : com.mysql.cj.jdbc.Driver
  mvc:
    static-path-pattern: /**
    view:
      prefix: /WEB-INF/jsp/
      suffix: .jsp
mybatis:
  type-aliases-package: com.test.sq1.entity
  mapper-locations: classpath:mapper/*.xml



```



#### pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.3.1.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.test</groupId>
    <artifactId>sq1</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>sq1</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.1.3</version>
        </dependency>
   
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>bootstrap</artifactId>
            <version>3.3.5</version>
        </dependency>
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>jquery</artifactId>
            <version>3.1.1</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
        <!--引入模板引擎-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <fork>true</fork>
                </configuration>
            </plugin>
        </plugins>
    </build>

</project>

```



### 前端界面

**index.html**:

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
    <title>Springboot整合Mybatis实现CRUD</title>
    
    <link href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap-theme.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css">
    <script src="https://cdn.staticfile.org/jquery/2.1.1/jquery.min.js"></script>
    <script src="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>
</head>
<body>
<div class="container">
    <div class="container">
        <table  cellpadding="0" cellspacing="0" class="table table-striped">
            <thead>
                <tr class="active">
                    <th>学号</th>
                    <th>姓名</th>
                    <th>年龄</th>
                    <th>性别</th>
                    <th>班级</th>
                    <th>操作</th>
                    <th>操作</th>
                </tr>
            </thead>
            <tbody th:each="student ,studentstart: ${list}">
                <tr class="success">
                    <!--<td th:text="${studentstart.index}"></td>-->
                    <td th:text="${student.getStuID()}" ></td>
                    <td th:text="${student.getStuName()}"></td>
                    <td th:text="${student.getStuAge()}"></td>
                    <td th:text="${student.getStuSex()}"></td>
                    <td th:text="${student.getStuGrade()}"></td>
                    <td>
                        <!--
                            controller中逻辑上可能出问题
                            点击更新后出来的个人表单信息只能是第一个人的，并不是跟随id变化
                        -->
                        <button  class="btn btn-default" data-toggle="modal" data-target="#addcase" >更新</button>
                        <div id="addcase" class="modal inmodal" tabindex="-1" role="dialog" aria-hidden="true">
                            <div class="modal-dialog">
                                <form action="/student/UpdStudent" role="form" method="post" th:each="student ,studentstart: ${list}">
                                    <div class="modal-content">
                                        <div class="modal-header">
                                            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                                                <span aria-hidden="true">×</span></button>
                                            <h4 class="modal-title">更新</h4>
                                        </div>
                                        <div class="modal-body">
                                            <div class="form-group">
                                                <label for="inputStuId1" >学生学号：</label>
                                                <input th:value="${student.getStuID()}"  class="form-control" id="inputStuId1"  name="StuID"  type="text" readonly>
                                            </div>
                                            <div class="form-group">
                                                <label for="inputStuName1" >学生姓名：</label>
                                                <input th:value="${student.getStuName()}" class="form-control" id="inputStuName1" name="StuName"  type="text" readonly/>
                                            </div>
                                            <div class="form-group">
                                                <label for="inputStuAge1" class="col-sm-2 control-label">学生年龄：</label>
                                                <input th:value="${student.getStuAge()}"  class="form-control" id="inputStuAge1"  name="StuAge"  type="text" />
                                            </div>
                                            <div class="form-group">
                                                <label for="inputStuSex1" class="col-sm-2 control-label">学生性别：</label>
                                                <input  th:value="${student.getStuSex()}" value=""class="form-control" id="inputStuSex1"  name="StuSex"  type="text" readonly/>
                                            </div>
                                            <div class="form-group">
                                                <label for="inputStuGrade1" class="col-sm-2 control-label">学生班级：</label>
                                                <input th:value="${student.getStuGrade()}" class="form-control" id="inputStuGrade1" name="StuGrade"  type="text" />
                                            </div>
                                        </div>
                                        <div class="modal-footer">
                                            <div class="form-group">
                                                <button type="button" class="btn btn-default pull-left" data-dismiss="modal">关闭</button>
                                                <button type="submit" class="btn btn-primary">更新</button>
                                            </div>
                                        </div>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </td>
                    <!--调用Ajax判断读取-->
                    <td ><a th:href="@{'/student/DelStudent?id='+${student.getStuID()}}">删除</a></td>
                    <!--点击链接后没有反应，必须在刷新一下页面才会出来信息-->
                    <!--<td ><a th:href="@{'/student/querysingleStudent?stuId='+${student.getStuID()}}">查看个人信息</a></td>-->
                </tr>
            </tbody>
            <tfoot>

            </tfoot>
        </table>
    </div>
    <div style="BORDER-RIGHT: 7px ridge;

BORDER-TOP: 7px ridge; BACKGROUND: #ffffff;

BORDER-LEFT: 7px ridge;

 WIDTH: 100%;

 BORDER-BOTTOM: 7px ridge;

 HEIGHT: 100%" align=left >
        <form action="/student/insertStudent" method="get" class="form-horizontal" style="margin-top: 60px;">
            <div class="form-group">
                <label for="inputStuId" class="col-sm-2 control-label">学生学号：</label>
                <div class="col-sm-10">
                    <input value=""  class="form-control" id="inputStuId"  name="StuID" placeholder="请输入学生学号" type="text"/>
                </div>
            </div>
            <div class="form-group">
                <label for="inputStuName" class="col-sm-2 control-label">学生姓名：</label>
                <div class="col-sm-10">
                    <input value="" class="form-control" id="inputStuName" name="StuName" placeholder="请输入学生姓名" type="text"/>
                </div>
            </div>
            <div class="form-group">
                <label for="inputStuAge" class="col-sm-2 control-label">学生年龄：</label>
                <div class="col-sm-10">
                    <input value="" class="form-control" id="inputStuAge"  name="StuAge" placeholder="请输入学生年龄" type="text"/>
                </div>
            </div>
            <div class="form-group">
                <label for="inputStuSex" class="col-sm-2 control-label">学生性别：</label>
                <div class="col-sm-10">
                    <input value=""class="form-control" id="inputStuSex"  name="StuSex" placeholder="请输入学生性别" type="text"/>
                </div>
            </div>
            <div class="form-group">
                <label for="inputStuGrade" class="col-sm-2 control-label">学生班级：</label>
                <div class="col-sm-10">
                    <input value="" class="form-control" id="inputStuGrade" name="StuGrade" placeholder="请输入学生班级" type="text"/>
                </div>
            </div>
            <div class="form-group">
                <div class="col-sm-offset-2 col-sm-10">
                    <button type="submit" class="btn btn-default">新增学生</button>
                </div>
            </div>
        </form>
    </div>

    </div>

</div>
</body>

</html>
```

### 测试

![aixin3](C:\Users\董鹏超\Desktop\aixin3.gif)

### 注意事项：

- 配置mapper文件的时候路径一定要正确
- 修改端口号和数据库以及用户名和密码