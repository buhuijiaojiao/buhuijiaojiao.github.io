# Spring Boot 注解总结 (含代码示例 - 分类版)

## 核心注解

### @SpringBootApplication

* **作用：** Spring Boot 应用入口注解，包含配置、自动配置和组件扫描。

* **使用场景：** 主启动类。

* **示例代码：**

  ```java
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  
  @SpringBootApplication
  public class MyApplication {
      public static void main(String[] args) {
          SpringApplication.run(MyApplication.class, args);
      }
  }
  ```

### @Configuration

* **作用：** 声明一个类为配置类，用于定义 Bean。

* **使用场景：** 定义 Bean、配置应用。

* **示例代码：**

  ```java
  import org.springframework.context.annotation.Bean;
  import org.springframework.context.annotation.Configuration;
  
  @Configuration
  public class AppConfig {
      @Bean
      public MyService myService() {
          return new MyService();
      }
  }
  ```

### @Bean

*   **作用：** 声明一个方法返回的对象为一个 Bean。
*   **使用场景：** 在配置类中创建 Bean。
*   **示例代码：** (见 `@Configuration`示例)

### @Component

* **作用：** 声明一个类为组件，可被自动扫描。

* **使用场景：** 通用组件，可被其他组件依赖。

* **示例代码：**

  ```java
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyComponent {
      // ...
  }
  ```

### @Service

* **作用：** 声明一个类为服务层组件。

* **使用场景：** 业务逻辑处理。

* **示例代码：**

  ```java
  import org.springframework.stereotype.Service;
  
  @Service
  public class MyService {
      // ...
  }
  ```

### @Repository

* **作用：** 声明一个类为数据访问层组件。

* **使用场景：** 数据库操作。

* **示例代码：**

  ```java
  import org.springframework.stereotype.Repository;
  
  @Repository
  public class MyRepository {
      // ...
  }
  ```

### @Controller

* **作用：** 声明一个类为控制器组件。

* **使用场景：** 处理用户请求，返回视图或数据。

* **示例代码：**

  ```java
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.ResponseBody;
  
  @Controller
  public class MyController {
      @RequestMapping("/hello")
      @ResponseBody
      public String hello() {
          return "Hello World!";
      }
  }
  ```

### @RestController

* **作用：** 声明一个类为 RESTful 控制器，返回数据。

* **使用场景：** 构建 API 接口。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class MyRestController {
      @GetMapping("/api/data")
      public String getData() {
          return "Some Data";
      }
  }
  ```

## 依赖注入注解

### @Autowired

* **作用：** 根据类型自动注入 Bean。

* **使用场景：** 依赖注入。

* **示例代码：**

  ```java
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyClient {
      @Autowired
      private MyService myService;
  }
  ```

### @Qualifier

* **作用：** 指定注入哪个 Bean (当有多个相同类型 Bean)。

* **使用场景：** 解决 Bean 注入冲突。

* **示例代码：**

  ```java
  import org.springframework.beans.factory.annotation.Autowired;
  import org.springframework.beans.factory.annotation.Qualifier;
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyClient {
      @Autowired
      @Qualifier("myServiceImpl1")
      private MyService myService;
  }
  ```

### @Resource

* **作用：** 根据名称注入 Bean。

* **使用场景：** 依赖注入。

* **示例代码：**

  ```java
  import javax.annotation.Resource;
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyClient {
      @Resource(name = "myServiceImpl1")
      private MyService myService;
  }
  ```

### @Value

* **作用：** 注入配置文件中的值。

* **使用场景：** 读取配置。

* **示例代码：**

  ```java
  import org.springframework.beans.factory.annotation.Value;
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyConfig {
      @Value("${my.property}")
      private String myProperty;
  }
  ```

## 请求映射注解

### @RequestMapping

* **作用：** 映射 HTTP 请求到处理方法。

* **使用场景：** 通用请求映射。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  @RequestMapping("/api")
  public class MyController {
      @RequestMapping("/data")
      public String getData(){
          return "Data";
      }
  }
  ```

### @GetMapping

* **作用：** 映射 GET 请求。

* **使用场景：** 获取资源。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class MyController {
      @GetMapping("/data")
      public String getData() {
          return "Data";
      }
  }
  ```

### @PostMapping

* **作用：** 映射 POST 请求。

* **使用场景：** 创建资源。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.PostMapping;
  import org.springframework.web.bind.annotation.RequestBody;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class MyController {
      @PostMapping("/data")
      public String createData(@RequestBody String data) {
          return "Created Data: " + data;
      }
  }
  ```

