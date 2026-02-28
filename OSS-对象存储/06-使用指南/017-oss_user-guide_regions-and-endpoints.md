### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[开始使用](https://help.aliyun.com/zh/oss/user-guide/product-introduction/)地域和Endpoint

# 地域和Endpoint

更新时间：2026-02-05 06:34:19

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：在Cursor中使用OSS文档](https://help.aliyun.com/zh/oss/user-guide/use-the-oss-document-in-cursor)[下一篇：使用限制及性能指标](https://help.aliyun.com/zh/oss/user-guide/limits)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

公共云

亚太-中国

亚太-其他

欧洲与美洲

中东

金融云

政务云

在全球多个地域部署OSS服务时，合理选择地域和获取正确的访问地址直接影响业务性能、成本控制和合规要求。通过了解各地域特性和Endpoint配置，可实现更佳的访问性能、合理的资源配置，并满足数据合规性要求。

地域是阿里云数据中心的物理位置标识，选择地域时建议综合考虑以下因素：

- **云产品互联**：当其他云产品和OSS位于同一地域时，可通过内网互访，既免除外网流量费用，又获得更稳定的网络连接。

- **成本考虑**：各地域的产品价格和优惠政策存在差异，选择价格更优惠的地域可有效控制成本，详见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)。

- **合规要求**：不同地域或行业对数据合规性要求不同，需根据业务规范选择合适地域。

