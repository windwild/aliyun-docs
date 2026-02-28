### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据采集](https://help.aliyun.com/zh/sls/data-collection-1/)[LoongCollector数据采集器（原Logtail）](https://help.aliyun.com/zh/sls/loongcollector-management/)[Windows 安装与管理](https://help.aliyun.com/zh/sls/loongcollector-installation-and-management-windows/)LoongCollector安装（Windows）

# LoongCollector安装（Windows）

更新时间：2026-02-01 21:55:02

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置管理](https://help.aliyun.com/zh/sls/loongcollector-management-linux)[下一篇：安装配置](https://help.aliyun.com/zh/sls/loongcollector-installation-kubernetes-1)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

前提条件

安装LoongCollector

相关参考

地域

LoongCollector网络传输类型

LoongCollector是日志服务提供的采集器。采集Windows服务器上的日志需要先在服务器上安装LoongCollector客户端，请根据服务器与日志服务Project的关系选择合适的安装方式。

## **使用限制**

- 支持的Windows操作系统



**重要**





目前只支持X86\_64版本的操作系统。





Microsoft Windows Server 2008、2012、2016、2019、2022、2025

Microsoft Windows 7

Microsoft Windows 10

Microsoft Windows 11

Microsoft Windows Server Version 1909

Microsoft Windows Server Version 2004


## **前提条件**

**权限须知**

如果您使用阿里云主账号登录，默认拥有所有操作权限，可直接进行相关操作。

若您使用RAM用户登录，请根据需要向主账号使用者申请如下系统策略以获得管理日志服务、ECS与OOS资源的权限。

- AliyunLogFullAccess：授予管理日志服务的权限。

- AliyunOOSFullAccess：授予管理OOS的权限，可执行OOS自动编排安装loongcollector。

- AliyunECSFullAccess：授予管理ECS的权限，可执行ECS云助手命令批量安装loongcollector。


当系统策略无法满足您的需求，您可以参考下表通过 [创建自定义权限策略](https://help.aliyun.com/zh/ram/create-a-custom-policy "") 实现精细化权限管理。

> 请将Resource中的`${projectName}`替换为您需要访问的Project名称。

```json
{
  "Version": "1",
  "Statement": [\
    {\
      "Effect": "Allow",\
      "Action": [\
        "ecs:DescribeTagKeys",\
        "ecs:DescribeTags",\
        "ecs:DescribeInstances",\
        "ecs:DescribeInvocationResults",\
        "ecs:RunCommand",\
        "ecs:DescribeInvocations",\
        "ecs:InvokeCommand"\
      ],\
      "Resource": "*"\
    },\
    {\
      "Effect": "Allow",\
      "Action": [\
        "oos:ListTemplates",\
        "oos:StartExecution",\
        "oos:ListExecutions",\
        "oos:GetExecutionTemplate",\
        "oos:ListExecutionLogs",\
        "oos:ListTaskExecutions"\
      ],\
      "Resource": "*"\
    },\
    {\
      "Effect": "Allow",\
      "Action": [\
        "log:ListProject",\
        "log:GetAcceleration",\
        "log:ListDomains",\
        "log:GetLogging",\
        "log:ListTagResources"\
      ],\
      "Resource": [\
        "acs:log:*:*:project/*"\
      ]\
    },\
    {\
      "Effect": "Allow",\
      "Action": [\
        "log:GetProject"\
      ],\
      "Resource": [\
        "acs:log:*:*:project/${projectName}"\
      ]\
    },\
    {\
      "Effect": "Allow",\
      "Action": [\
        "log:ListLogStores",\
        "log:GetLogStore",\
        "log:GetLogStoreHistogram",\
        "log:GetIndex",\
        "log:CreateIndex",\
        "log:UpdateIndex",\
        "log:ListShards",\
        "log:GetCursorOrData",\
        "log:ListSavedSearch",\
        "log:GetLogStoreLogs",\
        "log:ListDashboard",\
        "log:GetLogStoreContextLogs"\
      ],\
      "Resource": [\
        "acs:log:*:*:project/${projectName}/*"\
      ]\
    },\
    {\
      "Effect": "Allow",\
      "Action": [\
        "log:*"\
      ],\
      "Resource": [\
        "acs:log:*:*:project/${projectName}/logtailconfig/*",\
        "acs:log:*:*:project/${projectName}/machinegroup/*"\
      ]\
    }\
  ]
}
```

**创建Project**

若您无可用Project，请参考此处步骤创建一个基础Project，如需详细了解创建配置请参见 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#section-ahq-ggx-ndb "")。

登录[日志服务控制台](https://sls.console.aliyun.com/)，单击 **创建Project**，完成下述基础配置，其他配置保持默认即可：

- **所属地域**：请根据日志来源等信息选择合适的阿里云地域，创建后不可修改。

- **Project名称**：设置名称，名称在阿里云地域内全局唯一，创建后不可修改。


**创建Logstore**

若您无可用Logstore，请参考此处步骤创建一个基础Logstore，如需详细了解创建配置请参见 [管理LogStore](https://help.aliyun.com/zh/sls/manage-a-logstore "")。

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)，在Project列表中单击目标Project。

2. 在**日志存储** \> **日志库**页签中，单击 **+** 图标。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2410973271/p834639.png)

3. 填写 **Logstore名称**，其余配置保持默认无需修改。


**服务器网络要求**

1. 安装LoongCollector的机器需在出口方向开放80（HTTP）端口和443（HTTPS）端口，供LoongCollector上传数据。

2. 安装LoongCollector的机器至少需要保证能够连通下列地址：

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)，在Project列表中，单击目标Project。

2. 单击Project名称右侧的![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6586464571/p995186.png)进入项目概览页面。

3. 在访问域名中可查看当前Project的域名信息，根据 [LoongCollector网络传输类型](https://help.aliyun.com/zh/sls/loongcollector-installation-windows#63125f449cdpv "") 选择替换后执行命令。


      - 传输方式为内网传输，替换`${project名称}`为Project名称，`${域名信息}`为私网域名。

      - 传输方式为公网传输，替换`${project名称}`为Project名称，`${域名信息}`为公网域名。


```shell
curl https://${project名称}.${域名信息}
```

4. 返回类似信息`{"Error":{"Code":"OLSInvalidMethod","Message":"The script name is invalid : /","RequestId":"5D****09"}}`，说明网络畅通。否则检查目标地址是否被拦截以及其他网络方面的检查（例如DNS配置、安全组等）。


      > 返回Error信息是因为访问链接缺少必要参数。当前测试仅验证网络连通性，未使用完整链接，因此在网络正常的情况下会显示Error的提示信息。

## **安装LoongCollector**

1. 登录目标服务器，下载LoongCollector安装包。

   - 国内地域： [LoongCollector国内地域安装包](https://aliyun-observability-release-cn-hangzhou.oss-cn-hangzhou.aliyuncs.com/loongcollector/win64/3.1.7/x86_64/loongcollector_installer.zip)。

   - 海外地域： [LoongCollector海外地域安装包](https://aliyun-observability-release-ap-southeast-1.oss-ap-southeast-1.aliyuncs.com/loongcollector/win64/3.1.7/x86_64/loongcollector_installer.zip)。
2. 解压缩`loongcollector_installer.zip`到当前目录。

3. 根据 [LoongCollector网络传输类型](https://help.aliyun.com/zh/sls/loongcollector-installation-windows#63125f449cdpv "") 选择并执行安装命令。

1. 以管理员身份运行Windows PowerShell，进入`loongcollector_installer`目录（您的安装包的解压目录）。

2. 选择传输方式并执行安装命令：替换`${region_id}`为Project所属地域的 [RegionID](https://help.aliyun.com/zh/sls/loongcollector-installation-windows#0de41eca64tqj "")。

      - 内网：服务器和日志服务Project位于同一地域。















        ```powershell
        .\loongcollector_installer.exe install ${region_id}
        ```

      - 公网：适用于大多数场景，常见于跨地域或其他云/自建服务器，但受带宽限制且可能不稳定。















        ```powershell
        .\loongcollector_installer.exe install ${region_id}-internet
        ```

      - 传输加速：用于跨地域（如中国内地到海外），通过CDN加速提升性能，避免公网延迟高，传输不稳定问题，但流量需额外计费。


        > 需要先打开Project的 [日志跨域传输加速](https://help.aliyun.com/zh/sls/manage-a-project/#37a0b2e104zi8 "") 功能，再执行安装命令。
















        ```powershell
        .\loongcollector_installer.exe install ${region_id}-acceleration
        ```
4. 配置用户ID：用户ID文件包含Project所属阿里云主账号的ID信息，用于标识该账号有权限访问、采集这台服务器的日志。


> 只有在采集非本账号ECS、自建服务器、其他云厂商服务器日志时需要配置用户ID。多个账号对同一台服务器进行日志采集时，支持在同一台服务器上创建多个用户ID文件。


1. 登录[日志服务控制台](https://sls.console.aliyun.com/)，鼠标悬浮在右上角用户头像上，在弹出的标签页中查看并复制账号ID。注意需要复制主账号ID。

2. 在安装了LoongCollector的服务器上指定目录`C:\LogtailData\users`下创建阿里云账号ID文件，以主账号ID作为文件名，无需配置文件后缀。![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4246073671/p1028689.png)
5. 配置机器组：日志服务通过机器组发现用户自定义标识并与主机上的LoongCollector建立心跳连接。

1. 在指定目录`C:\LogtailData`下创建user\_defined\_id文件。


      > 如果目录C:\\LogtailData不存在，请手动创建。

2. 在服务器上将自定义字符串`user-defined-test-1`写入用户自定义标识文件C:\\LogtailData\\user\_defined\_id，该字符串将在后续步骤中使用。


      - > 同一机器组中不允许同时存在Linux服务器、Windows服务器，即请勿在Linux和Windows服务器上配置相同的用户自定义标识。

      - > 一个服务器可配置多个用户自定义标识，标识之间以换行符分割。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4246073671/p1028694.png)

3. 登录[日志服务控制台](https://sls.console.aliyun.com/)。在Project列表中，单击目标Project。

4. 单击![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3423261571/p982429.png) **资源**，单击 **机器组**。

5. 单击 **机器组** 右侧的![image](<Base64-Image-Removed>)，单击 **创建机器组**。![image](<Base64-Image-Removed>)

6. 进行如下配置后单击 **确定**。

      - 设置机器组名称：名称Project内唯一，必须以小写字母或数字开头和结尾，且只能包含小写字母、数字、连字符（-）和下划线（\_），长度为3~128字符。

      - **机器组标识：** 选择 **用户自定义标识**。

      - 用户自定义标识：输入配置的用户自定义标识，需要与服务器用户自定义标识文件中自定义字符串内容一致。此例为`user-defined-test-1`。
6. 机器组创建完成后，在机器组列表单击目标机器组，在机器组状态中查看 **心跳** 状态，若为FAIL，请等待两分钟左右并手动刷新。如果心跳为OK则表示创建成功。

7. 安装完成后若需要采集日志还需进行 [采集配置](https://help.aliyun.com/zh/sls/host-text-log-collection-auto-install#10b4e861fcxh0 "")。


## **相关参考**

### **地域**

1. 登录[日志服务控制台](https://sls.console.aliyun.com/?spm=a2c4g.11186623.0.0.70905a3dccueNa)，在Project列表中，单击目标Project。

2. 单击Project名称右侧的![image](<Base64-Image-Removed>)进入项目概览页面。

3. 在基础信息中可查看当前Project的地域名称，地域名称对应RegionID请参考下表。


> 地域代表云服务资源的物理数据中心所在的地理位置 **，** RegionID 是云服务地域的唯一标识符。


**地域RegionID映射表**

|     |     |
| --- | --- |
| **地域名称** | **RegionID** |
| 华北1（青岛） | cn-qingdao |
| 华北2（北京） | cn-beijing |
| 华北3（张家口） | cn-zhangjiakou |
| 华北5（呼和浩特） | cn-huhehaote |
| 华北6（乌兰察布） | cn-wulanchabu |
| 华东1（杭州） | cn-hangzhou |
| 华东2（上海） | cn-shanghai |
| 华东5（南京-本地地域-关停中） | cn-nanjing |
| 华东6（福州-本地地域-关停中） | cn-fuzhou |
| 华南1（深圳） | cn-shenzhen |
| 华南2（河源） | cn-heyuan |
| 华南3（广州） | cn-guangzhou |
| 菲律宾（马尼拉） | ap-southeast-6 |
| 韩国（首尔） | ap-northeast-2 |
| 马来西亚（吉隆坡） | ap-southeast-3 |
| 日本（东京） | ap-northeast-1 |
| 泰国（曼谷） | ap-southeast-7 |
| 西南1（成都） | cn-chengdu |
| 新加坡 | ap-southeast-1 |
| 印度尼西亚（雅加达） | ap-southeast-5 |
| 中国香港 | cn-hongkong |
| 德国（法兰克福） | eu-central-1 |
| 美国（弗吉尼亚） | us-east-1 |
| 美国（硅谷） | us-west-1 |
| 英国（伦敦） | eu-west-1 |
| 阿联酋（迪拜） | me-east-1 |
| 沙特（利雅得） | me-central-1 |

### **LoongCollector网络传输类型**

服务入口（Endpoint）表示日志服务对外服务的访问域名，是访问一个项目（Project）及其内部日志数据的URL，与Project所在的地域相关。日志服务提供私网域名、公网域名与传输加速域名。可通过如下操作查看域名：

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)，在Project列表中，单击目标Project。

2. 单击Project名称右侧的![image](<Base64-Image-Removed>)进入项目概览页面。

3. 在访问域名中可查看当前Project的域名信息，不同的网络传输方式对应不同的域名。合适的网络传输方式有利于日志数据的传输更快速稳定。


| **网络类型** | **对应域名类型** | **描述** | **适用场景** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **网络类型** | **对应域名类型** | **描述** | **适用场景** |
| 阿里云内网 | 私网域名 | 阿里云内网为千兆共享网络，日志数据通过阿里云内网传输比公网传输更快速、稳定，内网包括VPC和经典网络。 | ECS实例和日志服务Project属于同一地域或 [自建服务器打通内网](https://help.aliyun.com/zh/ecs/user-guide/manage-servers-that-are-not-provided-by-alibaba-cloud#bdcc5a304b7sl "") 的情况。<br>**说明**<br>推荐在ECS所在地域创建日志服务Project，通过阿里云内网采集ECS中日志，不消耗公网带宽。 |
| 公网 | 公网域名 | 使用公网传输日志数据，不仅会受到网络带宽的限制，还可能会因网络抖动、延迟、丢包等影响数据采集的速度和稳定性。 | 以下两种情况，可以选择公网传输数据。 <br>- ECS实例和日志服务Project属于不同地域。<br>  <br>- 服务器为其他云厂商服务器或自建IDC。 |
| 传输加速 | 传输加速域名 | 利用阿里云CDN边缘节点进行日志采集加速，相对公网采集在网络延迟、稳定性上具有很大优势，但流量需额外计费。 | 如果业务服务器、日志服务Project分别属于国内地域和国外地域，使用公网传输数据可能会出现网络延迟高、传输不稳定等问题，您可以选择传输加速传输数据。更多信息，请参见 [传输加速](https://help.aliyun.com/zh/sls/select-a-network-type#2ba2d6a585eny "")。 |