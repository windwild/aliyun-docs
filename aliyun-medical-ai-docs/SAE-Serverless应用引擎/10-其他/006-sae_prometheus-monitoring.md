### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)Prometheus监控

# Prometheus监控

更新时间：2025-11-18 04:46:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：收敛设置](https://help.aliyun.com/zh/sae/convergence-settings)[下一篇：告警管理](https://help.aliyun.com/zh/sae/alert-management-overview2-0/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

1\. 代码埋点

2\. 部署应用

3\. 开启Prometheus监控

SAE应用能够将程序中自定义的监控指标采集到 [可观测监控 Prometheus 版](https://help.aliyun.com/zh/arms/prometheus-monitoring/product-overview/what-is-prometheus "")。您仅需在代码中进行监控指标埋点，应用部署到SAE后开启Prometheus监控，即可实现自动采集监控指标。

**说明**

Prometheus监控仅适用于SAE应用标准版、专业版。

## **1\. 代码埋点**

以Spring Boot应用为例，采用Micrometer框架收集应用程序的监控指标，通过引入Actuator和Prometheus依赖来暴露指标端点，供Prometheus自动采集。

1. 引入Actuator和Prometheus依赖：















```xml
# pom.xml

...
   	<dependencies>
   		<!-- Actuator依赖 -->
   		<dependency>
   			<groupId>org.springframework.boot</groupId>
   			<artifactId>spring-boot-starter-actuator</artifactId>
   		</dependency>
   		<!-- Prometheus依赖 -->
   		<dependency>
   			<groupId>io.micrometer</groupId>
   			<artifactId>micrometer-registry-prometheus</artifactId>
   		</dependency>
   	</dependencies>
...
```

2. 配置采集端口和指标标签：















```properties
# src/main/resources/application.properties

# 服务器端口配置
# 设置Spring Boot应用监听的端口号为8080
server.port=8080

# 应用名称配置
# 设置应用的名称，该名称会在监控指标中作为标签使用
spring.application.name=frontend

# Actuator管理端口配置
# 设置管理端点使用独立的端口8091，与主应用端口分离，提高安全性
management.server.port=8091

# Actuator端点暴露配置
# '*' 表示暴露所有可用的管理端点，包括health、info、metrics以及prometheus等
# 引入micrometer-registry-prometheus依赖后，会暴露/actuator/prometheus端点用于监控指标采集
management.endpoints.web.exposure.include=*

# 监控指标标签配置
# 将应用名称作为统一标签添加到所有指标中，便于在监控系统中区分不同应用的指标
management.metrics.tags.application=${spring.application.name}
```

3. 通过Micrometer自定义监控指标：















```java
// src/main/java/com/example/webframework/WebFrameworkApplication.java

import io.micrometer.core.annotation.Timed;
...
       @GetMapping("/")
       // 本例将请求当前路径的响应定义为监控指标，详见https://javadoc.io/doc/io.micrometer/micrometer-core/1.3.1/io/micrometer/core/annotation/Timed.html，其他指标埋点方法请参考相应的API。
       @Timed(value = "main_page_request_duration", description = "Time taken to return main page", histogram = true)
       public ResponseEntity<String> welcome() {...}
...
```


## **2\. 部署应用**

将应用打包为JAR包后，部署到SAE。 [示例JAR包](https://help-static-aliyun-doc.aliyuncs.com/file-manage-files/zh-CN/20250730/bnhuat/webframework.jar) 可供快速部署和测试验证：

1. 在[SAE应用列表](https://saenext.console.aliyun.com/cn-hangzhou/app-list/micro)中，在顶部选择目标地域和命名空间，点击 **创建应用**。

1. 自定义 **应用名称**。

2. **应用部署方式** 选择 **代码包部署**，点击 **设置代码包部署**。

      1. **技术栈语言** 选择 **Java**。

      2. **代码包类型** 选择 **JAR包部署**。

      3. **Java环境** 根据代码中的Java版本来选择，示例JAR包需要选择 **Open JDK 8**。

      4. 在 **上传JAR包** 区域，上传实际应用打包后的JAR包或示例JAR包。
2. 点击一键创建应用，等待应用创建完成。


## **3\. 开启Prometheus监控**

1. 在[SAE应用列表](https://saenext.console.aliyun.com/cn-hangzhou/app-list/micro)中，在顶部选择目标地域和命名空间，点击目标 **应用ID** 跳转到应用详情页。

2. 点击 **Prometheus监控**，点击 **配置Prometheus监控**，开启 **Prometheus 监控**。

1. **采集间隔（秒）** 可自定义，例如`10`。

2. **目标端口** 设置为`8091`。

3. **指标路径** 设置为`/actuator/prometheus`。
3. 等待Prometheus监控配置生效，再次点击 **Prometheus监控** 跳转到Prometheus监控的 **实例列表**。

4. 点击**指标管理** \> **指标探索**。在查询框中输入自定义的监控指标名称，例如示例代码中的`main_page_request_duration`，根据 **智能提示** 选择需要查看的监控指标，选择 **时间范围**，点击 **执行查询**，显示监控指标的图表，表明配置成功。