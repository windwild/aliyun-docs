### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 搜索Demo

# 搜索Demo

更新时间：2024-11-22 04:43:39

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：动态与公告](https://help.aliyun.com/zh/open-search/announcements-and-updates)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

配置环境变量

引入依赖

搜索示例

## **配置环境变量**

配置环境变量 **ALIBABA\_CLOUD\_ACCESS\_KEY\_ID** 和 **ALIBABA\_CLOUD\_ACCESS\_KEY\_SECRET**。

**重要**

- 阿里云账号AccessKey拥有所有API的访问权限，建议您使用RAM用户进行API访问或日常运维，具体操作，请参见 [创建RAM用户](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "")。

- 创建AccessKey ID和AccessKey Secret，请参考 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "")。

- 如果您使用的是RAM用户的AccessKey，请确保主账号已授权AliyunServiceRoleForOpenSearch服务关联角色，请参考 [OpenSearch-行业算法版服务关联角色](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/aliyunserviceroleforopensearch "")，相关文档参考 [访问鉴权规则](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/access-authorization-rules "")。

- 请不要将AccessKey ID和AccessKey Secret保存到工程代码里，否则可能导致AccessKey泄露，威胁您账号下所有资源的安全。


- **Linux** 和 **macOS系统** 配置方法：

执行以下命令，其中，`<access_key_id>`需替换为您RAM用户的AccessKey ID，`<access_key_secret>`替换为您RAM用户的AccessKey Secret。















```java
export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
```

- **Windows系统** 配置方法

1. 新建环境变量文件，添加环境变量 **ALIBABA\_CLOUD\_ACCESS\_KEY\_ID** 和 **ALIBABA\_CLOUD\_ACCESS\_KEY\_SECRET**，并写入已准备好的AccessKey ID和AccessKey Secret。

2. 重启Windows系统生效。

### 引入依赖

```xml
pip install alibabacloud_tea_util
pip install alibabacloud_opensearch_util
pip install alibabacloud_credentials
```

BaseRequest参考： [Python client 示例](https://help.aliyun.com/zh/open-search/llm-intelligent-q-a-version/python-client-example "")

### 搜索示例

```python
# -*- coding: utf-8 -*-

import time, os
from typing import Dict, Any

from Tea.exceptions import TeaException
from Tea.request import TeaRequest
from alibabacloud_tea_util import models as util_models
from BaseRequest import Config, Client

class LLMSearch:
    def __init__(self, config: Config):
        self.Clients = Client(config=config)
        self.runtime = util_models.RuntimeOptions(
            connect_timeout=10000,
            read_timeout=10000,
            autoretry=False,
            ignore_ssl=False,
            max_idle_conns=50,
            max_attempts=3
        )
        self.header = {}

    def searchDoc(self, app_name: str,body:Dict, query_params: dict={}) -> Dict[str, Any]:
        try:
            response = self.Clients._request(method="POST", pathname=f'/v3/openapi/apps/{app_name}/actions/knowledge-search',
                                             query=query_params, headers=self.header, body=body, runtime=self.runtime)
            return response
        except TeaException as e:
            print(e)

if __name__ == "__main__":
    # 配置统一的请求入口和  需要去掉http://
    endpoint = "<endpoint>"

    # 支持 protocol 配置 HTTPS/HTTP
    endpoint_protocol = "HTTP"

    # 用户识别信息
    # 从环境变量读取配置的AccessKey ID和AccessKey Secret，
    # 运行代码示例前必须先配置环境变量，参考文档上面“配置环境变量”步骤
    access_key_id = os.environ.get("ALIBABA_CLOUD_ACCESS_KEY_ID")
    access_key_secret = os.environ.get("ALIBABA_CLOUD_ACCESS_KEY_SECRET")

    # 支持 type 配置 sts/access_key 鉴权. 其中 type 默认为 access_key 鉴权. 使用 sts 可配置 RAM-STS 鉴权.
    # 使用 access_key 鉴权
    # auth_type = "access_key"
    # type和security_token 参数如果不是子账号，需要省略
    # 配置请求使用的通用信息.
    # Configs = Config(endpoint=endpoint, access_key_id=access_key_id, access_key_secret=access_key_secret,
    #                  type=auth_type, protocol=endpoint_protocol)

    # 如果使用 RAM-STS 鉴权, 请配置 security_token, 可使用 阿里云 AssumeRole 获取 相关 STS 鉴权结构.
    auth_type = "sts"
    security_token =  "<security_token>"

    # 配置请求使用的通用信息.
     Configs = Config(endpoint=endpoint, access_key_id=access_key_id, access_key_secret=access_key_secret,
                      security_token=security_token, type=auth_type, protocol=endpoint_protocol)

    # 创建 opensearch 实例
    ops = LLMSearch(Configs)
    app_name = "替换为应用id"

    # --------------- 文档搜索 ---------------

    docQuery = {"question": {"text": "搜索", "type": "TEXT"}}

    res1 = ops.searchDoc(app_name=app_name, body=docQuery)
    print(res1)
```

**说明**

更多查询参数可参考 [问答参数说明](https://help.aliyun.com/zh/open-search/parameter-description "")