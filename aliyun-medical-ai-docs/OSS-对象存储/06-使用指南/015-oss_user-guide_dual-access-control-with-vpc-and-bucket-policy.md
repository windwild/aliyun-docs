### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[权限与访问控制](https://help.aliyun.com/zh/oss/user-guide/permissions-and-access-controls/)[Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/)基于VPC Policy和Bucket Policy实现双重访问控制

# 基于VPC Policy和Bucket Policy实现双重访问控制

更新时间：2026-01-14 03:48:43

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/)[下一篇：基于Bucket Policy实现跨部门数据共享](https://help.aliyun.com/zh/oss/user-guide/cross-departmental-data-sharing-based-on-bucket-policy)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

方案介绍

方案实现

步骤一：配置VPC Policy

步骤二：配置Bucket Policy

步骤三：验证访问控制效果

结合VPC Policy和Bucket Policy配置双重访问控制机制，从网络来源和资源两个层面实现对OSS的访问控制，确保云上数据仅在安全的网络环境内被授权访问，有效防范未授权访问和数据泄露风险。

## **方案介绍**

相比单纯依赖Bucket Policy进行目的端验证，双重控制方案通过VPC Policy和Bucket Policy组合形成 **源端授权+目的端验证** 的多层安全防护体系，显著提升数据访问安全性。VPC Policy在网络源端预先限制可访问的Bucket范围，实现细粒度权限管理和风险隔离；Bucket Policy在存储目的端验证访问来源，确保仅来自授权VPC的请求可以访问资源。

- **允许访问**：在授权VPC内访问授权的Bucket资源时，双端策略同时放行。

- **拒绝访问**：

  - VPC Policy拒绝：在授权VPC内尝试访问未被VPC Policy授权的Bucket资源。

  - Bucket Policy拒绝：在非授权VPC内尝试访问Bucket资源。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1250838671/CAEQZRiBgMD46d.N1xkiIGQwNTQ4OWIwNWRlYTQxODJiYzZlNWM1MWYwMTNhYmNm5931911_20251203162451.549.svg)

## **方案实现**

以下通过具体场景演示双重访问控制的配置过程。某企业用户（UID为`174649585760xxxx`）在OSS中创建了名为`example-bucket`的存储空间用于存放重要业务数据，同时在ID为`vpc-t4nlw426y44rd3iq4xxxx`的专有网络VPC内运行多台ECS实例。为遵循最小权限原则，使用RAM用户`example-user`（UID为`20655703638807****`）的AccessKey进行业务访问。需要实现以下访问控制目标：

- **VPC源端控制**：限制VPC仅允许访问OSS指定资源`example-bucket`。

- **Bucket目的端控制**：拒绝所有非当前VPC的OSS访问请求。


### **步骤一：配置VPC Policy**

为ID为`vpc-t4nlw426y44rd3iq4xxxx`的专有网络VPC创建终端节点策略，限制其仅能访问OSS中`example-bucket`下的资源。

1. 前往 [专有网络VPC控制台](https://vpcnext.console.aliyun.com/)，在左侧菜单栏单击 **终端节点**。

2. 单击 **创建终端节点**，按以下说明配置终端节点。


> 首次使用需 **开通私网连接服务**。


   - **所属地域**：选择VPC所在地域，如华东1（杭州）。

   - **节点名称**：输入终端节点名称。

   - **终端节点类型**：选择 **网关终端节点**。

   - **终端节点服务**：选择 **阿里云服务**，在服务列表中选择OSS终端节点服务（服务名称以`oss`结尾的条目）。

   - **专有网络**：选择目标专有网络。

   - **路由表**：选择目标路由表。

   - **终端节点策略**：在编辑器内输入以下策略。















     ```json
     {
       "Version": "1",
       "Statement": [\
         {\
           "Effect": "Allow",\
           "Action": "oss:*",\
           "Principal": [\
             "20655703638807****"\
           ],\
           "Resource": [\
             "acs:oss:*:*:example-bucket",\
             "acs:oss:*:*:example-bucket/*"\
           ]\
         }\
       ]
     }
     ```
3. 确认配置无误后，单击 **确定创建**。


### **步骤二：配置Bucket Policy**

配置Bucket Policy，拒绝ID不为`vpc-t4nlw426y44rd3iq4xxxx`的VPC网络请求访问OSS资源。

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket。

2. 在Bucket左侧菜单栏单击**权限控制** \> **Bucket授权策略**。

3. 选择 **按语法策略添加**，然后单击 **编辑**，在编辑器内输入以下策略。















```json
{
     "Statement": [\
       {\
         "Action": [\
           "oss:*"\
         ],\
         "Effect": "Deny",\
         "Principal": [\
           "20655703638807****"\
         ],\
         "Resource": "acs:oss:*:*:*",\
         "Condition": {\
           "StringNotEquals": {\
             "acs:SourceVpc": [\
               "vpc-t4nlw426y44rd3iq4xxxx"\
             ]\
           }\
         }\
       }\
     ],
     "Version": "1"
}
```

4. 确认授权策略无误后，单击 **保存**，根据页面提示保存授权策略。


### **步骤三：验证访问控制效果**

以下通过ossutil命令行工具验证双重访问控制的实际效果。使用命令前需先下载 [命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/ "") 并使用RAM用户的AccessKey和内网访问地址（如`oss-cn-hangzhou-internal.aliyuncs.com`）进行配置。

#### **验证允许访问场景**

在授权VPC（`vpc-t4nlw426y44rd3iq4xxxx`）内的ECS实例上，使用授权用户（UID为`20655703638807****`）的AccessKey访问`example-bucket`，如列举Bucket中的文件。

```bash
ossutil ls oss://example-bucket/
```

访问成功，说明双端策略均放行。

#### **验证VPC Policy拒绝场景**

在同一VPC内尝试访问未被VPC Policy授权的其他Bucket（如`other-bucket`）。

```bash
ossutil ls oss://other-bucket/
```

访问被拒绝，提示`Access denied by VPC endpoint policy..`，说明VPC Policy在源端成功限制了可访问的Bucket范围。

#### **验证Bucket Policy拒绝场景**

在非授权VPC或公网环境中，使用同一用户的AccessKey访问`example-bucket`。

```bash
ossutil ls oss://example-bucket/
```

访问被拒绝，提示`Access denied by bucket policy..`，说明Bucket Policy在目的端成功验证了VPC来源。