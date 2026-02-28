### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) API调用节点说明

# 流程编排 API 调用节点说明

更新时间：2026-02-11 02:34:45

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

节点界面

节点说明

配置页面

配置说明

输入变量的方法

（1）手工输入

（2）联想提示

结果获取方法

**重要**

为满足更丰富的编排需求，流程编排功能已全面升级为工作流应用和智能体编排应用。流程编排功能将逐步下线，但此变动不影响已经使用了流程编排功能的用户。您可以继续使用流程编排功能，也可以改为使用工作流应用或智能体编排应用，以获得更好的使用体验。具体请参见 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "") 和 [智能体编排应用](https://help.aliyun.com/zh/model-studio/multi-agent-application "")。

本文档主要介绍API调用节点的使用。

## **节点界面**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6027788271/p858893.png)

## **节点说明**

API调用节点允许您的AI应用使用HTTP/HTTPS协议与外部服务进行通信，以便与外部数据和功能进行集成和交互。

## **配置页面**![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6027788271/p858886.png)

## **配置说明**

API节点目前支持最常用的HTTP协议方法：GET和POST。URL地址需要附带HTTP或HTTPS协议头。API节点允许配置输入参数，并支持动态传入请求头，如上图所示。

> 请注意，API节点不支持`application/x-www-form-urlencoded`类型的POST请求。建议您使用 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "") 来完成该任务。

## **输入变量的方法**

### **（1）手工输入**

根据 [变量类型](https://help.aliyun.com/zh/model-studio/definition-and-values-of-process-variables "") 的不同，从相应的结果中获取，形如${bizVars.abc}，如果输入不在${}内，会被识别为常量。

### **（2）联想提示**

在界面输入/，会弹出提示，直接选中变量即可，选中后与手工输入一样。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8089676071/p763655.png)

## **结果获取方法**

为了减少您的配置工作，API节点不需要定义输出参数的格式。具体取值方式如下，假设当前节点的ID为`Api_xxx`。

- **JSON对象返回值：**

当返回的数据是一个JSON对象（例如：`{"a":1,"b":"cc"}`），后续节点可以通过表达式`${svcVars.Api_xxx.response.a}`获取其中的字段`a`。

- **JSON数组返回值：**

如果返回的数据是一个JSON数组（例如：`[{"a":1},{"a":3,"b":"cc"}]`），后续节点可以使用`${svcVars.Api_xxx.response.list[0].a}`获取第一条数据中的字段`a`。如果需要获取所有数据中的字段`a`，则使用`${svcVars.Api_xxx.response.list.a}`。（`list`是默认的一级键值）

- **非JSON返回值：**

对于非JSON格式的返回值（例如："这个问题怎么样"），后续节点可以通过`${svcVars.Api_xxx.response.text}`获取完整的数据。（`text`是默认的一级键值）


通过这些方式，您可以方便地从不同类型的返回值中提取所需信息。