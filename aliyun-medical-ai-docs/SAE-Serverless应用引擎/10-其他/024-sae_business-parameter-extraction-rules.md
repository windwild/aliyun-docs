### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[操作指南](https://help.aliyun.com/zh/sae/user-guide/)[运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/)[应用监控](https://help.aliyun.com/zh/sae/application-monitoring-1/)[专业版应用监控](https://help.aliyun.com/zh/sae/monitoring-on-application-professional-edition/)[应用配置](https://help.aliyun.com/zh/sae/application-settings-new/)业务参数提取规则

# 业务参数提取规则

更新时间：2025-05-20 05:23:33

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：监控方法自定义](https://help.aliyun.com/zh/sae/custom-monitoring-methods)[下一篇：收敛设置](https://help.aliyun.com/zh/sae/convergence-settings)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

功能入口

业务参数提取规则

支持范围说明

新增规则

生效验证

管理规则

参数提取规则示例

参数处理步骤最佳实践

常见问题

什么情况下会导致参数提取失败？

异常的提取生效范围？

SpringMVC应用中常见注解的参数提取应该如何配置？

目前不支持的业务参数来源应该如何提取？

自定义参数提取规则是否支持从RequestBodyAdvice和ResponseBodyAdvice修饰过的Body对象中提取？

SAE集成了ARMS的提取特定属性功能，该功能可以无侵入地提取请求和响应中的指定参数，进一步帮助您定位问题根因和追踪请求信息。您可以配置业务参数提取规则，并根据提取出的参数配置自定义错误。

**说明**

- 该功能目前仅支持Java应用。

- 该功能仅限4.1.0及以上版本探针支持，如果您的探针低于该版本，请先 [升级ARMS探针](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/update-the-arms-agent-for-java-applications "")。第一次开启该功能后需要重启应用才可以生效，之后修改配置均可动态生效。


## **功能入口**

1. 在 **应用监控** 页面，选择**应用配置** \> **业务参数提取规则**。

2. 在 **业务参数提取规则** 区域，您可以创建、查看和修改当前应用的业务参数提取规则。

ARMS应用监控探针会动态识别规则变化，并依照所有已启动的规则将业务参数提取出来。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1345045171/p798574.png)

3. 在 **自定义错误设置** 区域，您可以配置自定义错误规则，对提取出来的业务参数值进行过滤。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7656485171/p800931.png)


## 业务参数 **提取规则**

### **支持范围说明**

业务参数提取规则对框架和实际用法有一定要求，支持的类型和来源如下：

| **参数提取类型** | **参数提取来源** | **支持的框架** | **备注** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数提取类型** | **参数提取来源** | **支持的框架** | **备注** |
| HTTP服务端请求 | - Header<br>  <br>- Cookie<br>  <br>- Parameter | - Tomcat 7.0.4+<br>  <br>- Jetty 8.0.0+<br>  <br>- Undertow 1.4.0.Final+ | - |
| Body | SpringMVC 4.2.0+ | 类名需使用@Controller注解标注，且方法入参被@RequestBody注解标注。 |
| HTTP服务端响应 | - Header<br>  <br>- Cookie | - Tomcat 7.0.4+<br>  <br>- Jetty 8.0.0+<br>  <br>- Undertow 1.4.0.Final+ | - |
| Body | SpringMVC 4.2.0+ | 类名需使用@Controller注解标注，且方法被@ResponseBody注解标注。 |
| 异常信息 | Message | - | 对应类需要继承 java.lang.Exception。 |

### **新增规则**

**重要**

- 规则创建完成并启用后将实时下发至客户端探针侧，无需重启应用，预计1~2分钟后开始生效。

- 业务参数被提取后将记录至对应调用链Span的属性Attributes中，可在 **调用链分析** 页面按需筛选查询。

- Attribute名称会默认具有`biz.`前缀，不允许重复。

