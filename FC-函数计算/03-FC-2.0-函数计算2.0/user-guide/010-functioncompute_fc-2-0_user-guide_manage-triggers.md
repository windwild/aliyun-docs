### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/)[操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)[事件触发](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/event-triggers/)触发器管理

# 触发器管理

更新时间：2025-08-04 01:32:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：触发器简介](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/trigger-overview)[下一篇：触发器Event格式](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/formats-of-event-for-different-triggers)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

创建触发器

双向集成触发器

单向集成触发器

云产品事件触发器

更新触发器配置

您可以在指定函数中创建触发器，使用触发器描述一组规则，当某个事件满足这些规则，事件源就会触发关联的函数。本文列举函数计算支持的所有触发器。

## 前提条件

- [创建服务](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-services#section-765-0zj-cc4 "")

- [创建函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/manage-functions#section-b9y-zn1-5wr "")


## 创建触发器

**重要**

单个函数下最多允许创建10个触发器。

### **双向集成触发器**

- [创建定时触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-a-time-trigger#section-gbz-k3r-vum "")

- [创建OSS触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-a-native-oss-trigger#section-lo1-872-rwb "")

- [创建SLS触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-a-log-service-trigger#section-pz6-4oj-c28 "")

- [创建CDN触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-an-alibaba-cloud-cdn-trigger#section-fap-ps2-k5n "")

- [创建Tablestore触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-a-tablestore-trigger#section-25b-1hy-csz "")

- [创建HTTP触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-an-http-trigger-that-invokes-a-function-with-http-requests#section-11e-t95-jq7 "")

- [创建MNS主题触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-an-mns-topic-trigger#section-uhk-14c-0i3 "")

- [创建MNS队列触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/mns-queue-triggers#section-qqh-vij-ljv "")

- [创建RocketMQ触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/apsaramq-for-rocketmq-triggers#section-qp6-qe6-ide "")

- [创建RabbitMQ触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/apsaramq-for-rocketmq-triggers-1#section-jvf-anh-5xo "")

- [创建Kafka触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/apsaramq-for-kafka-trigger#task-2533588 "")

- [创建DTS触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/dts-triggers "")

- [创建MQTT触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/message-queue-for-mqtt-triggers "")

- [创建Apache RocketMQ触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/apache-rocketmq-trigger "")


### **单向集成触发器**

- [创建ALB触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/alb-triggers "")

- [创建API网关触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-an-api-gateway-trigger "")

- [创建DataHub单向触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/datahub-one-way-trigger "")

- [IoT物联网平台](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/iot-platform "")

- [DataWorks大数据开发治理平台](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/dataworks-big-data-development-and-governance-platform "")

- [Serverless工作流](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/serverless-workflow "")

- [云数据库MongoDB版触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/apsaradb-for-mongodb-trigger/ "")

- [RDS MySQL数据库触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/rds-mysql-database-trigger-is-synchronized-to-fc "")


### **云产品事件触发器**

- [创建阿里云产品事件触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/configure-event-triggers-for-alibaba-cloud-services#section-208-xwp-jfk "")


## 更新触发器配置

**说明**

已创建的 [MNS主题触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/overview-18#concept-2259991 "")、 [Tablestore触发器](https://help.aliyun.com/zh/functioncompute/fc-2-0/overview-20#multiTask8694 "") 和单向集成触发器不支持使用以下方法修改。

1. 登录 [函数计算控制台](https://fcnext.console.aliyun.com/)，在左侧导航栏，单击 **服务及函数**。
2. 在顶部菜单栏，选择地域，然后在 **服务列表** 页面，单击目标服务 **操作** 列的 **函数管理**。
3. 在 **函数管理** 页面，单击目标函数名称。

4. 在函数详情页面，单击 **触发器管理** 页签。在触发器列表，找到目标触发器，然后单击其右侧 **操作** 列的 **编辑**。

5. 在编辑触发器面板根据需要修改触发器的配置，然后单击 **确定**。


不同触发器修改您也可以根据界面提示删除不再使用的触发器。