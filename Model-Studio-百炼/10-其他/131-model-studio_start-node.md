### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) Start节点使用说明

# Start节点使用说明

更新时间：2026-02-11 02:34:38

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

节点界面

节点说明

配置页面

配置说明

**重要**

为满足更丰富的编排需求，流程编排功能已全面升级为工作流应用和智能体编排应用。流程编排功能将逐步下线，但此变动不影响已经使用了流程编排功能的用户。您可以继续使用流程编排功能，也可以改为使用工作流应用或智能体编排应用，以获得更好的使用体验。具体请参见 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "") 和 [智能体编排应用](https://help.aliyun.com/zh/model-studio/multi-agent-application "")。

本文档主要介绍Start节点使用说明。

## **节点界面**

点击应用中心--流程编排--新建流程，默认 **开始** 节点。开始节点只能拖拽一个，拖拽成功后置灰。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6999850271/p819301.png)

## **节点说明**

Start节点支持两种参数来源：模型识别和业务透传。如果在流程中需要使用该变量，可以直接通过${bizVars.xxx}进行关联。

- **业务透传**：对应SDK调用中的bizParams传入的参数。

- **模型识别**：在调用流程时，大模型自动判断需要传入流程的参数。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6999850271/p819303.png)

## **配置页面**

支持输入string、number、boolean三种类型的参数。该参数可以被后续节点引用到。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6999850271/p819321.png)

## **配置说明**

参数可以按需录入，需要注意的是录入的参数在调用时为必传参数。