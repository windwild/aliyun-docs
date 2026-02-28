### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [快速入门](https://help.aliyun.com/zh/sae/getting-started/) 周期性执行或手动触发执行Job 任务

# 周期性执行或手动触发执行Job 任务

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：部署第一个Serverless应用](https://help.aliyun.com/zh/sae/quick-deployment-of-microservice-applications)[下一篇：操作指南](https://help.aliyun.com/zh/sae/user-guide/)

该文章对您有帮助吗？

反馈

通过SAE快速创建Job任务模板，实现周期性地自动执行任务，或者手动发送HTTP/HTTPS请求来触发任务执行，并且在任务完成后快速释放计算资源。

## 使用场景

Job任务适用于对延时不敏感的异步离线场景，可以一次性执行，也可以按照设定的周期定时执行。例如：批量统计数据报表、在整点定时发送优惠券。

## **准备工作**

已开通 [Serverless应用引擎](https://saenext.console.aliyun.com/)、 [EventBridge](https://help.aliyun.com/zh/eventbridge/getting-started/activate-eventbridge-and-grant-permissions-to-a-ram-user#task-1947668 "") 并授权。

## **周期性执行Job任务**

1. 在[SAE任务模板](https://saenext.console.aliyun.com/cn-hangzhou/job-list)中，在顶部选择目标地域和命名空间，点击 **创建任务模板**。配置以下信息。

1. 自定义 **任务模板名称**。

2. 任务部署方式 **选择镜像部署**，使用默认的Demo镜像即可。实际场景中，可以点击 **设置镜像**，灵活定义任务执行时使用的镜像。

3. 其余参数保持默认，点击 **下一步**。
2. 在 **任务设置** 区域，配置以下信息。

1. **任务类型** 选择 **周期性任务**。

2. **Cron表达式** 设置为`*/1 * * * ?`，表示每分钟执行1次。

3. 其余参数保持默认，点击 **创建**，等待任务创建完成。
3. 在左侧导航栏点击 **任务记录**，可以查看任务周期性自动执行的记录。点击页面右上角的刷新按钮，查看最新结果。

4. 在左侧导航栏点击**日志管理** \> **实时日志**，可以查看最近一次任务的执行结果，具体到本例中，程序在控制台打印出一串数字。


## **通过HTTP/HTTPS请求单次触发Job任务执行**

1. 在[SAE任务模板](https://saenext.console.aliyun.com/cn-hangzhou/job-list)中，在顶部选择目标地域和命名空间，点击 **创建任务模板**。配置以下信息。

1. 自定义 **任务模板名称**。

2. 任务部署方式 **选择镜像部署**，使用默认的Demo镜像即可。实际场景中，可以点击 **设置镜像**，灵活定义任务执行时使用的镜像。

3. 其余参数保持默认，点击 **下一步**。
2. 在 **任务设置** 区域，配置以下信息。

1. **任务类型** 选择 **一次性任务**。

2. **请求类型** 选择 **HTTP&HTTPS**，表示同时支持HTTP和HTTPS请求来触发任务执行。

3. **请求方法** 选择 **GET** 和 **POST**，表示同时支持通过GET和POST请求来触发任务执行。

4. 其余参数保持默认，点击 **创建**，等待任务创建完成。
3. 在 **任务模板详情** 页的 **任务设置** 区域，可以查看触发任务执行的 **公网请求 URL**，复制到浏览器的地址栏并回车，即可触发任务执行。

4. 在左侧导航栏点击 **任务记录**，可以查看任务单次执行的记录。点击页面右上角的刷新按钮，查看最新结果。

5. 在左侧导航栏点击**日志管理** \> **实时日志**，可以查看最近一次任务的执行结果，具体到本例中，程序在控制台打印出一串数字。


## 清理资源

在完成本教程后，如果无需继续使用资源，请删除相关资源，否则会持续产生费用。

在[SAE任务模板](https://saenext.console.aliyun.com/cn-hangzhou/job-list)中，在顶部选择目标地域和命名空间，找到已创建的任务模板。单击 **操作** 列的 **删除**，然后跟随指引操作。

## **后续步骤**

在实际场景中，需要通过应用镜像、代码包、或Shell脚本等方式创建任务模板，请参考 [管理任务模板](https://help.aliyun.com/zh/sae/job-template-management-2-0 "")。