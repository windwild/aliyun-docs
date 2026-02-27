### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) Script节点使用说明

# Script节点使用说明

更新时间：2026-02-11 02:34:48

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

脚本类型

返回变量名称

脚本示例

javascript示例

Python示例

**重要**

为满足更丰富的编排需求，流程编排功能已全面升级为工作流应用和智能体编排应用。流程编排功能将逐步下线，但此变动不影响已经使用了流程编排功能的用户。您可以继续使用流程编排功能，也可以改为使用工作流应用或智能体编排应用，以获得更好的使用体验。具体请参见 [工作流应用](https://help.aliyun.com/zh/model-studio/workflow-application/ "") 和 [智能体编排应用](https://help.aliyun.com/zh/model-studio/multi-agent-application "")。

本文档介绍Script节点使用说明。

## **节点界面**

点击应用中心--流程编排--新建流程，点击 **脚本节点**。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6530551271/p823439.png)

## **节点说明**

Script节点是脚本节点，面向开发者提供简单的代码开发能力。代码运行在归属于用户的免费函数计算实例上。目前支持javascript、python。Code节点中的代码封装在函数中，返回语句用于输出函数的结果。返回的任何结果都可以在后续步骤中使用。

## **配置页面**

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6530551271/p823438.png)

## **配置说明**

### **脚本类型**

当前支持javascript、python两种。

### **返回变量名称**

设定函数体返回的变量名称，如果不填写，默认使用fcResult作为变量名称。

例如

```json
{
    "svcVars":{
        "Script_szLxMn":{ // 脚本节点id
            "response":{ // 固定返回字段
                "temp":[ // 声明的返回变量名称，缺省值为scriptResult\
                    "a",\
                    " ",\
                    "c"\
                ]
            }
        }
    }
}
```

## **脚本示例**

当前支持的是代码段编程，代码封装在函数中进行执行，所以脚本最后必须return相应的结果，在后续的流程中该变量才能进行使用。

### javascript示例

```javascript
const a = 1;
const b = a+2;
return a;
```

### **Python示例**

```python
import json
import logging
json_string = svcVars['LLM_ae4fzv']['response']['text']
data = json.loads(json_string)
prefix_str = '天猫精灵将为你播放'
media_name = data['mediaName']
singer_name = data['singerName']
return f"{prefix_str} {singer_name} 的 {media_name}，收听完整版请下载天猫精灵APP收听完整版"
```