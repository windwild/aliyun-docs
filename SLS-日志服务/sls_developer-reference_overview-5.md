### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[开发参考](https://help.aliyun.com/zh/sls/developer-reference/)[API参考附录](https://help.aliyun.com/zh/sls/developer-reference/api-reference-appendix/)[鉴权规则](https://help.aliyun.com/zh/sls/developer-reference/ram-authentication-rules/)概览

# 概览

更新时间：2023-10-26 02:48:03

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：错误码](https://help.aliyun.com/zh/sls/developer-reference/error-codes)[下一篇：资源列表](https://help.aliyun.com/zh/sls/developer-reference/resource-list)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

背景信息

授权策略

更多信息

本文介绍借助RAM实现RAM用户对主账号日志服务资源的访问。

## 背景信息

您创建的Project、Logstore、采集配置、机器组，都是您自己拥有的资源。默认情况下，您对自己的资源拥有完整的操作权限，可以使用本文档中列举的所有API对资源进行操作。

但在RAM用户场景下，刚创建的RAM用户无权限操作主账号资源，需要通过RAM授权方式，授予RAM用户操作主账号资源的权限。

**说明**

在了解如何使用RAM来授权和访问日志服务资源之前，请确保您已详细阅读了 [创建可信实体为阿里云账号的RAM角色及授权](https://help.aliyun.com/zh/sls/create-a-ram-role-whose-trusted-entity-is-an-alibaba-cloud-account-and-authorize-the-ram-role-to-access-log-service#concept-jtj-s4q-zdb "") 和 [RAM简介](https://help.aliyun.com/zh/sls/overview-8#concept-hgk-q4q-zdb "")。

如果您不需要跨账户进行日志服务资源的授权和访问，您可以跳过此章节。跳过这些部分并不影响您对文档中其余部分的理解和使用。

## 授权策略

RAM和日志服务相关的授权策略：

- AliyunLogFullAccess
给RAM用户授予该权限后，RAM用户将对主账号拥有的日志服务资源具备访问权限。授权策略描述如下：
















```plaintext
    {
      "Version": "1",
      "Statement": [\
        {\
          "Action": "log:*",\
          "Resource": "*",\
          "Effect": "Allow"\
        }\
      ]
    }
```

- AliyunLogReadOnlyAccess
给RAM用户授予该权限后，RAM用户将对主账号拥有的日志服务资源具备只读权限。授权策略描述如下：
















```plaintext
{
      "Version": "1",
      "Statement": [\
        {\
          "Action": [\
            "log:Get*",\
            "log:List*"\
          ],\
          "Resource": "*",\
          "Effect": "Allow"\
        }\
      ]
    }
```

- 向指定日志库（Logstore）上传数据
给RAM用户授予该权限后，RAM用户可以通过API、SDK直接向指定日志库上传数据，授权策略描述如下：















```plaintext
    {
      "Version": "1",
      "Statement": [\
        {\
          "Action": [\
            "log:Post*",\
            "log:BatchPost*"\
          ],\
          "Resource": ["acs:log:*:*:project/<指定的project名称>/logstore/<指定的logstore名称>"],\
          "Effect": "Allow"\
        }\
      ]
    }
```

- 控制台查询指定日志库（Logstore）数据
给RAM用户授予该权限后，RAM用户在控制台上拥有指定日志库资源的只读访问权限（查询日志、拖取日志、查看日志库列表）。授权策略描述如下：
















```plaintext
    {
      "Version": "1",
      "Statement": [\
        {\
          "Action": ["log:List*"],\
          "Resource": ["acs:log:*:*:project/<指定的project名称>/*"],\
          "Effect": "Allow"\
        },\
        {\
          "Action": ["log:Get*"],\
          "Resource": ["acs:log:*:*:project/<指定的project名称>/logstore/<指定的logstore名称>"],\
          "Effect": "Allow"\
        }\
      ]
    }
```


## 更多信息

- [RAM中可授权的Log Service资源类型](https://help.aliyun.com/zh/sls/developer-reference/resource-list#reference-sdz-l5q-12b "")
- [RAM中可对Log Service资源进行授权的Action](https://help.aliyun.com/zh/sls/action-list#reference-zq5-m5q-12b "")
- [Log Service API发生RAM用户访问主账号资源时的鉴权规则](https://help.aliyun.com/zh/sls/developer-reference/ram-authentication-rules-1#reference-hkk-n5q-12b "")