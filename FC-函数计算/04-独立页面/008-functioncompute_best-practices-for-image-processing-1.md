### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 图像处理最佳实践

# 图像处理最佳实践

更新时间：2023-09-17 21:36:53

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/fc)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：函数计算](https://help.aliyun.com/zh/functioncompute/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

应用场景与优势

教程示例说明

准备工作

通过函数计算控制台部署GPU应用

执行结果

您可以通过函数计算控制台、SDK或Serverless Devs来体验GPU实例的最佳实践。本文以Python语言为例，说明如何通过控制台，将原始图像经过函数代码处理，实现边缘检测。

## 应用场景与优势

在不同的应用场景下，函数计算提供的GPU实例与CPU相比所具备的优势如下。

- **实时、准实时的应用场景**

  - 提供数倍于CPU的图形图像处理效率，从而快速将生产内容推向终端用户。
- **成本优先的图像处理场景**

  - 提供弹性预留模式，从而按需为客户保留GPU工作实例，对比自建GPU集群拥有较大成本优势。

  - 提供GPU共享虚拟化，支持以1/2、独占方式使用GPU，允许业务以更精细化的方式配置GPU实例。
- **效率优先的图像处理场景**

  - 屏蔽运维GPU集群的繁重负担（驱动/CUDA版本管理、机器运行管理、GPU坏卡管理），使得开发者专注于代码开发、聚焦业务目标的达成。

GPU实例的更多信息，请参见 [实例类型及使用模式](https://help.aliyun.com/zh/functioncompute/fc/product-overview/instance-types-and-specifications "")。

## 教程示例说明

如下表所示，左列为原图，右列是经过部署在函数计算的边缘检测函数代码处理后，所生成的图片。

| **原始图像** | **边缘检测结果** |
| --- | --- |

|     |     |
| --- | --- |
| **原始图像** | **边缘检测结果** |
| ![image_processing_example](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1208975561/p345922.png) | ![image_processing_result_example](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1208975561/p346357.png) |

## 准备工作

- OpenCV需要自行编译以使用GPU加速，编译方式如下：

  - （推荐）通过Docker使用已编译好的OpenCV。下载地址： [opencv-cuda-docker](https://github.com/JulianAssmann/opencv-cuda-docker) 或 [cuda-opencv](https://hub.docker.com/r/awokeknowing/cuda-opencv)

  - 自行编译。具体步骤，请参见 [官网编译手册](https://docs.opencv.org/2.4/modules/gpu/doc/introduction.html)。
- 将需处理的音视频资源上传至在GPU实例所在地域的OSS Bucket中，且您对该Bucket中的文件有读写权限。具体步骤，请参见 [控制台上传文件](https://help.aliyun.com/zh/oss/getting-started/upload-objects-16#concept-zx1-4p4-tdb "")。权限相关说明，请参见 [修改存储空间读写权限](https://help.aliyun.com/zh/oss/modify-bucket-acls#concept-d2d-3gz-5db "")。

## 通过函数计算控制台部署GPU应用

1. 部署镜像。
1. 建容器镜像服务的企业版实例或个人版实例。
      推荐您创建企业版实例。具体操作步骤，请参见 [创建企业版实例](https://help.aliyun.com/zh/acr/user-guide/create-a-container-registry-enterprise-edition-instance#task488 "")。

2. 创建命名空间和镜像仓库。
      具体操作步骤，请参见 [步骤二：创建命名空间](https://help.aliyun.com/zh/acr/getting-started/build-images-on-container-registry-enterprise-edition-instances#section-m0h-3y9-s89 "") 和 [步骤三：创建镜像仓库](https://help.aliyun.com/zh/acr/getting-started/build-images-on-container-registry-enterprise-edition-instances#section-7ek-3k0-l1n "")。

3. 在[容器镜像服务控制台](https://cr.console.aliyun.com/)，根据界面提示完成Docker相关操作步骤。然后将上述示例app.py和Dockerfile推送至实例镜像仓库，文件信息，请参见通过ServerlessDevs部署GPU应用时/code目录中的app.py和Dockerfile。
      ![db-acr-docker](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4432093961/p451532.png)
2. 创建GPU函数。具体操作步骤，请参见 [创建Custom Container函数](https://help.aliyun.com/zh/functioncompute/fc-2-0/user-guide/create-a-custom-container-function#task-2559807 "")。

3. 修改函数的执行超时时间。


1. 在目标函数的 **配置** 页签，在左侧导航栏，选择 **运行时**，然后单击 **运行时** 右侧的 **编辑**。

2. 在 **运行时** 面板，修改 **执行超时时间**，然后单击 **确定**。


**说明**

CPU转码耗时会超过默认的60s，因此建议您修改 **执行超时时间** 为较大的值。

4. 配置GPU预留实例。关于配置预留实例的具体操作，请参见 [配置预留实例](https://help.aliyun.com/zh/functioncompute/fc/user-guide/configure-launch-snapshot-and-auto-scaling-rules#section-7v8-a44-j5q "")。



配置完成后，您可以在规则列表查看预留的GPU实例是否就绪。即 **当前预留实例数** 是否为设置的预留实例数。

5. 使用cURL测试函数。

1. 在函数详情页面，单击 **触发器管理** 页签，查看触发器的配置信息，获取触发器的访问地址。
2. 在命令行执行如下命令，调用GPU函数。



      - 查看线上函数版本















        ```plaintext
        curl "https://tgpu-op-console-tgpu-op-console-ajezokddpx.cn-shenzhen.fcapp.run"
        {"function": "opencv_edge_canny"}
        ```

      - 执行图片边缘检测















        ```plaintext
        curl "https://tgpu-op-console-tgpu-op-console-ajezokddpx.cn-shenzhen.fcapp.run" -H "RUN-MODE: normal"
        {"result": "CUDA-capable device supported | process image ok!"}
        ```

## 执行结果

您可通过在浏览器中访问以下域名，查看经过边缘检测处理后的图片：

```plaintext
https://cri-zfen7xhpsx******-registry.oss-cn-shenzhen.aliyuncs.com/cats2.png
```

本域名仅为示例，需以实际情况为准。