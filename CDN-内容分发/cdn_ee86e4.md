### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/)

# 如何查看CDN节点是否生效

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

## 概述

本文主要介绍将源站业务配置到CDN后，如何查看CDN节点是否生效。

## 详细信息

可通过以下三种方法查看CDN节点是否生效，请根据现场实际情况，选择下列对应的步骤：

- [方法一：通过ping或dig的方式查看所添加的加速域名](https://help.aliyun.com/zh/cdn/ee86e4#RGmAG)
- [方法二：在CDN控制台中查看节点是否生效](https://help.aliyun.com/zh/cdn/ee86e4#PQQYX)
- [方法三：获取对应加速域名资源的response查看节点是否生效](https://help.aliyun.com/zh/cdn/ee86e4#ysfzn)

### 方法一：通过ping或dig的方式查看所添加的加速域名

> **说明：** 该操作以Windows系统为例，若您需要在Linux系统中查看CDN节点是否生效，请参见 [获取对应加速域名资源的response查看节点是否生效](https://help.aliyun.com/zh/cdn/ee86e4#RGmAG)。

- 在Windows系统中执行以下命令，通过ping的方式查看所添加的加速域名。


```
ping example.aliyundoc.com
```


系统显示类似如下，如果被转向`example.aliyundoc.com.w.alikunlun.com`的域名，即表示CDN功能已生效。

![11.png](https://onekb.oss-cn-zhangjiakou.aliyuncs.com/51061013/0f9f3c35-8c9e-4c9f-8e96-b579c31104fb.png)
- 在Windows系统中执行以下命令，通过dig的方式查看所添加的加速域名，可以查看相应的加速域名访问CDN节点的IP。


```
dig example.aliyundoc.com
```


系统显示类似如下，确认CDN节点以生效。

![dig.png](https://onekb.oss-cn-zhangjiakou.aliyuncs.com/51061013/26c6e938-61b9-4ee5-9648-0b3b7d67a938.png)

### 方法二：在CDN控制台中查看节点是否生效

请参见 [如何验证指定的IP是否为阿里云CDN节点的IP地址](https://help.aliyun.com/zh/cdn/verify-that-the-specified-ip-address-is-the-ip-address-of-the-alibaba-cloud-cdn-pop)，在CDN控制台中查看节点是否生效。

### 方法三：获取对应加速域名资源的response查看节点是否生效

在Linux系统中执行以下命令，获取对应加速域名资源的response，查看是否有CDN加速的对应节点信息，从而判断CDN是否生效。

```
curl -I example.aliyundoc.com/10.JPG
```

系统显示类似如下。

![TB1rps_LpXXXXbpaXXXXXXXXXXX.jpg](https://onekb.oss-cn-zhangjiakou.aliyuncs.com/51061013/4d573034-dbf4-41b6-bf0a-971a3467e752.jpg)

## 更多信息

CDN控制台成功添加加速域名后，如何验证加速域名访问正常，详情请参见 [本地测试CDN加速域名](https://help.aliyun.com/zh/cdn/test-whether-a-domain-name-is-accessible)。

## 适用于

- CDN

该文章对您有帮助吗？

反馈