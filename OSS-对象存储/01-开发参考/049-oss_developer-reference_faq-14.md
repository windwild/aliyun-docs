### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[ossftp](https://help.aliyun.com/zh/oss/developer-reference/ossftp-overview/)常见问题

# 常见问题

更新时间：2023-08-30 22:33:08

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：WordPress如何存储远程附件到OSS](https://help.aliyun.com/zh/oss/developer-reference/how-to-store-remote-attachments-from-wordpress-websites-to-oss)[下一篇：使用OSS Connector for AI/ML加速模型训练](https://help.aliyun.com/zh/oss/developer-reference/oss-connector-overview/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

连接FTP Server时提示无法连接到服务器

使用FileZilla连接FTP Server时报错501

登录ossftp成功后List文件超时导致连接断开

数据传输不成功

客户端和FTP Server之间的连接经常断开

本文主要介绍在使用ossftp时可能遇到的问题及解决方案。

## 连接FTP Server时提示无法连接到服务器

- 问题现象

提示：严重错误，无法连接到服务器。
![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1324459951/p2521.png)
- 问题原因

  - 输入的AccessKey ID和AccessKey Secret有误。

  - 所用的AccessKey信息为RAM用户的AccessKey，但RAM用户没有访问OSS的权限。
- 解决方法

  - 输入正确的AccessKey ID和AccessKey Secret信息后重试连接服务器。

  - 结合实际使用场景为RAM用户配置相应的权限。

    以下为常见场景的权限说明：


    - 只读访问OSS某个Bucket的资源

      所需权限为`oss:ListObjects`和`oss:GetObject`

    - 在OSS某个Bucket中写入数据

      所需权限为`oss:ListObjects`和`oss:PutObject`

    - 删除Bucket中的数据

      所需权限为`oss:ListObjects`和`oss:DeleteObject`


关于授权RAM用户其他场景的配置示例，请参见 [RAM Policy常见示例](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#concept-2025445 "")。

## 使用FileZilla连接FTP Server时报错501

- 问题现象



在Linux下运行FTP Server，然后使用FileZilla连接时报错501。

















```plaintext
501 can't decode path (server filesystem encoding is ANSI_X3.4-1968)
```

- 问题原因

本地中文编码问题。

- 解决方法

1. 在将要运行start.sh的终端中输入下面的命令。















     ```plaintext
     $ export LC_ALL=en_US.UTF-8; export LANG="en_US.UTF-8"; locale
     ```

2. 重新启动FileZilla。

## 登录ossftp成功后List文件超时导致连接断开

Bucket根目录下的文件或文件夹数量过多。 登录ossftp后，FTP Server会尝试List Bucket根目录下的所有文件和文件夹。单次可以List 1000个文件和文件夹。如果根目录下文件和文件夹数量超过100万，会导致1000次以上的List请求，从而造成超时。

## 数据传输不成功

- 问题原因

FTP协议的控制端口与数据端口不同。当FTP Server在被动模式下需要传输数据时，FTP Server会打开1个随机端口用于连接客户端。当FTP Server所在机器有端口限制时，可能会导致数据无法正常传输。

- 解决方法

运行`ftpserver.py`时，通过指定--passive\_ports\_start和--passive\_ports\_end选项设置本地端口的起止范围，然后打开该范围内的端口。


## 客户端和FTP Server之间的连接经常断开

- 问题原因

客户端和FTP Server之间连接超时。

- 解决方法

设置客户端和FTP Server之间连接不超时。以FileZilla工具为例，在**设置** \> **连接**，将超时设置为0（表示不超时）。