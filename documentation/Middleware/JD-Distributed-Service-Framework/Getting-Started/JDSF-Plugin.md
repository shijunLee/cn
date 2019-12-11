# 微服务平台插件说明

## spring cloud 插件说明

* 在您使用京东云微服务平台的时候如果您需要使用京东云微服务平台的`服务治理`和`部署`功能则需要引用插件 `spring-cloud-jdsf` 系列插件，包括 `spring-cloud-jdsf-auth`、`spring-cloud-jdsf-consul`和`spring-cloud-jdsf-route`。按照您使用的 Spring Cloud 版本，来选择对应的插件。

&emsp;&emsp;如果您使用的springcloud版本为 `Edgware` 则需要引用：

```
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-auth</artifactId>
        <version>1.1.0-Edgware</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>1.1.0-Edgware</version>
    </dependency>
     <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-route</artifactId>
        <version>1.1.0-Edgware</version>
    </dependency>
```

&emsp;&emsp;如果使用的springcloud版本为 `Finchley` 版本则需要引用：

```
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-auth</artifactId>
        <version>1.1.0-Finchley</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>1.1.0-Finchley</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-route</artifactId>
        <version>1.1.0-Finchley</version>
    </dependency>
```

&emsp;&emsp;如果使用的为 `Greenwich` 版本则需要引用

```
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-auth</artifactId>
        <version>1.1.0-Greenwich</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>1.1.0-Greenwich</version>
    </dependency>
     <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-route</artifactId>
        <version>1.1.0-Greenwich</version>
    </dependency>
```

&emsp;&emsp;引用后服务不需要进行任何配置，所有的认证配置只需要在控制台进行

* 如果您不想使用 JDSF 的服务治理功能，只想使用JDSF 的注册中心和部署功能，可以只配置注册中心的参数即可：  

```
spring:
  cloud:
    consul:
      host: ${JDSF_CONSUL_HOST}
      port: ${JDSF_CONSUL_PORT}
```

* 如果您只想使用注册中心和部署又不想在配置文件中配置环境变量，推荐您引用我们的插件：
  
```
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>${version}</version>
    </dependency>
```  

## 插件功能说明

* `spring-cloud-jdsf-consul` 插件会获取使用微服务平台部署功能部署时候的环境变量，从环境变量中自动查找注册中心地址，替换您配置文件中配置的地址，进行服务注册

* `spring-cloud-jdsf-auth` 请求鉴权插件，支持服务之间调用认证设置，引用以后需要在启动类上面使用注解 `@EnableJdsfAuth` 标签才能开启鉴权功能的自动配置，需要注意的是如果项目使用了 spring-webflux 框架的应用需要import 的 class 为 `com.jdcloud.jdsf.auth.annotation.reactive.EnableJdsfAuth`,请在使用的时候注意一下。开启以后会根据您在控制台配置的规则进行鉴权操作。

* `spring-cloud-jdsf-route` 路由功能插件，可以在控制台配置路由规则，插件会按照响应的规则进行路由，只要引用插件以后就会自动的配置开启路由功能，如果您在控制台没有配置路由规则，默认会按照 Spring Cloud 的原始实现进行路由，如果配置了当前服务可用的规则，会按照规则进行路由。
&emsp;&emsp;路由规则默认的刷新时间为`10s`,可以通过如下配置进行修改：

```
   spring.cloud.jdsf.route.ttlValue=10
```