- Span数据是否上报会受到采样策略影响，您可以通过调整采样策略来保证重要信息被正确上报，更多信息请参见 [调用链采样模式选择（3.2.8以下探针版本）](https://help.aliyun.com/zh/arms/application-monitoring/use-cases/use-trace-sampling-policies "")。

- 如果调用链中无对应的业务参数信息，请检查提取规则的参数是否配置正确。


在 **业务参数提取规则** 区域单击 **新增规则**，填写规则信息并保存。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1345045171/p798578.png)

- **规则名称**：该条规则的可读名称。

- **Attribute名称**：该条规则提取出的值在Span中对应的Attribute名称，默认以biz.开头，后续由多个单词组成，每个单词仅允许由大小写字母、数字、短划线（-）、下划线（\_）组成，单词与单词之间必须有一个半角句号（.）分隔。最多允许存在10个单词。

- **参数提取类型**：需要提取的参数类型。

- **生效接口（HTTP类型）**：该条规则作用的HTTP接口范围，探针仅对匹配成功的接口提取相应参数。

- **异常类名（异常类型）**：该条规则作用的异常类名范围，探针仅对匹配成功的异常提取相应参数。

- **文本编码类型**：待提取参数文本的编码类型。

- **参数提取规则**：定义待提取参数所在的实际载体来源和提取后的处理方式，支持配置多个参数来源和提取步骤。若多个来源均可提取到参数，排序在前的参数提取步骤优先级高于后者。更多信息，请参见 [参数提取规则示例](https://help.aliyun.com/zh/sae/business-parameter-extraction-rules#fd112e607bi2o "")。

  - **参数来源**：待提取参数所在的实际载体来源，对于Header、Cookie、Parameter，需要您填写相应的Key来初步提取，对于Body、Message，则代表载体为整个对象。

  - **参数处理步骤**：流式的参数处理步骤，用于从参数载体中逐步解析出最终的参数值。您可以添加多条参数处理步骤，前者的解析结果会成为后者的输入。如果不添加处理步骤，则提取到的参数值为载体对象的JSON文本。更多信息，请参见 [参数处理步骤最佳实践](https://help.aliyun.com/zh/sae/business-parameter-extraction-rules#d316428145ty4 "")。


    支持的参数处理方式：



    - Ognl：入参要求为Object，支持点表示法的Ognl语句，示例：`#this.data.getCode()`。

    - JsonPath：入参要求为JsonString，支持点表示法的JsonPath语句，示例：`$.data.code`。

    - Regex：入参要求为String，支持基于命名分组的正则表达式语句，待提取的子串对应名为res的分组，示例：`.*from:(?<res>[a-z]+).*`。
- **是否启用**：该条规则是否启用。


### **生效验证**

参数提取规则配置完成后，无需重启应用即可生效。跳转到 **调用链分析** 页面查看相关调用链，如果对应接口的Span Attribute有自定义的Attribute被写入，说明提取规则生效。

1. 找到新增的规则对应的Attribute名称。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1345045171/p798612.png)

2. 在 **调用链分析** 页面添加`attributes.$attributesName`作为查询条件，过滤相关Span。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1345045171/p798614.png)

3. 单击任意一条Trace，在对应的Span下可以看到自定义的Attributes。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1345045171/p798615.png)


### **管理规则**

- 启用/禁用规则：在目标规则右侧设置 **是否启用** 开关。

- 编辑和删除：在目标规则右侧单击 **编辑** 和 **删除**，可以修改或删除对应规则。

- 批量删除：选中需要删除的提取规则，并单击 **批量删除**。

- 批量复制：选中需要复制的提取规则，并单击 **批量复制至其他应用**，在弹窗中选择复制到其他所有应用或者选择指定应用。



**说明**





  - 批量复制至其他应用需要1~2分钟时间生效。

  - 该功能仅复制参数提取规则，其配套的自定义错误不会被复制到目标应用。

  - 参数提取规则要求Attribute名称唯一，如果目标应用已经存在同样的Attribute名称，则该条规则不会被复制到目标应用。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1345045171/p798610.png)

### 参数提取规则示例

#### Ognl

