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



# 请求内容

使用`RequestBody`获得请求内容

```java
public ResponseEntity<Object> createProduct(@RequestBody Product product) {
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