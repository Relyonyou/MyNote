# JavaWeb

```java
		map.put("status", "error");
		map.put("msg", "验证码错误");
		JSONObject json = JSONObject.fromObject(map);//将map的数据转化为json格式
		//把json数据响应给浏览器 把json数据输出给浏览器
		response.getWriter().print(json);
		map本来就是kv对，Json的数据格式也是kv对
```

request.setAttribute();

request.getAttribute();