### @PutMapping

* **作用：** 映射 PUT 请求。

* **使用场景：** 更新资源。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.PutMapping;
  import org.springframework.web.bind.annotation.RequestBody;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class MyController {
      @PutMapping("/data")
      public String updateData(@RequestBody String data) {
           return "Updated Data: " + data;
      }
  }
  ```

### @DeleteMapping

* **作用：** 映射 DELETE 请求。

* **使用场景：** 删除资源。

* **示例代码：**

   ```java
   import org.springframework.web.bind.annotation.DeleteMapping;
   import org.springframework.web.bind.annotation.PathVariable;
   import org.springframework.web.bind.annotation.RestController;
  
   @RestController
   public class MyController {
       @DeleteMapping("/data/{id}")
       public String deleteData(@PathVariable Long id) {
          return "Deleted Data with id: " + id;
       }
   }
   ```

### @PatchMapping

* **作用：** 映射 PATCH 请求。

* **使用场景：** 部分更新资源。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.PatchMapping;
  import org.springframework.web.bind.annotation.RequestBody;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class MyController {
      @PatchMapping("/data")
      public String patchData(@RequestBody String data) {
          return "Patched Data: " + data;
      }
  }
  ```

### @PathVariable

* **作用：** 获取 URL 中的路径参数。

* **使用场景：** 获取动态参数。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.PathVariable;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class MyController {
      @GetMapping("/data/{id}")
      public String getData(@PathVariable Long id) {
          return "Data with ID: " + id;
      }
  }
  ```

### @RequestParam

* **作用：** 获取请求参数。

* **使用场景：** 获取查询参数。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RequestParam;
  import org.springframework.web.bind.annotation.RestController;
  
  @RestController
  public class MyController {
      @GetMapping("/data")
      public String getData(@RequestParam String name) {
          return "Data for name: " + name;
      }
  }
  ```

### @RequestBody

*   **作用：** 获取请求体中的数据。
*   **使用场景：** 获取 POST、PUT 请求的数据。
*   **示例代码：** (见 `@PostMapping` 示例)

## AOP 注解

### @Aspect

* **作用：** 声明一个类为切面。

* **使用场景：** 定义 AOP 横切逻辑。

* **示例代码：**

  ```java
  import org.aspectj.lang.annotation.Aspect;
  import org.springframework.stereotype.Component;
  
  @Aspect
  @Component
  public class MyAspect {
      // ... advice methods
  }
  ```

### @Before

* **作用：** 方法执行前执行。

* **使用场景：** 前置通知。

* **示例代码：**

   ```java
   import org.aspectj.lang.annotation.Aspect;
   import org.aspectj.lang.annotation.Before;
   import org.springframework.stereotype.Component;
  
   @Aspect
   @Component
   public class MyAspect {
  
       @Before("execution(* com.example.demo.service.*.*(..))")
       public void beforeAdvice(){
          System.out.println("Before Method");
       }
   }
   ```

### @After

* **作用：** 方法执行后执行。

* **使用场景：** 后置通知。

* **示例代码：**

  ```java
  import org.aspectj.lang.annotation.After;
  import org.aspectj.lang.annotation.Aspect;
  import org.springframework.stereotype.Component;
  
  @Aspect
  @Component
  public class MyAspect {
  
       @After("execution(* com.example.demo.service.*.*(..))")
       public void afterAdvice(){
          System.out.println("After Method");
       }
   }
  ```

### @AfterReturning

* **作用：** 方法成功返回后执行。

* **使用场景：** 返回通知。

* **示例代码：**

   ```java
   import org.aspectj.lang.annotation.AfterReturning;
   import org.aspectj.lang.annotation.Aspect;
   import org.springframework.stereotype.Component;
  
   @Aspect
   @Component
   public class MyAspect {
  
        @AfterReturning(value ="execution(* com.example.demo.service.*.*(..))",returning = "result")
        public void afterReturningAdvice(Object result){
           System.out.println("After Returning Method, Return Value:"+ result);
        }
    }
   ```

### @AfterThrowing

* **作用：** 方法抛出异常后执行。

* **使用场景：** 异常通知。

* **示例代码：**

  ```java
  import org.aspectj.lang.annotation.AfterThrowing;
  import org.aspectj.lang.annotation.Aspect;
  import org.springframework.stereotype.Component;
  
  @Aspect
  @Component
  public class MyAspect {
        @AfterThrowing(value = "execution(* com.example.demo.service.*.*(..))",throwing = "ex")
        public void afterThrowingAdvice(Exception ex){
          System.out.println("After Throwing, Exception :"+ ex.getMessage());
      }
  }
  ```

