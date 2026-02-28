### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 函数计算节点使用说明

# 函数计算节点使用说明

更新时间：2026-02-11 02:34:52

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：大模型服务平台百炼](https://help.aliyun.com/zh/model-studio/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

节点界面

节点说明

授权说明

配置页面

函数节点配置说明

函数计算创建及使用

函数计算的出参

**重要**

为满足更丰富的编排需求，流程编排功能已全面升级为工作流应用和智能体编排应用。流程编排功能将逐步下线，但此变动不影响已经使用了流程编排功能的用户。您可以继续使用流程编排功能，也可以改为使用工作流应用或智能体编排应用，以获得更好的使用体验。具体请参见 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "") 和 [智能体编排应用](https://help.aliyun.com/zh/model-studio/multi-agent-application "")。

本文档主要介绍函数计算节点的使用。

## **节点界面**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7689676071/p765442.png)

## **节点说明**

阿里云百炼平台提供函数计算节点，借助阿里云函数计算（FC）能力，旨在为开发者提供更丰富的代码开发能力。利用阿里云的服务关联角色，在用户授权后，可以拉取用户的函数列表，同时也可以调用指定的函数，来完成自定义代码在流程内的应用。

## **授权说明**

如果函数计算没有进行过授权，函数计算节点会置灰不可拖动，需要先进行授权。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6689676071/p765443.png)

点击授权后，会弹出授权说明。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7689676071/p765444.png)授权后，函数计算节点可拖动。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7689676071/p765445.png)关于服务关联角色的介绍以及角色如何删除，可以参考 [服务关联角色](https://help.aliyun.com/zh/model-studio/bailian-service-linked-role "")。

## **配置页面**

### **函数节点配置说明**![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6689676071/p764212.png)

如上图，【region】是用户函数计算服务所对应的区域，当前仅支持杭州和北京。当切换region后，【函数名称】对应的列表会获取相应region下的所有函数名称进行展示，最终选取待调用的函数即可。

【输入参数设置】，用于函数调用时透传参数。如图举例，函数计算中需要两个参数，cityParam和dateParam，需要将业务入参中的city和date参数传给相应的参数，可以像图中一样进行配置。【输出参数设置】用于定义函数计算结果放入结果集合中的key，方便后续节点获取函数计算的结果。输入输出参数的取值逻辑可以参考 [流程变量含义及取值方式说明](https://help.aliyun.com/zh/model-studio/definition-and-values-of-process-variables "")。

## **函数计算创建及使用**

函数计算建议创建【事件函数】，该方式已和函数计算节点进行了打通，可以方便进行传参。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6689676071/p764213.png)

以hello world的示例代码进行举例，代码如下图所示，打印event参数。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6689676071/p764214.png)

从阿里云百炼流程调试发起调用，传入2个参数，cityParam为杭州，dateParam为2024-01-26，调用之后返回结果hello world。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6689676071/p765448.png)查看函数计算的日志，输出了当前的event，cityParam及dateParam参数以dict的形式传入函数计算中，实现了函数计算中能够使用大模型流程中间结果的功能。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7689676071/p764216.png)

## **函数计算的出参**

由于调用函数计算的输出均被转为string处理，这样在各个节点内无法方便获取复杂对象中的值，所以阿里云百炼在函数计算的返回结果上进行了转换，当返回为dict、map或者list时，会被转为对象在全局变量中。

例如，函数计算返回"{\\"a\\":\\"1\\",\\"b\\":\\"2\\"}"，百炼会将这个jsonstring转为{"a":"1","b":"2"}，当获取该结果值时可以直接通过svcVars.{函数计算id}.{结果key}.a获取到a的值。以上具体的取值逻辑可以参考 [流程变量含义及取值方式说明](https://help.aliyun.com/zh/model-studio/definition-and-values-of-process-variables "")。