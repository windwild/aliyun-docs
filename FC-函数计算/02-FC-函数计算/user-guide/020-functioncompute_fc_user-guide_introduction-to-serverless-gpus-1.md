### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [函数计算](https://help.aliyun.com/zh/functioncompute/)[函数计算 FC 3.0](https://help.aliyun.com/zh/functioncompute/fc/)[函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/)[创建函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/function-instance-1/)[创建GPU函数](https://help.aliyun.com/zh/functioncompute/fc/user-guide/creating-a-gpu-function/)Serverless GPU概述

# Serverless GPU概述

更新时间：2025-06-19 23:51:28

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

Serverless GPU是一种新兴的云计算GPU服务，它采用了服务器无感知计算的理念，通过提供一种按需分配的GPU计算资源，有效地解决原有GPU长驻使用方式导致的低资源利用率、高使用成本和低弹性能力等痛点问题。本文介绍Serverless GPU的详细功能和优势。

传统GPU长驻使用方式存在许多问题，例如，需要提前规划好资源需求，需要占用大量的计算资源，且在使用过程中由于任务间的不均衡性，可能导致一些GPU资源一直处于空闲状态。而Serverless GPU则提供了一种更加灵活的方式来利用GPU计算资源，用户只需根据自己的实际需求选择合适的GPU型号和计算资源规模，即可随时启动和停止GPU计算，无需事先规划资源使用情况。

Serverless GPU采用了一系列优化措施，以提高计算资源的利用率和弹性。例如，针对GPU计算的冷启动问题，Serverless GPU通过全链路GPU启停优化，可以在极短的时间内启动和准备GPU计算资源，以支持用户在短时间内启动和停止大量的GPU计算任务。此外，Serverless GPU还提供了按量付费的计费方式，用户只需按照实际使用的GPU计算时间进行付费，无需长期承担高额的资源成本。

Serverless GPU是一种高度灵活、高效利用、按需分配GPU计算资源的新兴云计算服务。Serverless GPU可以帮助用户有效地解决GPU长驻使用方式导致的资源浪费、高成本、低弹性等问题，为用户提供更加便捷、高效的GPU计算服务，有效承载AI模型推理、AI模型训练、音视频加速生产、图形图像加速等加速工作负载。