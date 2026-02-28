### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[安全合规](https://help.aliyun.com/zh/sls/security-compliance/)[使用RAM进行访问控制](https://help.aliyun.com/zh/sls/use-ram-for-access-control-sls/)[服务关联角色](https://help.aliyun.com/zh/sls/service-association-role-sls/)管理服务关联角色AliyunServiceRoleForSLSMiddlewareLens

# 管理服务关联角色AliyunServiceRoleForSLSMiddlewareLens

更新时间：2023-10-26 03:08:57

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：管理服务关联角色AliyunServiceRoleForSLSAILens](https://help.aliyun.com/zh/sls/aliyunserviceroleforslsailens-role)[下一篇：管理服务关联角色AliyunServiceRoleForSLSSecurityLens](https://help.aliyun.com/zh/sls/aliyunserviceroleforslssecuritylens-role)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

应用场景

权限策略

您可以授予日志服务应用（例如日志审计服务、CloudLens等）使用SLS日志服务关联角色（AliyunServiceRoleForSLSMiddlewareLens）来获取中间件云产品的资源。本文介绍AliyunServiceRoleForSLSMiddlewareLens角色的应用场景和权限策略。

## 应用场景

当您通过日志服务应用（例如日志审计服务、CloudLens等）采集中间件云产品日志时，日志服务会调用相关云产品的OpenAPI接口获取采集账号下的云产品信息。此过程中，日志服务需要通过AliyunServiceRoleForSLSMiddlewareLens角色获取中间件云产品的部分读取及日志采集相关的部分修改权限。更多信息，请参见 [服务关联角色](https://help.aliyun.com/zh/ram/user-guide/service-linked-roles#concept-2448621 "")。

## 权限策略

- 角色名称：AliyunServiceRoleForSLSMiddlewareLens
- 角色权限策略名称：AliyunServiceRolePolicyForSLSMiddlewareLens
- 权限策略：















```plaintext
{
      "Version": "1",
      "Statement": [\
          {\
              "Action": [\
                  "sae:DescribeApplicationConfig"\
              ],\
              "Resource": "*",\
              "Effect": "Allow"\
          },\
          {\
              "Action": [\
                  "log:CreateProject",\
                  "log:GetProject",\
                  "log:ListProject",\
                  "log:ListLogStores",\
                  "log:GetLogStore",\
                  "log:CreateIndex",\
                  "log:UpdateIndex",\
                  "log:GetIndex",\
                  "log:CreateDashboard",\
                  "log:UpdateDashboard",\
                  "log:ListDashboard",\
                  "log:CreateLogStore",\
                  "log:CreateSavedSearch",\
                  "log:UpdateSavedSearch"\
              ],\
              "Resource": [\
                  "acs:log:*:*:project/*"\
              ],\
              "Effect": "Allow"\
          },\
          {\
              "Action": "ram:DeleteServiceLinkedRole",\
              "Resource": "*",\
              "Effect": "Allow",\
              "Condition": {\
                  "StringEquals": {\
                      "ram:ServiceName": "middlewarelens.log.aliyuncs.com"\
                  }\
              }\
          }\
      ]
}
```