### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [文字识别](https://help.aliyun.com/zh/ocr/)[服务支持](https://help.aliyun.com/zh/ocr/support/)[OCR云市场文档集合](https://help.aliyun.com/zh/ocr/support/ocr-document-collection-in-alibaba-cloud-marketplace/)云市场OCR快速入门

# 云市场OCR快速入门

更新时间：2023-11-29 03:04:29

复制为 MD 格式

[产品详情](https://ai.aliyun.com/ocr)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：云市场资源包计费](https://help.aliyun.com/zh/ocr/support/billing-of-resource-plans-for-alibaba-cloud-marketplace)[下一篇：云市场API参考](https://help.aliyun.com/zh/ocr/support/api-reference-for-alibaba-cloud-marketplace/)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

参考示例 — 身份证识别

欢迎使用OCR服务，这里主要为您介绍如何使用OCR的各种服务，如何快速找到需要的帮助信息。下文主要通过身份证识别服务的例子来介绍各个流程。

## **参考示例 — 身份证识别**

云市场OCR快速入门

[AppKey&AppCode管理](https://market.console.aliyun.com/?spm=5176.product-detail.detail.5.6e136573tHJz5z&productCode=cmapi010401#/?_k=6dq7b0)：在此处可以查看您的AppKey、AppSecret、AppCode

**购买服务**

1、开通API网关 [https://www.aliyun.com/product/apigateway](https://www.aliyun.com/product/apigateway)

2、在身份证服务 [https://market.aliyun.com/products/57124001/cmapi010401.html](https://market.aliyun.com/products/57124001/cmapi010401.html) 页面购买服务

**授权API**

1、进入 [API网关-控制台](https://apigateway.console.aliyun.com/)，点击左侧`调用API`—\> `应用管理`，创建新应用。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5172421071/p742958.png)

2、应用创建后，点击应用名称，查看`应用ID`

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5172421071/p742960.png)

3、点击左侧`已购买API`，在对应的API一行中选择`查看API`，点击`授权`，输入步骤2获取的应用ID，进行授权即可。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6172421071/p742962.png)![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6172421071/p742963.png)![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6172421071/p742964.png)

**API调用**

API的具体调用方式见身份证服务 [产品页面](https://market.aliyun.com/products/57124001/cmapi010401.html)

![image.png](<Base64-Image-Removed>)

具体的示例代码见产品页面的请求示例代码，通过 [此页面](https://market.console.aliyun.com/imageconsole/index.htm#/apiService/list) 查看APPCODE， 请阅读 [API介绍-身份证](https://market.aliyun.com/products/57124001/cmapi010401.html?spm=5176.730005.result.13.22db3524UQTOpf&innerSource=search_%E8%BA%AB%E4%BB%BD%E8%AF%81%E8%AF%86%E5%88%AB#sku=yuncode440100000) 了解身份证服务具体的输入输出格式。

![image.png](<Base64-Image-Removed>)

示例如下：

```javascript
{
	"image":  "图片二进制数据的base64编码/图片url",
	"configure": {
            "side":"face", #身份证正反面类型:face/back
            "quality_info": false   # 是否输出身份证质量分信息，默认为否（包括 是否是翻拍、是否是复印件、完整度评分、整体质量分数、篡改分数）
         }
}
```

上面列出的是识别身份证正面图像的输入格式，主要是传输了图像数据和配置字符串，其中图像是经过base64编码后的数据，配置字符串主要传递了一个参数，表示当前图像为身份证正面图像，进行正面识别。

返回结果示例如下：

```javascript
正面返回结果：
{
  "address"    : "浙江省杭州市余杭区文一西路969号",   #地址信息
  "config_str" : "{\\\"side\\\":\\\"face\\\"}",    #配置信息，同输入configure
  "face_rect":{       #人脸位置
    "angle": -90,   #angle表示矩形顺时针旋转的度数
    "center":{      #center表示人脸矩形中心坐标
      "x" : 952,
      "y" : 325.5
    },
    "size":{        #size表示人脸矩形长宽
      "height":181.99,
      "width":164.99
    }
  },
  "card_region":[  #身份证区域位置，四个顶点表示\
     {"x":165,"y":657},\
     {"x":534,"y":658},\
     {"x":535,"y":31},\
     {"x":165,"y":30}\
   ],
  "face_rect_vertices":[  #人脸位置，四个顶点表示\
      {\
         "x":1024.6600341796875,\
         "y":336.629638671875\
      },\
      {\
         "x":906.66107177734375,\
         "y":336.14801025390625\
      },\
      {\
         "x":907.1590576171875,\
         "y":214.1490478515625\
      },\
      {\
         "x":1025.157958984375,\
         "y":214.63067626953125\
      }\
    ],
  "name" : "张三",                 #姓名
  "nationality": "汉"，            #民族
  "num" : "1234567890",            #身份证号
  "sex" : "男",                    #性别
  "birth" : "20000101",            #出生日期
  "is_fake": false,                   #是否是复印件
  "warning": {         # 身份证质量分结果，只有当请求参数 quality_info=true 时，才会返回此字段
       "completeness_score": 100,         # 完整度评分（浮点类型）
       "is_copy": 0,          # 是否是复印件（1:是，0:否）
       "is_reshoot": 0,               # 是否是翻拍（1:是，0:否）
       "quality_score": 89.296059,         # 整体质量分数（浮点类型）
       "tamper_score": 99.99968.            # 篡改分数（数值越大表示篡改可能性越大，推荐阈值：60）
    },
  "success" : true                 #识别结果，true表示成功，false表示失败
}

反面返回结果:
{
    "config_str" : "{\\\"side\\\":\\\"back\\\"}",  #配置信息，同输入configure
    "start_date" : "19700101",       #有效期起始时间
    "end_date" : "19800101",         #有效期结束时间
    "issue" : "杭州市公安局",         #签发机关
    "is_fake": false,                   #是否是复印件
    "success" : true                 #识别结果，true表示成功，false表示失败
}
```