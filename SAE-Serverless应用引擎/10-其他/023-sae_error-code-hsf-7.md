## 报错信息

应用启动时，报错如下，表示不可识别的序列化类型。


```nginx
unsupported serialization [${serializeType}]
```

## 解决方案

Provider的bean配置了serializeType属性，HSF1的序列化配置类型不在支持的范围内。请检查对端的HSF版本和序列化协议的配置。


- serializeType属性指定HSF1使用的序列化方式，支持的值仅包括Java和hessian，默认值为hessian。
- preferSerializeType属性指定HSF2使用的序列化方式，支持的值包括Java、hessian、hessian2、kyro和json，默认值为hessian2。

### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 错误编码：HSF-0006

# 错误编码：HSF-0006

更新时间：2022-11-17 01:50:15

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

报错信息

解决方案