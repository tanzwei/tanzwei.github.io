#### 1、什么是Swagger2
Swagger2 是一个规范和完整的框架，用于生成、描述、调用和可视化 RestFul 风格的 Web 服务。它可以快速的帮助我们编写最新的 API 接口文档。
官网文档：[https://swagger.io/docs/specification/2-0/basic-structure/](https://swagger.io/docs/specification/2-0/basic-structure/)
#### 2、Swagger2 的特点

- 及时性（接口变更后，能够及时准确的通知相关前后端开发人员）
- 规范性（保证接口的规范性，如接口的地址，请求方式，参数及响应格式和错误信息）
- 一致性（接口信息一致性，不会因为出现开发人员拿到的文档版本一致，而出现分歧）
- 可测性（直接在接口文档上进行测试，以方便理解业务）
#### 3、常用注解

- @Api：修饰整个类，描述Controller的作用；
- @ApiOperation：描述一个类的一个方法或一个接口；
- @ApiParam：单个参数描述；
- @ApiModel：用对象来接收参数；
- @ApiModelProperty：用对象接收参数时，描述对象的一个字段；
- @ApiImplicitParam：一个请求参数；
- @ApiLmplicitParams：多个请求参数。
### 4、如何使用Swagger2
#### 4.1、引入pom依赖
```java
    	<!--swagger2依赖-->
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger2</artifactId>
            <version>2.9.2</version>
        </dependency>
        <dependency>
            <groupId>io.springfox</groupId>
            <artifactId>springfox-swagger-ui</artifactId>
            <version>2.9.2</version>
        </dependency>
```
#### 4.2、编写配置文件
```java
@Configuration
@EnableSwagger2  //开启swagger
public class SwaggerConfig {

    @Bean
    public Docket createRestApi(){
        return new Docket(DocumentationType.SWAGGER_2)
                //指定构建api文档的详细信息的方法：apiInfo()
                .apiInfo(apiInfo())
                .select()
                //指定生成api接口的包路径，这里把controller作为包路径，生成controller中的所有接口
                .apis(RequestHandlerSelectors.basePackage("com.myself.boot.controller"))
                .paths(PathSelectors.any())
                .build();
    }

    /**
     * 构建api文档的详细信息
     */
    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                //设置页面标题
                .title("Spring Boot 集成Swagger2接口总览")
                //设置接口描述
                .description("简单用构建swagger2")
                //设置联系方式
                .contact("MoYuJian_0826")
                //设置版本
                .version("1.0")
                //构建
                .build();
    }
}
```
4.3、如果配置了拦截器或者SpringSecurity要放行Swagger2
拦截器：
```java
@Configuration
public class AdminWebConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {

        //创建拦截器对象
        registry.addInterceptor(new LoginInterceptor())
                .addPathPatterns("/**")
                .excludePathPatterns("/",
                        "/login",
                        //放行静态资源
                        "/css/**",
                        "/picture/**",
                        //放行swagger相关的
                        "/swagger-ui/**",
                        "/swagger-resources/**",
                        "/v3/api-docs"
                );
    }

}
```
SpringSecurity：
```java
@Override
    protected void configure(HttpSecurity http) throws Exception {
                http
                //其它需要拦截的请求
                //除上面外的所有请求全部不需要认证即可访问
                .anyRequest().permitAll();
    }
```
4.4、如果没有放行swagger或者没有@EnableSwagger2注解，则会出以下错误：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/32486163/1665315620457-4e50ddd4-4726-4ace-97b2-1aa0ca9edd44.png#clientId=u7ada2f05-3195-4&crop=0&crop=0&crop=1&crop=1&from=paste&id=u9c6979a9&margin=%5Bobject%20Object%5D&name=image.png&originHeight=375&originWidth=561&originalType=url&ratio=1&rotation=0&showTitle=false&size=28345&status=done&style=none&taskId=u72a75fb6-4f43-4d64-a705-4171e315d95&title=)
#### 5、在我们要使用swagger的其它工程中的启动类上添加注解
```java
@SpringBootApplication
@EnableSwagger2
@ComponentScan("com.myself.config") //swagger2所在的部分包名
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class,args);
    }
}

```
#### 6、访问路径
http://localhost:8080/swagger-ui.html

完结😝

