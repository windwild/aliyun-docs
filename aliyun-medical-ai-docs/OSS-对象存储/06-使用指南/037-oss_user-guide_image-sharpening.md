### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[数据处理](https://help.aliyun.com/zh/oss/user-guide/data-transformation/)[图片处理](https://help.aliyun.com/zh/oss/user-guide/overview-17/)[旧版图片处理指南](https://help.aliyun.com/zh/oss/user-guide/earlier-version-of-img/)[图片效果](https://help.aliyun.com/zh/oss/user-guide/image-effects/)锐化

# 锐化

更新时间：2025-03-12 23:17:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：自适应方向](https://help.aliyun.com/zh/oss/user-guide/auto-rotate)[下一篇：模糊效果](https://help.aliyun.com/zh/oss/user-guide/blurring)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

参数

示例

图片处理支持锐化处理，使图片变得更清晰。

## 参数

\## 参数\| 名称 \| 描述 \| 取值范围 \|\| --- \| --- \| --- \|\| sh \| 表示进行锐化处理。参数越大，图像越清晰。 \| \\\[50, 399\]（推荐值：100） \|

| **名称** | **描述** | **取值范围** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **名称** | **描述** | **取值范围** |
| sh | 表示进行锐化处理。参数越大，图像越清晰。 | \[50, 399\] （推荐值：100，可达到较优的平衡效果） |

## 示例

- 进行锐化处理，锐化参数为100。

[https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100sh](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100sh)

![锐化1](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6774030761/p530717.jpg@100sh)

- 进行锐化处理，锐化参数为50。

[https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@50sh](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@50sh)

![锐化2](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6774030761/p530718.jpg@50sh)

- 缩略成高度100，宽度100，并进行锐化操作，保存成png格式。

[https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100w\_100h\_100sh.png](https://oss-console-img-demo-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/example.jpg@100w_100h_100sh.png)

![锐化3](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6774030761/p530719.png)