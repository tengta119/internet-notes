


# bug

## 后端

### 依赖问题

![](attachments/Pasted%20image%2020251106214353.png)

### 微信 http 请求的路径

![](attachments/Pasted%20image%2020251109202416.png)

在使用内网穿透的情况下，如果不加这个 '/'，微信无法将请求发送到本地

### StringRedisTemplate

![](attachments/Pasted%20image%2020251112172507.png)

如果名字不是 `stringRedisTemplate` 就会报错


### 预检请求（OPTIONS 方法）

![](attachments/Pasted%20image%2020251113194633.png)

OPTIONS 预检请求，

### CORS

![](attachments/Pasted%20image%2020251113201106.png)

![](attachments/Pasted%20image%2020251113201119.png)

`@CrossOrigin("*")` 会与 过滤器发生冲突

### **客户端请求的 `Content-Type` 与服务器接口期望的类型不匹配**

![](attachments/Pasted%20image%2020251115160935.png)

![](attachments/Pasted%20image%2020251115161106.png)

```
Resolved [org.springframework.web.HttpMediaTypeNotSupportedException: Content-Type 'application/x-www-form-urlencoded;charset=UTF-8' is not supported]
```

### 不同包下的类重名

![](attachments/Pasted%20image%2020251119163145.png)

### 参数绑定错误 @RequestParam("file")

![](attachments/Pasted%20image%2020251120200359.png)

```
Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed: java.lang.IllegalArgumentException: Name for argument of type [org.springframework.web.multipart.MultipartFile] not specified, and parameter name information not available via reflection. Ensure that the compiler uses the '-parameters' flag.] with root cause

java.lang.IllegalArgumentException: Name for argument of type [org.springframework.web.multipart.MultipartFile] not specified, and parameter name information not available via reflection. Ensure that the compiler uses the '-parameters' flag.
```

**错误原因简述：** Java 编译器默认不会将**方法的参数名称**保留在编译后的 `.class` 文件中。Spring MVC 在处理请求时（例如上传文件 `MultipartFile`），如果你的代码中没有显式指定参数名，它会尝试通过反射获取参数名。如果编译器没有保留参数名（即未使用 `-parameters` 标志），Spring 就无法知道参数叫什么，从而抛出此异常。


## 前端

### `Promise` 对象

![](attachments/Pasted%20image%2020251113204634.png)