### @Around

* **作用：** 方法执行前后执行。

* **使用场景：** 环绕通知。

* **示例代码：**

  ```java
  import org.aspectj.lang.ProceedingJoinPoint;
  import org.aspectj.lang.annotation.Around;
  import org.aspectj.lang.annotation.Aspect;
  import org.springframework.stereotype.Component;
  
  @Aspect
  @Component
  public class MyAspect {
      @Around("execution(* com.example.demo.service.*.*(..))")
      public Object aroundAdvice(ProceedingJoinPoint joinPoint) throws Throwable {
          System.out.println("Before Method");
          Object result = joinPoint.proceed();
           System.out.println("After Method");
           return result;
      }
  }
  ```

## 数据校验注解

### @Valid

* **作用：** 开启数据校验。

* **使用场景：** 校验请求参数。

* **示例代码：**

  ```java
  import org.springframework.web.bind.annotation.PostMapping;
  import org.springframework.web.bind.annotation.RequestBody;
  import org.springframework.web.bind.annotation.RestController;
  import javax.validation.Valid;
  
  @RestController
  public class MyController {
      @PostMapping("/data")
      public String createData(@Valid @RequestBody MyData data) {
          return "Data is valid";
      }
  }
  ```

### @NotNull

* **作用：** 验证值不为空。

* **使用场景：** 必填字段。

* **示例代码：**

  ```java
   import javax.validation.constraints.NotNull;
  
   public class MyData{
       @NotNull
       private String name;
   }
  ```

### @NotEmpty

* **作用：** 验证字符串、集合、数组不为空。

* **使用场景：** 必填集合或字符串。

* **示例代码：**

  ```java
  import javax.validation.constraints.NotEmpty;
  import java.util.List;
  public class MyData{
     @NotEmpty
     private String name;
     @NotEmpty
     private List<String> items;
  }
  ```

### @NotBlank

* **作用：** 验证字符串不为空且去空格后不为空。

* **使用场景：** 必填且非空的字符串。

* **示例代码：**

  ```java
  import javax.validation.constraints.NotBlank;
  
  public class MyData{
       @NotBlank
       private String name;
   }
  ```

### @Min

* **作用：** 验证数字最小值。

* **使用场景：** 验证最小值。

* **示例代码：**

  ```java
  import javax.validation.constraints.Min;
  
  public class MyData{
       @Min(1)
       private int age;
   }
  ```

### @Max

* **作用：** 验证数字最大值。

* **使用场景：** 验证最大值。

* **示例代码：**

  ```java
  import javax.validation.constraints.Max;
  
  public class MyData{
       @Max(100)
       private int age;
   }
  ```

### @Email

* **作用：** 验证邮箱格式。

* **使用场景：** 验证邮箱。

* **示例代码：**

  ```java
  import javax.validation.constraints.Email;
  public class MyData{
      @Email
      private String email;
  }
  ```

### @Pattern

* **作用：** 验证字符串是否匹配正则表达式。

* **使用场景：** 复杂格式校验。

* **示例代码：**

  ```java
  import javax.validation.constraints.Pattern;
  public class MyData{
      @Pattern(regexp = "^[a-zA-Z0-9]+$")
      private String username;
  }
  ```

## 其他常用注解

### @EnableScheduling

* **作用：** 开启定时任务功能。

* **使用场景：** 启用定时任务。

* **示例代码：**

  ```java
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.scheduling.annotation.EnableScheduling;
  
  @SpringBootApplication
  @EnableScheduling
  public class MyApplication {
      public static void main(String[] args) {
          SpringApplication.run(MyApplication.class, args);
      }
  }
  ```

### @Scheduled

* **作用：** 定义定时任务。

* **使用场景：** 配置定时任务。

* **示例代码：**

  ```java
  import org.springframework.scheduling.annotation.Scheduled;
  import org.springframework.stereotype.Component;
  
  @Component
  public class MyTask {
      @Scheduled(fixedRate = 5000)
      public void myTask() {
          System.out.println("Running Task");
      }
  }
  ```

### @Transactional

* **作用：** 开启事务管理。

* **使用场景：** 数据库事务。

* **示例代码：**

  ```java
  import org.springframework.stereotype.Service;
  import org.springframework.transaction.annotation.Transactional;
  
  @Service
  public class MyService {
      @Transactional
      public void myTransaction(){
          //... database operation
      }
  }
  ```