- **产品功能**：新功能在发布初期通常在部分地域进行公测，如需使用最新功能，应在指定地域创建Bucket。产品功能发布记录请参见 [新功能发布记录](https://help.aliyun.com/zh/oss/release-notes#concept-185831 "")。

- **就近原则**：选择与主要用户或应用程序距离最近的地域，可显著降低网络延迟，提升访问体验。


除上述具体地域外，针对地域属性不敏感且仅需外网访问的业务场景，OSS还提供 [无地域属性Bucket](https://help.aliyun.com/zh/oss/user-guide/region-attribute-of-buckets#1082a5f1d47ne "")。无地域属性Bucket的数据存储于中国内地的某个地域，用户无需感知具体位置信息，仅通过该Bucket的外网Endpoint进行访问。

##### **如何快速测试不同地域的网络延迟？**

使用`curl`命令快速测试本地网络到不同地域OSS Endpoint的访问延迟，辅助地域选择决策。较低的`time_connect`和`time_starttransfer`值通常表示更佳的网络质量。

```shell
# 测试到 华东1 (杭州) 的延迟
curl -o /dev/null -s -w "Connect: %{time_connect}s\nStart Transfer: %{time_starttransfer}s\nTotal: %{time_total}s\n" "https://oss-cn-hangzhou.aliyuncs.com"

# 测试到 华北2 (北京) 的延迟
curl -o /dev/null -s -w "Connect: %{time_connect}s\nStart Transfer: %{time_starttransfer}s\nTotal: %{time_total}s\n" "https://oss-cn-beijing.aliyuncs.com"
```

## **公共云**

部分海外地域名称在OSS产品定价页面和资源包购买页面中可能存在表述差异，但均指向相同的物理地理位置。例如，美国（硅谷）地域在不同页面中可能显示为美西1或美西，更多信息请参见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)或 [购买资源包](https://common-buy.aliyun.com/?spm=5176.7933691.1309819..68b22a66FQKm7f&commodityCode=ossbag&request=%7B%22region%22%3A%22china-common%22%7D#/buy)。

### **亚太-中国**

| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| 华东1（杭州） | cn-hangzhou | oss-cn-hangzhou.aliyuncs.com | oss-cn-hangzhou-internal.aliyuncs.com | cn-hangzhou.oss.aliyuncs.com | - 100.118.28.0/24<br>  <br>- 100.114.102.0/24<br>  <br>- 100.98.170.0/24<br>  <br>- 100.118.31.0/24 |
| 华东2（上海） | cn-shanghai | oss-cn-shanghai.aliyuncs.com | oss-cn-shanghai-internal.aliyuncs.com | cn-shanghai.oss.aliyuncs.com | - 100.98.35.0/24<br>  <br>- 100.98.110.0/24<br>  <br>- 100.98.169.0/24<br>  <br>- 100.118.102.0/24 |
| 华东5 （南京-本地地域-关停中） | cn-nanjing | oss-cn-nanjing.aliyuncs.com | oss-cn-nanjing-internal.aliyuncs.com | 不支持 | 100.114.142.0/24 |
| 华东6（福州-本地地域-关停中） | cn-fuzhou | oss-cn-fuzhou.aliyuncs.com | oss-cn-fuzhou-internal.aliyuncs.com | 不支持 | 100.115.21.0/24 |
| 华中1（武汉-本地地域） | cn-wuhan-lr | oss-cn-wuhan-lr.aliyuncs.com | oss-cn-wuhan-lr-internal.aliyuncs.com | 不支持 | 100.115.89.0/24 |
| 华北1（青岛） | cn-qingdao | oss-cn-qingdao.aliyuncs.com | oss-cn-qingdao-internal.aliyuncs.com | cn-qingdao.oss.aliyuncs.com | - 100.115.173.0/24<br>  <br>- 100.99.113.0/24<br>  <br>- 100.99.114.0/24<br>  <br>- 100.99.115.0/24 |
| 华北2（北京） | cn-beijing | oss-cn-beijing.aliyuncs.com | oss-cn-beijing-internal.aliyuncs.com | cn-beijing.oss.aliyuncs.com | - 100.118.58.0/24<br>  <br>- 100.118.167.0/24<br>  <br>- 100.118.170.0/24<br>  <br>- 100.118.171.0/24<br>  <br>- 100.118.172.0/24<br>  <br>- 100.118.173.0/24 |
| 华北3（张家口） | cn-zhangjiakou | oss-cn-zhangjiakou.aliyuncs.com | oss-cn-zhangjiakou-internal.aliyuncs.com | cn-zhangjiakou.oss.aliyuncs.com | - 100.118.90.0/24<br>  <br>- 100.98.159.0/24<br>  <br>- 100.114.0.0/24<br>  <br>- 100.114.1.0/24 |
| 华北5（呼和浩特） | cn-huhehaote | oss-cn-huhehaote.aliyuncs.com | oss-cn-huhehaote-internal.aliyuncs.com | cn-huhehaote.oss.aliyuncs.com | - 100.118.195.0/24<br>  <br>- 100.99.110.0/24<br>  <br>- 100.99.111.0/24<br>  <br>- 100.99.112.0/24 |
| 华北6（乌兰察布） | cn-wulanchabu | oss-cn-wulanchabu.aliyuncs.com | oss-cn-wulanchabu-internal.aliyuncs.com | cn-wulanchabu.oss.aliyuncs.com | - 100.114.11.0/24<br>  <br>- 100.114.12.0/24<br>  <br>- 100.114.100.0/24<br>  <br>- 100.118.214.0/24 |
| 华南1（深圳） | cn-shenzhen | oss-cn-shenzhen.aliyuncs.com | oss-cn-shenzhen-internal.aliyuncs.com | cn-shenzhen.oss.aliyuncs.com | - 100.118.78.0/24<br>  <br>- 100.118.203.0/24<br>  <br>- 100.118.204.0/24<br>  <br>- 100.118.217.0/24 |
| 华南2（河源） | cn-heyuan | oss-cn-heyuan.aliyuncs.com | oss-cn-heyuan-internal.aliyuncs.com | cn-heyuan.oss.aliyuncs.com | - 100.98.83.0/24<br>  <br>- 100.118.174.0/24 |
| 华南3（广州） | cn-guangzhou | oss-cn-guangzhou.aliyuncs.com | oss-cn-guangzhou-internal.aliyuncs.com | cn-guangzhou.oss.aliyuncs.com | - 100.115.33.0/24<br>  <br>- 100.114.101.0/24 |
| 西南1（成都） | cn-chengdu | oss-cn-chengdu.aliyuncs.com | oss-cn-chengdu-internal.aliyuncs.com | cn-chengdu.oss.aliyuncs.com | - 100.115.155.0/24<br>  <br>- 100.99.107.0/24<br>  <br>- 100.99.108.0/24<br>  <br>- 100.99.109.0/24 |
| 中国香港 | cn-hongkong | oss-cn-hongkong.aliyuncs.com | oss-cn-hongkong-internal.aliyuncs.com | cn-hongkong.oss.aliyuncs.com | - 100.115.61.0/24<br>  <br>- 100.99.103.0/24<br>  <br>- 100.99.104.0/24<br>  <br>- 100.99.106.0/24 |
| [无地域属性](https://help.aliyun.com/zh/oss/user-guide/region-attribute-of-buckets#1082a5f1d47ne "") | rg-china-mainland | oss-rg-china-mainland.aliyuncs.com | 不支持 | 不支持 | 不支持 |

### **亚太-其他**

| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| 日本（东京） | ap-northeast-1 | oss-ap-northeast-1.aliyuncs.com | oss-ap-northeast-1-internal.aliyuncs.com | 不支持 | - 100.114.211.0/24<br>  <br>- 100.114.114.0/25 |
| 韩国（首尔） | ap-northeast-2 | oss-ap-northeast-2.aliyuncs.com | oss-ap-northeast-2-internal.aliyuncs.com | 不支持 | 100.99.119.0/24 |
| 新加坡 | ap-southeast-1 | oss-ap-southeast-1.aliyuncs.com | oss-ap-southeast-1-internal.aliyuncs.com | 不支持 | - 100.118.219.0/24<br>  <br>- 100.99.213.0/24<br>  <br>- 100.99.116.0/24<br>  <br>- 100.99.117.0/24 |
| 马来西亚（吉隆坡） | ap-southeast-3 | oss-ap-southeast-3.aliyuncs.com | oss-ap-southeast-3-internal.aliyuncs.com | 不支持 | - 100.118.165.0/24<br>  <br>- 100.99.125.0/24<br>  <br>- 100.99.130.0/24<br>  <br>- 100.99.131.0/24 |
| 印度尼西亚（雅加达） | ap-southeast-5 | oss-ap-southeast-5.aliyuncs.com | oss-ap-southeast-5-internal.aliyuncs.com | 不支持 | 100.114.98.0/24 |
| 菲律宾（马尼拉） | ap-southeast-6 | oss-ap-southeast-6.aliyuncs.com | oss-ap-southeast-6-internal.aliyuncs.com | 不支持 | 100.115.16.0/24 |
| 泰国（曼谷） | ap-southeast-7 | oss-ap-southeast-7.aliyuncs.com | oss-ap-southeast-7-internal.aliyuncs.com | 不支持 | 100.98.249.0/24 |

### **欧洲与美洲**

| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| 德国（法兰克福） | eu-central-1 | oss-eu-central-1.aliyuncs.com | oss-eu-central-1-internal.aliyuncs.com | eu-central-1.oss.aliyuncs.com | 100.115.154.0/24 |
| 英国（伦敦） | eu-west-1 | oss-eu-west-1.aliyuncs.com | oss-eu-west-1-internal.aliyuncs.com | 不支持 | 100.114.114.128/25 |
| 美国（硅谷） | us-west-1 | oss-us-west-1.aliyuncs.com | oss-us-west-1-internal.aliyuncs.com | 不支持 | 100.115.107.0/24 |
| 美国（弗吉尼亚） | us-east-1 | oss-us-east-1.aliyuncs.com | oss-us-east-1-internal.aliyuncs.com | 不支持 | - 100.115.60.0/24<br>  <br>- 100.99.100.0/24<br>  <br>- 100.99.101.0/24<br>  <br>- 100.99.102.0/24 |
| 墨西哥 | na-south-1 | oss-na-south-1.aliyuncs.com | oss-na-south-1-internal.aliyuncs.com | 不支持 | 100.115.112.0/27 |

### **中东**

| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| 阿联酋（迪拜） | me-east-1 | oss-me-east-1.aliyuncs.com | oss-me-east-1-internal.aliyuncs.com | 不支持 | 100.99.235.0/24 |

## **金融云**

| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| 华东1 金融云 | cn-hangzhou-finance | 不支持 | oss-cn-hzjbp-a-internal.aliyuncs.com<br>oss-cn-hzjbp-b-internal.aliyuncs.com | 不支持 | - 100.103.4.210/32<br>  <br>- 100.115.6.0/24 |
| 华东2 金融云 | cn-shanghai-finance-1 | 不支持 | oss-cn-shanghai-finance-1-internal.aliyuncs.com | 不支持 | - 100.115.105.0/24<br>  <br>- 100.100.36.8/32 |
| 华南1 金融云 | cn-shenzhen-finance-1 | 不支持 | oss-cn-shenzhen-finance-1-internal.aliyuncs.com | 不支持 | 100.112.15.0/24 |
| 华北2 金融云（邀测） | cn-beijing-finance-1 | 不支持 | oss-cn-beijing-finance-1-internal.aliyuncs.com | 不支持 | 100.112.52.0/24 |
| 杭州金融云外网 | cn-hangzhou-finance | oss-cn-hzfinance.aliyuncs.com | oss-cn-hzfinance-internal.aliyuncs.com | cn-hangzhou-finance.oss.aliyuncs.com | - 100.103.4.95/32<br>  <br>- 100.103.5.142/32<br>  <br>- 100.103.5.143/32<br>  <br>- 100.103.5.144/32<br>  <br>- 100.115.6.0/24 |
| 上海金融云外网 | cn-shanghai-finance-1 | oss-cn-shanghai-finance-1-pub.aliyuncs.com | oss-cn-shanghai-finance-1-pub-internal.aliyuncs.com | cn-shanghai-finance.oss.aliyuncs.com | - 100.100.36.24/32<br>  <br>- 100.100.36.8/32 |
| 深圳金融云外网 | cn-shenzhen-finance-1 | oss-cn-szfinance.aliyuncs.com | oss-cn-szfinance-internal.aliyuncs.com | cn-shenzhen-finance.oss.aliyuncs.com | - 100.112.15.0/24<br>  <br>- 100.100.80.70/32 |
| 北京金融云外网 | cn-beijing-finance-1 | oss-cn-beijing-finance-1-pub.aliyuncs.com | oss-cn-beijing-finance-1-pub-internal.aliyuncs.com | 不支持 | 100.112.52.0/24 |

## **政务云**

| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **地域** | **地域ID** | **外网Endpoint** | **内网Endpoint** | **双栈Endpoint** | **内网VIP网段** |
| 华北2 阿里政务云1 | cn-north-2-gov-1 | oss-cn-north-2-gov-1.aliyuncs.com | oss-cn-north-2-gov-1-internal.aliyuncs.com | cn-north-2-gov-1.oss.aliyuncs.com | 不支持 |