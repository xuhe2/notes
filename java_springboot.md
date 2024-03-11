# 配置应用程序属性

在文件`src/main/resources/application.properties`

```java
server.port = 9090
spring.application.name = project_name
```



# controller

用来控制处理请求代码

```java
@SpringBootApplication
@ComponentScan("com.example.demo.other")
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}

@Controller
public class UserController {

    @RequestMapping("/users")
    public List<User> getAllUsers() {
        // ...
    }

}

```

* `controller`的信息不需要在`application`注册,可以直接使用(会被spring boot scan)



## 配置`prefix`

```java
@RequestMapping("/auth")
public class xxxx
```



## 请求处理

```java
@PostMapping(value = "/login")
```

可以快捷指定请求的方式



# 请求内容

使用`RequestBody`获得请求内容

```java
public ResponseEntity<Object> createProduct(@RequestBody Product product) {
}
```



## 分析请求内容

使用`@RequestBody`实现

```java
    @PostMapping(value = "/login")
    public LoginResponse login(@RequestBody Users requestBody) {
        // 验证用户名和密码
        // 返回登录成功或失败的信息
        System.out.println(requestBody);
        return LoginResponse.success(5);
    }
```

* 接受的参数应该是一个POJO



## 类型名字大小写不匹配

在JSON化的时候特殊处理, 使用`Jackson`的注解

```java
@Data
public class Users {
    private String id;
    @JsonProperty("Name")
    private String name;
    @JsonProperty("Password")
    private String password;
}

```





# 回传数据

使用`ResponseEntity`实现

```java
@RestController
public class ProductServiceController {
   private static Map<String, Product> productRepo = new HashMap<>();
   static {
      Product honey = new Product();
      honey.setId("1");
      honey.setName("Honey");
      productRepo.put(honey.getId(), honey);
      
      Product almond = new Product();
      almond.setId("2");
      almond.setName("Almond");
      productRepo.put(almond.getId(), almond);
   }
   @RequestMapping(value = "/products")
   public ResponseEntity<Object> getProduct() {
      return new ResponseEntity<>(productRepo.values(), HttpStatus.OK);
   }
}
```

* 可以使用`HashMap`作为回传的内容



# 异常处理

全局代码错误处理,使用`@ControllerAdvice`申明类

使用`ExceptionHandler`实现方法

```java
@ControllerAdvice
public class ProductExceptionController {
   @ExceptionHandler(value = ProductNotfoundException.class)
   public ResponseEntity<Object> exception(ProductNotfoundException exception) {
      return new ResponseEntity<>("Product not found", HttpStatus.NOT_FOUND);
   }
}
```



# 拦截器

使用拦截器之前需要使用`@Component`类,并且需要实现`HandleInterceptor`接口

- **preHandle()** 方法 − 这用于在将请求发送到控制器之前执行操作。 此方法应返回 true 以将响应返回给客户端。
- **postHandle()** 方法 − 这用于在向客户端发送响应之前执行操作。
- **afterCompletion()** 方法 − 这用于在完成请求和响应后执行操作。



您必须使用 **WebMvcConfigurerAdapter** 向 **InterceptorRegistry** 注册此拦截器



# 文件配置

存在`properties`和`yml`配置文件

* `yml`配置文件的层次更加清晰



## 读取配置文件

使用`@Value`配置我的变量

```java
@Value("${user.name}")
    private String name;
```



使用`@ConfigurationProperties(prefix = "XXX")`

* 需要设置`setter`,`getter`
* 使用第三方插件自动创建`setter`,`getter`



# 数据库

使用`mybatis-plus-ext`实现



* 使用基于`mybatis-plus`的库需要在`application`中加入注解`@MapperScan("com.xuhe.to_do_java.model.mapper")`



编写POJO类

```java
package com.xuhe.to_do_java.model.pojo;

import lombok.Data;


@Data
public class Users {
    private String id;
    private String name;
    private String password;
}

```

* 注意, POJO类的名字需要和表明一致
* 需要实现`getter`和`setter`的功能



编写`Mapper`类

```java
package com.xuhe.to_do_java.model.mapper;


import com.baomidou.mybatisplus.core.mapper.BaseMapper;
import com.xuhe.to_do_java.model.pojo.Users;

public interface UserMapper extends BaseMapper<Users> {

}

```

> 只需要在这个类中继承`BaseMapper`的类, 其他不需要操作



在其他文件中使用的时候需要使用`Autowired`实现DI

```java
package com.xuhe.to_do_java.controller;

import com.xuhe.to_do_java.model.mapper.UserMapper;
import com.xuhe.to_do_java.model.pojo.Users;
import lombok.Data;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@Data
public class HelloWorld {

    @Autowired
    private UserMapper userMapper;

    @RequestMapping("/query")
    public Users query(int id) {
        return userMapper.selectById(id);
    }
}

```



## 加入新的数据

使用`insert`方法实现



## 查询复杂数据

使用`QueryWrapper`

```java
List<Users> users = usersMapper.selectList(new QueryWrapper<Users>().eq("name",requestBody.getName()));
```

* 返回值是`List`
* 没有查找的时候返回空数组



# 导入第三方Bean

使用`@Import`实现导入

可以使用`@ImportSelector`实现一次导入多个(需要一个接口)

可以新建一个`common.imports`配置文件, 然后使用代码加载加入文件



# 自动配置

一些`starter`在加入配置之后, 会在启动的时候自动往IOT容器中加入Bean

* 需要编写相关的`imports`文件



# 实践



## 定义返回数据类

使用泛型实现

* 需要使用全参数构造函数和无参数构造函数

> 添加
>
> ```java
> @NoArgsConstructor
> @AllArgsConstructor
> ```



创建一个用于回复的POJO类

```java
package com.xuhe.to_do_java.user.model.pojo;

import lombok.AllArgsConstructor;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class LoginResponse {
    private Boolean is_exist;
    private int user_id;

    public static LoginResponse success(int user_id){
        return new LoginResponse(true, user_id);
    }


    public static LoginResponse failure(){
        // 用户不存在
        return new LoginResponse(false, -1);
    }
}

```

* 需要使用`getter`,`setter`



## 日志

使用`@Slf4j`(默认)

```java
@RestController
@CrossOrigin
@RequestMapping("/auth")
@Slf4j
public class AuthController {

    @Autowired
    private UsersMapper usersMapper;

    @PostMapping(value = "/login")
    public LoginResponse login(@RequestBody Users requestBody) {
        // 验证用户名和密码
        // 返回登录成功或失败的信息
        List<Users> users = usersMapper.selectList(new QueryWrapper<Users>().eq("name",requestBody.getName()));
        log.info("users:{}",users);
        return LoginResponse.success(5);
    }
}

```



## JWT

使用`base64`处理

分成`header`,`payload`,`signature`三个部分



## 文件处理



### 文件上传

在`.yml`文件中配置上传地址和文件的大小

```properties
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/to_do
    username: root
    password:
  servlet:
    multipart:
      location: /files
```

* 如果文件夹不存在,会自动创建对应的文件夹

> 保存在`/resources/files`文件夹下	



接受参数

```java
public UploadResponse upload(@RequestParam("file") MultipartFile file) {
```



保存文件

```java
// store file
file.transferTo(new File(fileStorageLocation + file.getOriginalFilename()));
```