Ognl语句是一种对象访问语言，允许使用者通过表达式获取Java对象中的属性，或者执行Java对象的方法。Ognl作为参数处理方法，允许您对使用了@ResponseBody或者@RequestBody注解标注的Java对象进行提取。提取结果会被转为一个String（如果是对象会被转为Json字符串），便于您做进一步提取。示例：

```java
@RestController
@RequestMapping("/components/api/v1/mall")
public class MallController {
  @RequestMapping("/product")
  @ResponseBody
  public ResponseBody product(@RequestBody RequestBody req) {
    // 您的业务代码
  }

  static class RequestBody {
    String requestId;
    Map<String, String> queryParam;

    public String getQueryJsonStr() {
      return JSON.toJsonString(queryParam);
    }
  }

  static class ResponseBody {
    int code;
    boolean success;
    String message;
  }
}
```

如果您希望提取RequestBody中的requestId字段，可以将提取规则设置如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0853083271/p830995.png)

如果您希望提取ResponseBody中的code字段，可以将提取规则设置如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0853083271/p830997.png)

Ognl支持您调用对象中的get方法来获取字段，如果您希望提取RequestBody中getQueryJsonStr()方法的执行结果，可以将提取规则设置如下。

**重要**

在使用前请保证该类存在该方法。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0853083271/p830998.png)

#### JsonPath

JsonPath语句是一种JSON字符串提取语言，允许使用者通过表达式获取JSON String中的属性。JsonPath作为参数处理方法，允许您对JSON字符串进行提取。示例：

```json
{
  "code": 200,
  "message": "Query success.",
  "success": true,
  "data": {
    "name": "John",
    "age": 21
  }
}
```

如果您希望提取上述JSON中data.age字段，可以将提取规则设置如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0853083271/p831000.png)

#### Regex

Regex语句即正则表达式，用于描述、匹配一系列符合某个句法规则的字符串。Regex作为参数处理方法，允许您对待提取字符串进行正则匹配，并将匹配到的名称为res的分组作为提取结果。示例：

**说明**

正则表达式默认为从头匹配，如果为任意匹配，请在语句前后添加`.*`。

```xml
https://test.aliyun.com/v2/workitem#requestId=0c978f115b6f7&cityCode=34&env=online
```

如果您希望提取上述URL中的cityCode部分，可以将提取规则设置如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0853083271/p831003.png)

#### 实际样例

如下示例为HTTP应用的响应Body对象。

```java
class DemoResponse {
    int code = 200;
    boolean success = true;
    String message = "text content";
    String extraInfo = "{\"id\": 15, \"cityInfo\": \"from:hangzhou,to:beijing\"}";

    public String getExtraInfo() {
        return this.extraInfo;
    }
}
```

如果希望从extraInfo字段中提取cityInfo的from城市名，可以将提取规则设置如下。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7656485171/p800940.png)

探针实际的提取与处理过程如下：

1. 从响应中获取到DemoResponse对象。

2. 执行`#this.getExtraInfo()`语句，获取到extraInfo字段。

3. 执行`$.cityInfo`语句，将extraInfo字段的值当作JsonString解析，并获取到其中的cityInfo字段。

4. 执行`^from:(?<res>[a-z]+).*`语句，将cityInfo字段的值当做String解析，匹配到res命名的分组，即`hangzhou`子串。

5. 把`hangzhou`作为提取结果写入Span的Attribute。


### **参数处理步骤最佳实践**

#### **参数处理原理**

参数处理步骤支持您从参数载体中进一步检索和过滤需要的信息，可以理解为一种流式映射规则，上一步的输出会作为下一步的输入。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2103377471/CAEQQRiBgMDAn5SW.xgiIDM5NzNhYzliYzYyYTQ2YTI4OTVhNTRjMzZmZDllYzk14409991_20240510111234.396.svg)

不同的参数处理方法对输入有一定的要求，如果输入不满足要求，则会直接中止后续流程，把当前结果作为最终值记录下来。

