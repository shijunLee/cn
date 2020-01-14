# 微服务平台插件说明

## spring cloud 插件说明

* 在您使用京东云微服务平台的时候如果您需要使用京东云微服务平台的`服务治理-服务鉴权`和`部署`功能则需要引用插件 `spring-cloud-jdsf` 系列插件，包括 `spring-cloud-jdsf-auth`和`spring-cloud-jdsf-consul`。按照您使用的 Spring Cloud 版本，来选择对应的插件。

* `spring-cloud-jdsf-consul`: 插件会获取使用微服务平台部署功能部署时候的环境变量，从环境变量中自动查找注册中心地址，替换您配置文件中配置的地址，进行服务注册
* `spring-cloud-jdsf-auth`:服务鉴权插件，如果您需要使用服务鉴权功能，请在控制台添加配置，然后在服务中引用插件。在 spring cloud 启动类上面添加注解`@EnableJdsfAuth`,需要注意的是，如果您使用的是`Spring WebFlux`框架开发的应用请使用`com.jdcloud.jdsf.auth.annotation.reactive.EnableJdsfAuth` 这个annotation,如果您使用的是普通的`Spring WebMVC` 请使用`com.jdcloud.jdsf.auth.annotation.EnableJdsfAuth`这个annotation。
* `spring-cloud-jdsf-route`: 京东云微服务平台路由插件，当引用插件的时候会自动的开启路由功能，默认情况下您如果没有在京东云微服务控制台配置路由规则的时候，服务路由功能不会生效，只有在开启的情况下才会生效。需要注意的是目前在使用`Spring WebFlux` 框架的时候，当前是不支持使用`RestTemplate` or `AsyncRestTemplate`进行请求路由，需要使用 `WebClient`.当您使用路由功能的时候必须使用京东云微服务平台的部署功能和注册中心插件(`spring-cloud-jdsf-consul`).

&emsp;&emsp;如果您使用的springcloud版本为 `Edgware` 则需要引用：

```xml
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-auth</artifactId>
        <version>1.1.2-Edgware</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>1.1.2-Edgware</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-route</artifactId>
        <version>1.1.2-Edgware</version>
    </dependency>
```

&emsp;&emsp;如果使用的springcloud版本为 `Finchley` 版本则需要引用：

```xml
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-auth</artifactId>
        <version>1.1.2-Finchley</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>1.1.2-Finchley</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-route</artifactId>
        <version>1.1.2-Finchley</version>
    </dependency>
```

&emsp;&emsp;如果使用的为 `Greenwich` 版本则需要引用

```xml
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-auth</artifactId>
        <version>1.1.2-Greenwich</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>1.1.2-Greenwich</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-route</artifactId>
        <version>1.1.2-Greenwich</version>
    </dependency>
```

&emsp;&emsp;如果使用的为 `Hoxton` 版本则需要引用

```xml
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-auth</artifactId>
        <version>1.1.2-Hoxton</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>1.1.2-Hoxton</version>
    </dependency>
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-route</artifactId>
        <version>1.1.2-Hoxton</version>
    </dependency>
```

* 如果您不想使用 JDSF 的服务治理功能，只想使用JDSF 的注册中心和部署功能，可以只配置注册中心的参数即可：  

```yaml
spring:
  cloud:
    consul:
      host: ${JDSF_CONSUL_HOST}
      port: ${JDSF_CONSUL_PORT}
```

## dubbo 插件说明

* `dubbo-registry-consul`: dubbo consul 注册中心插件，适配于 dubbo 2.7.x 版本，在使用京东云微服务平台部署功能时能自动的获取注册中心地址，在开发的时候可以正常的使用配置文件配置注册中心地址，插件信息如下：
  
```xml

<dependency>
    <groupId>com.jdcloud.jdsf</groupId>
    <artifactId>dubbo-registry-consul</artifactId>
    <version>1.0.0</version>
</dependency>

```

* `dubbo-opentracing`: dubbo opentracing 插件支持在 dubbo 2.7.x 版本，基于opentracing标准实现开发的，在使用中需要配置基于 Opentracing 的标准 trace 实现才能使用，插件信息如下：

```xml

<dependency>
    <groupId>com.jdcloud.jdsf</groupId>
    <artifactId>dubbo-opentracing</artifactId>
    <version>1.0.0</version>
</dependency>

```

&emsp;&emsp;在使用的时候需要配置 tracing 的 bean，详细信息可以查看[jdsf-demo-dubbo](https://github.com/jdcloud-cmw/jdsf-demo-dubbo)

* 如果您使用的是 dubbo 2.6.x 版本的请联系客服获取插件，稍后 2.6.x 版本的插件会发布到京东云的公共仓库中。



