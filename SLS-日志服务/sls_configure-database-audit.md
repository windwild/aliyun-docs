### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 配置通用数据库审计

# 配置通用数据库审计

更新时间：2026-01-04 22:06:32

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是日志服务](https://help.aliyun.com/zh/sls/what-is-log-service)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

操作步骤

相关操作

您可以在数据库服务器或应用服务器上安装Logtail和抓包工具，采集数据库的所有活动记录，实现数据库审计。本文介绍配置通用数据库审计的操作步骤。

## 前提条件

- 已有可用的数据库。

- 已创建Project。具体操作，请参见 [管理Project](https://help.aliyun.com/zh/sls/manage-a-project/#section-ahq-ggx-ndb "")。


## 操作步骤

1. 登录[日志服务控制台](https://sls.console.aliyun.com/)。

2. 在 **日志应用** 区域的 **审计与安全** 页签中，单击 **通用数据库审计**。

3. 在 **接入配置管理** 页面中，单击 **添加**。

4. 在 **任务配置** 页面中，配置如下参数，然后单击 **下一步**。






| **参数** | **说明** |
| --- | --- |



|     |     |
| --- | --- |
| **参数** | **说明** |
| **任务ID** | 任务ID，支持自定义。默认情况下，通用数据库审计应用会自动分配一个ID。 |
| **任务名称** | 任务的名称。 |
| **任务描述** | 任务的描述。 |
| **项目Project** | 用于管理通用数据库审计应用相关资产的Project。 |
| **区域** | 目标Project所在地域。 |

5. 在 **审计场景查看** 页面中，单击 **下一步**。



此处仅介绍审计场景，无需配置。

6. 在 **安装Logtail** 页面中，完成如下操作。

1. 选择用于安装Logtail的服务器。



      请根据您的审计场景，选择服务器。



      - 如果是在ECS中安装Logtail，则在 **ECS机器** 页签中，选中目标ECS，单击 **创建**。具体操作，请参见 [安装Logtail（ECS实例）](https://help.aliyun.com/zh/sls/install-logtail-on-ecs-instances#task-2561331 "")。

      - 如果是在自建服务器或其他云厂商服务器中安装Logtail，则需要登录服务器并手动安装Logtail。具体操作，请参见 [安装Logtail（Linux系统）](https://help.aliyun.com/zh/sls/install-logtail-on-a-linux-server#concept-u5y-3lv-vdb "") 或 [安装Logtail（Windows系统）](https://help.aliyun.com/zh/sls/install-logtail-on-a-windows-server#concept-j22-xnv-vdb "")。


2. 安装完成后，单击 **确认安装完毕**。

3. 在 **选择机器** 区域，设置机器组信息，然后单击 **下一步**。



      日志服务支持创建IP地址机器组和用户自定义标识机器组，详细参数说明请参见 [创建IP地址机器组](https://help.aliyun.com/zh/sls/create-an-ip-address-based-machine-group#task-wc3-xn1-ry "") 和 [创建用户自定义标识机器组](https://help.aliyun.com/zh/sls/create-a-user-defined-identity-machine-group#concept-gyy-k3q-zdb "")。



      完成此操作后，日志服务会自动生成Logtail配置，并下发到Logtail所在的服务器上。
7. 根据 **安装抓包工具** 页面的提示信息安装和配置抓包工具。



抓包工具需支持Logtail的Lumberjack插件，推荐使用Packetbeat。本文以安装和配置Packetbeat为例，其他工具请参见 [采集Beats和Logstash数据源](https://help.aliyun.com/zh/sls/collect-data-from-beats-and-logstash#concept-tk3-gtz-c2b "")。




1. 在 **安装抓包工具** 页面中，设置 **请选择抓包工具** 为 **Packetbeat**。

2. 在 **安装抓包工具** 页面中，选择目标数据库。



      通用数据库审计应用会根据您所选择的数据库提供配置信息。后续配置packetbeat.yml文件时，需使用该信息。![配置Packetbeat](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7741065461/p407753.png)

3. 登录用于安装Packetbeat的服务器。

4. 下载并安装Packetbeat。



      具体操作，请参见 [Packetbeat](https://www.elastic.co/guide/en/beats/packetbeat/current/packetbeat-installation-configuration.html?spm=5176.2020520112.0.0.6ee734c07aSGu1#installation)。

5. 进入Packetbeat安装包所在路径，然后编辑packetbeat.yml文件。



      请根据您在 **安装抓包工具** 中获取的配置信息进行配置。



      1. 在 **General** 区域，添加如下内容。

         其中 **gjdd62** 为您所创建的任务ID。

         ![General配置](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7741065461/p407765.png)

      2. 在 **Transaction protocols** 区域的packetbeat.protocols节点下，添加如下内容。![packetbeat.protocols](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7741065461/p407776.png)

      3. 在 **Outputs** 区域的 **Logstash Output** 中，添加如下内容。



         **重要**





         默认情况下 **Elasticsearch Output** 为开启状态，您需要将其关闭，即手动注释output.elasticsearch中的配置。





         ![Logstash Output](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7741065461/p407823.png)


6. 启动Packetbeat。



      不同操作系统对应的启动方式不同，示例如下所示。更多信息，请参见 [start Packetbeat](https://www.elastic.co/guide/en/beats/packetbeat/current/packetbeat-installation-configuration.html?spm=5176.2020520112.0.0.6ee734c0y063gK#start)。

















      ```plaintext
      sudo chown root packetbeat.yml
      sudo ./packetbeat -e
      ```







      如果返回如下类似信息，表示启动成功。![启动Packetbeat](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7741065461/p407879.png)


完成上述操作后，日志服务开始采集数据库日志。

## 相关操作

您还可以在 **接入配置管理** 页签中，执行如下操作。

| **操作** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **操作** | **说明** |
| 查看审计日志 | 单击目标任务对应的 **查看审计日志**，系统将跳转至对应的LogStore中。您可以在LogStore中查看对应的原始日志，并执行查询分析操作。具体操作，请参见 [查询与分析快速指引](https://help.aliyun.com/zh/sls/quick-guide-to-query-and-analysis#task-tqc-ddm-gfb "")。 |
| 查看报表 | 单击目标任务对应的 **查看报表**，系统将跳转至对应的仪表盘页面，并展示各类审计指标。具体操作，请参见 [数据报表](https://help.aliyun.com/zh/sls/data-report-1#task-2187827 "")。 |
| 修改任务 | 单击目标任务对应的 **修改**，可修改任务的名称、描述、对应的Project、Logtail配置等信息。 |
| 删除任务 | 如果您不再使用此任务，可单击目标任务对应的 **删除**。<br>**重要**<br>删除任务后，不可恢复，请谨慎操作。 |