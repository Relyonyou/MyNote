# SpringBoot实现文件上传

**知识点：**

- input标签（文件类型）
- SpringBoot
- MultipartFile类
- File

## 编写entity

**==Message类==**

```java
package com.xxx.entity;

public class Message {
    //0表示成功;-1表示失败
    int status;
    //向前端返回的内容
    String massage;
    public int getStatus() {
        return status;
    }

    public void setStatus(int status) {
        this.status = status;
    }

    public String getMassage() {
        return massage;
    }

    public void setMassage(String massage) {
        this.massage = massage;
    }

    public Message() {
        super();
    }
    public Message(int status, String massage) {
        super();
        this.status = status;
        this.massage = massage;
    }
}

```

## 编写Controller

**==FileController==**:

```java
package com.xxx.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class FileController {
    @RequestMapping("/picUpload")
    public String picUpload(){
        /**
         * 跳转到picUpload.html
         */
        return "picUpload";
    }
}

```



**==FileUploadController==**:

```java
package com.xxx.controller;

import com.test.sq1.entity.Message;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.multipart.MultipartFile;
import java.io.File;
import java.io.IOException;
import java.util.UUID;

@RestController
public class FileUploadController {
    @PostMapping("/upload")
    public Object upload(@RequestParam("fileUpload") MultipartFile  fileUpload){
        /**
         * getOriginalFilename():得到原来的文件名在客户机的文件系统名称
         */
        String filename = fileUpload.getOriginalFilename();
        String suffixName = filename.substring(filename.lastIndexOf("."));
        /**
         * UUID.randomUUID():生成唯一标识码
         */
        filename = UUID.randomUUID() + suffixName;
        String filepath="F:/sq1/src/main/resources/static";
        try {
         /**
          * transferTo(new File(filepath+filename)):将MultipartFile转化为文件类型
          */
            fileUpload.transferTo(new File(filepath+filename));
            return new Message(0,filename+"上传成功");
        } catch (IOException e) {
            e.printStackTrace();
            return new Message(1,filename+"上传失败");
        }
    }
}
```

## 编写前端界面



**==picUpload.html==**:

```html
<!DOCTYPE html>
<html lang="en" >
<head>
    <meta charset="UTF-8">
    <title>文件上传</title>
    <link href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <link href="https://cdn.bootcss.com/twitter-bootstrap/3.3.7/css/bootstrap-theme.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdn.staticfile.org/twitter-bootstrap/3.3.7/css/bootstrap.min.css">
</head>
<body>
<div class="container">
    <div class="container">
    <form enctype="multipart/form-data" method="post" action="/upload" class="form-horizontal">
        <div class="form-group">
            <label for="fileUpload" class="col-sm-2 control-label">文件：</label>
            <div class="col-sm-10">
                <input type="file" id="fileUpload" class="form-control"name="fileUpload"/>
            </div>
        </div>
        <div class="form-group">
            <div class="col-sm-offset-2 col-sm-10">
                <button type="submit" class="btn btn-default">上传</button>
            </div>
        </div>
    </form>
    </div>
</div>
</body>
</html>
```

## 测试



![在这里插入图片描述](https://img-blog.csdnimg.cn/20200711161913470.gif#pic_center)

## 结束

怎么样，你学会了吗？

So easy！妈妈再也不用担心我的学习。

今天进步**"亿"**点点

