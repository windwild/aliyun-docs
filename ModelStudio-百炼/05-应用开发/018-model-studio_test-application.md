### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/)

# 如何测试应用

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/bailian)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

开发者如果要调试当前应用的效果，需要集成SDK后发起请求调用才能看到结果。这样非常不直观，于是平台为开发者提供了应用的测试窗服务，便于开发者在可视化的情况下进行调试。

## **测试步骤**

### **步骤一：测试前做好配置检查**

要检查应用中心内的配置是否已经配置完全，例如中控模型的选择是否符合预期，插件是否完成了范围勾选，下面是一些应用中心的配置。

- [点击了解如何选择应用](https://help.aliyun.com/zh/model-studio/application-gallery/ "")


### **步骤二：使用说明**

1. 应用中心→我的应用→点击【 **管理**】按钮。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2108594171/p796568.png)

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2108594171/p796643.png)

### **步骤三：重新生成/问题反馈**

（1）右上角「重置对话」，是清空当前对话的作用，由于 **测试窗调试过程中是一直携带上下文的**，为避免上下文干扰，在调试过程中可以直接重置对话。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2108594171/p796573.png)

（2）下方输入框是模拟用户问题的录入框，单次模拟有字符限制，且一次调试完成后才可以录入下一个问题。若需要重新输入问题，可以点击"停止生成"再进行提问。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2108594171/p796645.png)

（3）中间通义图标右侧的就是应用的最终输出结果，在输出结果的下方有「 **问题反馈**」按钮。

requestID是串联整个服务的traceId，当给答疑的同学进行问题反馈时， **提供requestID可以快速定位问题**，省时省力。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2108594171/p796644.png)

### **步骤四：测试完毕，验证结果**

界面输出的为responseText，验证是否符合预期。