| **参数处理方法** | **输入** | **输出** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **参数处理方法** | **输入** | **输出** |
| Ognl | 任意的Java对象 | String（如果处理结果为一个对象，会序列化为Json字符串） |
| JsonPath | JSON字符串 | String |
| Regex | String | String |

#### **性能开销**

参数处理步骤涉及序列化/反序列化、Java反射、正则匹配等逻辑，是整个业务参数提取环节中性能损耗占比最高的部分，不建议对RT要求高和性能要求高的接口配置过多参数处理步骤。如果您需要对这样的接口进行提取，可以考虑适当地对业务进行改造。

1. 如果安全合规允许，可以考虑在业务中把对应参数直接写入Header等位置。

2. 采用OTelSDK手动将相关参数写入Span的Attribute，具体操作请参见 [通过OpenTelemetry Java SDK为调用链增加自定义埋点](https://help.aliyun.com/zh/arms/application-monitoring/use-cases/use-opentelemetry-sdk-for-java-to-manually-instrument-applications "")。


#### **参数处理语句合法性**

为了保证提取逻辑的安全性，参数处理语句相比开源实现有更严格的限制，详情如下：

| **参数处理方法** | **语法参考** | **额外语法限制** | **正确示例** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **参数处理方法** | **语法参考** | **额外语法限制** | **正确示例** |
| Ognl | [Apache Ognl](https://commons.apache.org/dormant/commons-ognl/language-guide.html) | 仅支持点表示法的字段/方法访问，且调用方法必须以get开头。最大支持的访问深度为10。 | #this.extraInfo.getPid() |
| JsonPath | [JsonPath](https://goessner.net/articles/JsonPath/) | 仅支持点表示法的字段访问。最大支持的访问深度为10。 | $.cityInfo |
| Regex | [Java Regex](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) | 必须有且仅有一个名为res的分组表示被提取的结果。 | ^from:(?<res>\[a-z\]+).\* |

## **常见问题**

### **什么情况下会导致参数提取失败？**

- 如果您的提取来源为Body，请确认您的应用是否使用了SpringMVC，方法所在类是否添加了@Controller注解，以及对应方法和参数是否添加了@RequestBody和@ResponseBody注解。

- 如果您的提取来源为Response中的Cookie，目前仅支持Tomcat 7.0.4-9.x版本、Undertow 1.4.0.Final+版本获取，建议您将提取来源替换为Request中的Cookie。


### 异常的提取生效范围？

Java探针仅会对抛到Span外部的自定义异常进行拦截，对于内部的关键方法，如果需要提取其中的异常信息并标识为错误，可以通过监控方法自定义功能为该方法创建埋点，具体操作请参见 [监控方法自定义](https://help.aliyun.com/zh/arms/application-monitoring/user-guide/monitoring-method-customization "")。

### **SpringMVC应用中常见注解的参数提取应该如何配置？**

当前已支持的SpringMVC注解与相关配置的对应关系如下所示：

| **注解** | **参数提取类型** | **参数** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **注解** | **参数提取类型** | **参数** |
| @RequestParam | HTTP服务端请求 | Parameter |
| @RequestHeader | HTTP服务端请求 | Header |
| @CookieValue | HTTP服务端请求 | Cookie |
| @RequestBody | HTTP服务端请求 | Body |
| @ResponseBody | HTTP服务端响应 | Body |

### 目前不支持的业务参数来源应该如何提取？

您可以通过引入OpenTelemetry SDK为应用添加自定义埋点，并将希望提取的业务参数作为Attributes写入Span。详情请参见 [通过OpenTelemetry Java SDK为调用链增加自定义埋点](https://help.aliyun.com/zh/arms/application-monitoring/use-cases/use-opentelemetry-sdk-for-java-to-manually-instrument-applications "")。

### 自定义参数提取规则是否支持从RequestBodyAdvice和ResponseBodyAdvice修饰过的Body对象中提取？

支持。ARMS探针对Body的提取时机发生在用户定义的BodyAdvice之后，Spring内置的BodyAdvice之前。