### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/) [函数计算 FC 2.0（文档已停止维护）](https://help.aliyun.com/zh/functioncompute/fc-2-0/) [快速入门](https://help.aliyun.com/zh/functioncompute/fc-2-0/getting-started-v2/) 示例代码

# 示例代码

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：快速创建函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/create-a-function-in-the-function-compute-console)[下一篇：操作指南](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/)

该文章对您有帮助吗？

反馈

函数计算为您提供丰富的示例代码，您可以在创建或配置函数时，快速选择您需要的函数代码。本文提供适用于函数计算的各种类型的示例代码列表。

## 使用说明

关于以下示例的使用方法，请参见对应代码库的README.md文件。

## Hello World

|     |     |     |
| --- | --- | --- |
| **标准Runtime** | **Custom Runtime** | **Custom Container** |
| **HTTP函数** |
| - [fc-http-node.js10](https://github.com/devsapp/start-fc/tree/master/http-function/fc-http-node.js10/src)<br>  <br>- [fc-http-node.js12](https://github.com/devsapp/start-fc/tree/master/http-function/fc-http-node.js12/src)<br>  <br>- [fc-http-node.js14](https://github.com/devsapp/start-fc/tree/master/http-function/fc-http-node.js14/src)<br>  <br>- [fc-http-php7.2](https://github.com/devsapp/start-fc/tree/master/http-function/fc-http-php7.2/src)<br>  <br>- [fc-http-python3.6](https://github.com/devsapp/start-fc/tree/master/http-function/fc-http-python3/src)<br>  <br>- [fc-http-java8](https://github.com/devsapp/start-fc/tree/master/http-function/fc-http-java8/src)<br>  <br>- [fc-http-golang](https://github.com/devsapp/start-fc/tree/master/http-function/fc-http-golang1.x/src) | - [PHP74-Swoole HTTP](https://github.com/devsapp/start-fc/tree/master/custom-function/php74/fc-custom-php74-http/src)<br>  <br>- [Python37 HTTP](https://github.com/devsapp/start-fc/tree/master/custom-function/python37/fc-custom-python37-http/src)<br>  <br>- [C++ HTTP](https://github.com/devsapp/start-fc/tree/master/custom-function/cpp/fc-custom-cpp-http/src) | - [C++ HTTP](https://github.com/devsapp/start-fc/tree/master/custom-container-function/fc-custom-container-http-cpp/src)<br>  <br>- [Spring Boot HTTP](https://github.com/devsapp/start-fc/tree/master/custom-container-function/fc-custom-container-http-springboot/src)<br>  <br>- [ASP.Net Core HTTP](https://github.com/devsapp/start-fc/tree/master/custom-container-function/fc-custom-container-http-aspdotnetcore/src) |
| **事件函数** |
| - [fc-event-node.js10](https://github.com/devsapp/start-fc/tree/master/event-function/fc-event-node.js10/src)<br>  <br>- [fc-event-node.js12](https://github.com/devsapp/start-fc/tree/master/event-function/fc-event-node.js12/src)<br>  <br>- [fc-event-node.js14](https://github.com/devsapp/start-fc/tree/master/event-function/fc-event-node.js14/src)<br>  <br>- [fc-event-php7.2](https://github.com/devsapp/start-fc/tree/master/event-function/fc-event-php7.2/src)<br>  <br>- [fc-event-python3.6](https://github.com/devsapp/start-fc/tree/master/event-function/fc-event-python3/src)<br>  <br>- [fc-event-java8](https://github.com/devsapp/start-fc/tree/master/event-function/fc-event-java8/src)<br>  <br>- [fc-event-golang](https://github.com/devsapp/start-fc/blob/master/event-function/fc-event-golang1.x/src) | - [Golang Event](https://github.com/devsapp/start-fc/tree/master/custom-function/golang/fc-custom-golang-event/src)<br>  <br>- [Node.js10 Event](https://github.com/devsapp/start-fc/tree/master/custom-function/nodejs10/fc-custom-nodejs10-event/src)<br>  <br>- [Node.js12 Event](https://github.com/devsapp/start-fc/tree/master/custom-function/nodejs12/fc-custom-nodejs12-event/src)<br>  <br>- [PHP74-Swoole Event](https://github.com/devsapp/start-fc/tree/master/custom-function/php74/fc-custom-php74-event/src)<br>  <br>- [Python37 Event](https://github.com/devsapp/start-fc/tree/master/custom-function/python37/fc-custom-python37-event/src)<br>  <br>- [C++ Event](https://github.com/devsapp/start-fc/tree/master/custom-function/cpp/fc-custom-cpp-event/src) | - [C++ Event](https://github.com/devsapp/start-fc/tree/master/custom-container-function/fc-custom-container-event-cpp/src)<br>  <br>- [Node.js14 Event](https://github.com/devsapp/start-fc/tree/master/custom-container-function/fc-custom-container-event-nodejs14/src)<br>  <br>- [Python3.9 Event](https://github.com/devsapp/start-fc/tree/master/custom-container-function/fc-custom-container-event-python3.9/src) |
| **Websocket函数** |
| 不涉及 | - [Golang Websocket](https://github.com/devsapp/start-fc/blob/master/custom-function/golang/fc-custom-golang-websocket/src)<br>  <br>- [Node.js10 Websocket](https://github.com/devsapp/start-fc/tree/master/custom-function/nodejs10/fc-custom-nodejs10-websocket/src)<br>  <br>- [Node.js12 Websocket](https://github.com/devsapp/start-fc/tree/master/custom-function/nodejs12/fc-custom-nodejs12-websocket/src)<br>  <br>- [Python37 Websocket](https://github.com/devsapp/start-fc/tree/master/custom-function/python37/fc-custom-python37-websocket/src) | - [Golang Websocket](https://github.com/devsapp/start-fc/blob/master/custom-container-function/fc-custom-container-websocket-golang/src)<br>  <br>- [Node.js14 Websocket](https://github.com/devsapp/start-fc/blob/master/custom-container-function/fc-custom-container-websocket-nodejs14/src)<br>  <br>- [Python3.9 Websocket](https://github.com/devsapp/start-fc/blob/master/custom-container-function/fc-custom-container-websocket-python3.9/src) |
| **自定义框架** |
| 不涉及 | - [Java8-SpringBoot](https://github.com/devsapp/start-fc/tree/master/custom-function/java8/fc-custom-java8-http/src)<br>  <br>- [Ruby example](https://github.com/devsapp/start-fc/tree/master/custom-function/ruby/fc-custom-ruby-event/src)<br>  <br>- [PowerShell example](https://github.com/devsapp/start-fc/tree/master/custom-function/powershell/fc-custom-powershell-event/src)<br>  <br>- [F# example](https://github.com/devsapp/start-fc/tree/master/custom-function/f%23/fc-custom-fsharp-http/src)<br>  <br>- [TypeScript example](https://github.com/devsapp/start-fc/tree/master/custom-function/typescript/fc-custom-typescript-event/src)<br>  <br>- [Lua example](https://github.com/devsapp/start-fc/tree/master/custom-function/lua/fc-custom-lua-event/src)<br>  <br>- [Dart example](https://github.com/devsapp/start-fc/tree/master/custom-function/dart/fc-custom-dart-event/src)<br>  <br>- [Rust example](https://github.com/devsapp/start-fc/tree/master/custom-function/rust/fc-custom-rust-event/src) | 不涉及 |

## 访问其他服务

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **Node.js** | **Python** | **PHP** | **Go** | **Java** |
| [访问 MySQL 数据库\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/rds-mysql-nodejs14/src) | [访问 MySQL 数据库\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/rds-mysql-python/src) | [访问 MySQL 数据库\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/rds-mysql-php) | [访问 MySQL 数据库\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/rds-mysql-golang/src) | [访问 MySQL 数据库\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/rds-mysql-java11/src) |
| [访问 MongoDB 数据库\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/mongodb-nodejs14/src) | [访问 MongoDB 数据库\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/mongodb-python/src) | [访问 MongoDB 数据库\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/mongodb-php) | [访问 MongoDB 数据库\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/mongodb-golang/src) | [访问 MongoDB 数据库\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/mongodb-java/src) |
| [访问表格存储 TableStore\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/tablestore-nodejs14/src) | [访问表格存储 TableStore\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/tablestore-python/src) | [访问表格存储 TableStore\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/tablestore-php) | [访问表格存储 TableStore\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/tablestore-golang/src) | [访问表格存储 TableStore\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/tablestore-java/src) |
| 无 | [访问云原生大数据计算服务 MaxCompute\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/fc-to-odps-sample/src) | 无 | 无 | [访问云原生大数据计算服务 MaxCompute\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/fc-to-odps-sample-java11/src) |
| [向消息队列 Kafka 投递消息\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/kafka-producer-nodejs/src) | [向消息队列 Kafka 投递消息\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/kafka-producer-python/src) | 无 | [向消息队列 Kafka 投递消息\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/kafka-producer-golang/src) | [向消息队列 Kafka 投递消息\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/kafka-producer-java/src) |
| [向轻量消息队列（原 MNS）队列投递消息\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/mns-queue-producer-nodejs-event/src) | [向轻量消息队列（原 MNS）队列投递消息\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/mns-queue-producer-python3-event/src) | [向轻量消息队列（原 MNS）队列投递消息\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/mns-queue-producer-php-event) | [向轻量消息队列（原 MNS）队列投递消息\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/mns-queue-producer-golang-event/src) | [向轻量消息队列（原 MNS）队列投递消息\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/mns-queue-producer-java11-event/src) |
| [向轻量消息队列（原 MNS）主题投递消息\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/mns-topic-producer-nodejs14-event/src) | [向轻量消息队列（原 MNS）主题投递消息\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/mns-topic-producer-python-event/src) | [向轻量消息队列（原 MNS）主题投递消息\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/mns-topic-producer-php-event) | [向轻量消息队列（原 MNS）主题投递消息\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/mns-topic-producer-golang-event/src) | [向轻量消息队列（原 MNS）主题投递消息\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/mns-topic-producer-java11-event/src) |
| [向消息 RocketMQ 投递消息\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/RocketMQ-trigger-nodejs14/src) | [向消息 RocketMQ 投递消息\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/RocketMQ-trigger-python/src) | 无 | [向消息 RocketMQ 投递消息\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/RocketMQ-trigger-golang/src) | [向消息 RocketMQ 投递消息\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/RocketMQ-trigger-java11/src) |

## 云服务触发函数

|     |     |     |     |     |
| --- | --- | --- | --- | --- |
| **Node.js** | **Python** | **PHP** | **Go** | **Java** |
| [定时触发函数\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/timer-trigger-nodejs/src) | [定时触发函数\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/timer-trigger-python/src) | 无 | [定时触发函数\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/timer-trigger-golang/src) | [定时触发函数\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/timer-trigger-java/src) |
| [日志服务 SLS 触发函数\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/sls-trigger-nodejs/src) | [日志服务 SLS 触发函数\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/sls-trigger-python/src) | 无 | [日志服务 SLS 触发函数\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/sls-trigger-golang/src) | [日志服务 SLS 触发函数\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/sls-trigger-java/src) |
| [对象存储 OSS 触发函数\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/oss-trigger-nodejs/src) | [对象存储 OSS 触发函数\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/oss-trigger-python/src) | [访问对象存储 OSS\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/oss-trigger-php/src) | [对象存储 OSS 触发函数\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/oss-trigger-golang/src) | [对象存储 OSS 触发函数\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/oss-trigger-java/src) |
| [内容分发网络 CDN 触发函数\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/cdn-trigger-nodejs/src) | [内容分发网络 CDN 触发函数\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/cdn-trigger-python/src) | [内容分发网络 CDN 触发函数\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/cdn-trigger-php) | [内容分发网络 CDN 触发函数\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/cdn-trigger-golang/src) | [内容分发网络 CDN 触发函数\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/cdn-trigger-java/src) |
| [消息队列 Kafka 触发函数\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/kafka-trigger-nodejs/src) | [消息队列 Kafka 触发函数\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/kafka-trigger-python/src) | 无 | [消息队列 Kafka 触发函数\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/kafka-trigger-golang/src) | [消息队列 Kafka 触发函数\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/kafka-trigger-java/src) |
| [轻量消息队列（原 MNS）队列触发函数\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/mns-queue-trigger-nodejs/src) | [轻量消息队列（原 MNS）队列触发函数\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/mns-queue-trigger-python/src) | [轻量消息队列（原 MNS）队列触发函数\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/mns-queue-trigger-php) | [轻量消息队列（原 MNS）队列触发函数\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/mns-queue-trigger-golang/src) | [轻量消息队列（原 MNS）队列触发函数\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/mns-queue-trigger-java11/src) |
| [轻量消息队列（原 MNS）主题触发函数\[node.js14\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-nodejs/mns-topic-trigger-nodejs14/src) | [轻量消息队列（原 MNS）主题触发函数\[python3\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-python/mns-topic-trigger-python/src) | [轻量消息队列（原 MNS）主题触发函数\[php7.2\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-php/mns-topic-trigger-php) | [轻量消息队列（原 MNS）主题触发函数\[go1\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-golang/mns-topic-trigger-golang/src) | [轻量消息队列（原 MNS）主题触发函数\[java11\]](https://github.com/awesome-fc/code-example/tree/master/quick-start-sample-codes/quick-start-sample-codes-java/mns-topic-trigger-java11/src) |

## Web应用

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **Node.js** | **Python** | **PHP** | **Go** | **Java** | **Others** |
| [Express \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/nodejs/express/src) | [Flask \[python3\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/python/flask/src) | [Think PHP \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/php/thinkphp/src) | [Gin \[custom\]](https://github.com/liufangchen/start-gin) | [SpringBoot \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/java/springboot) | [Hugo \[custom\]](https://github.com/liufangchen/start-hugo) |
| [Egg \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/nodejs/egg/src) | [Tornado \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/python/tornado/src) | [Laravel \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/php/laravel/src) | 无 | 无 | 无 |
| [Next.js \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/nodejs/next/src) | 无 | 无 | 无 | 无 | 无 |
| 无 | [Web.py \[python3\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/python/webpy/src) | 无 | 无 | 无 | 无 |
| [Hapi \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/nodejs/hapi/src) | [Django \[python3\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/python/django/src) | 无 | 无 | 无 | 无 |
| [Koa \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/nodejs/koa/src) | [FastAPI \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/python/fastapi/src) | 无 | 无 | 无 | 无 |
| [Nest \[node.js12\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/nodejs/nest/src) | 无 | 无 | 无 | 无 | 无 |
| 无 | 无 | [Whatsns \[custom\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/php/whatsns/src) | 无 | 无 | 无 |
| [Think.js \[node.js12\]](https://github.com/devsapp/start-web-framework/tree/master/web-framework/nodejs/thinkjs/src) | 无 | 无 | 无 | 无 | 无 |
| 无 | 无 | [Kodbox \[custom\]](https://github.com/devsapp/start-fc-kodbox) | 无 | 无 | 无 |

## 静态网站应用

- [Hexo应用](https://github.com/devsapp/start-website/tree/master/hexo/src)

- [Docusaurus应用](https://github.com/devsapp/start-website/tree/master/docusaurus/src)

- [VuePress应用](https://github.com/devsapp/start-website/tree/master/vuepress/src)


## AI场景

- [PyTorch案例](https://github.com/devsapp/start-ai/tree/master/start-pytorch/src)

- [TensorFlow案例](https://github.com/devsapp/start-ai/tree/master/start-tensorflow/src)

- [OCR案例](https://github.com/devsapp/start-ai/tree/master/start-ocr/src)

- [目标检测案例](https://github.com/devsapp/start-ai/tree/master/image-prediction-app/src)

- [GPU应用模板案例](https://github.com/devsapp/start-fc-gpu)


## 音视频处理

- [弹性高可用的高度自定义音视频处理](https://github.com/devsapp/start-ffmpeg/tree/master/ffmpeg-app/src)

- [对直播视频流截图的应用](https://github.com/devsapp/start-ffmpeg/tree/master/rtmp-snapshot/src)

- [一个对浏览器全景录制](https://github.com/devsapp/start-ffmpeg/tree/master/headless-ffmpeg/src)


## 其他

- 基于puppeteer的截图Web应用

  - [基于Node.js的案例](https://github.com/devsapp/start-puppeteer/tree/master/puppeteer-nodejs/src)

  - [基于Container的案例](https://github.com/devsapp/start-puppeteer/tree/master/puppeteer-container/src)
- [WORD转PDF的应用](https://github.com/devsapp/start-word2pdf)

- [PDF转图片的应用](https://github.com/devsapp/start-pdf2img)

- [现代应用解决方案](https://github.com/devsapp/modern-web-application)