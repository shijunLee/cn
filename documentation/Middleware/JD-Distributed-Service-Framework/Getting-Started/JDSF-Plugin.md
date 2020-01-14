# 微服务平台插件说明

## spring cloud 插件说明

* 在您使用京东云微服务平台的时候如果您需要使用京东云微服务平台的`服务治理-服务鉴权`和`部署`功能则需要引用插件 `spring-cloud-jdsf` 系列插件，包括 `spring-cloud-jdsf-auth`和`spring-cloud-jdsf-consul`。按照您使用的 Spring Cloud 版本，来选择对应的插件。

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
```

&emsp;&emsp;引用后服务不需要进行任何配置，所有的认证配置只需要在控制台进行

* 如果您不想使用 JDSF 的服务治理功能，只想使用JDSF 的注册中心和部署功能，可以只配置注册中心的参数即可：  

```yaml
spring:
  cloud:
    consul:
      host: ${JDSF_CONSUL_HOST}
      port: ${JDSF_CONSUL_PORT}
```

* 如果您只想使用注册中心和部署又不想在配置文件中配置环境变量，推荐您引用我们的插件：
  
```xml
    <dependency>
        <groupId>com.jdcloud.jdsf</groupId>
        <artifactId>spring-cloud-jdsf-consul</artifactId>
        <version>${version}</version>
    </dependency>
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

## 插件功能说明

* `spring-cloud-jdsf-consul`: 插件会获取使用微服务平台部署功能部署时候的环境变量，从环境变量中自动查找注册中心地址，替换您配置文件中配置的地址，进行服务注册