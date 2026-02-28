### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK Serverless集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/)[开发参考](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/)[CLI参考](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/cli-reference/)查看所有集群实例

# 查看所有集群实例

更新时间：2023-09-04 03:16:39

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：概述](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/overview-11)[下一篇：查看集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/view-cluster)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

API请求响应

查看您在容器服务中创建的所有集群。

## API请求响应

请求格式

```shell
aliyun cs GET /clusters
```

响应结果

```json
[\
    {\
        "agent_version": "string",\
        "cluster_id": "string",\
        "created": "datetime",\
        "external_loadbalancer_id": "string",\
        "master_url": "string",\
        "name": "string",\
        "network_mode": "string",\
        "region_id": "string",\
        "security_group_id": "string",\
        "size": "numbers",\
        "state": "string",\
        "updated": "datetime",\
        "vpc_id": "string",\
        "vswitch_id": "string"\
    }\
]
```