### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[技术解决方案](https://help.aliyun.com/zh/sls/sls-technical-solutions/)[日志审计（旧版）](https://help.aliyun.com/zh/sls/log-audit-service/)使用前须知

# 使用前须知

更新时间：2025-09-04 04:53:43

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：日志审计（旧版）](https://help.aliyun.com/zh/sls/log-audit-service/)[下一篇：授予RAM用户操作日志审计服务的权限](https://help.aliyun.com/zh/sls/authorize-a-ram-user-to-manage-log-audit-service)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

使用限制

费用说明

本文介绍日志审计服务的使用限制、费用说明等信息。

## 使用限制

- 存储方式与地域限制



**重要**





使用日志审计服务进行日志区域化存储或中心化存储前，请合理评估存储地域是否满足相关法律法规和安全监管的要求。





  - 中心化存储



    从各个阿里云账号、各个地域采集到的日志，会存储到中心账号下的一个中心Project中，目前中心化存储可供选择的地域如下所示。





    **说明**





    当您切换中心账号所在地域时，日志服务为您创建一个新的中心Project，原Project不会被删除。







    - 中国：华北1（青岛）、华北2（北京）、华北3（张家口）、华北5（呼和浩特）、华北6（乌兰察布）、华东1（杭州）、华东2（上海）、华南1（深圳）、中国（香港）

    - 海外：新加坡、日本（东京）、德国（法兰克福）、印度尼西亚（雅加达）、马来西亚（吉隆坡）


  - 区域化存储

    针对SLB、ALB、OSS、PolarDB-X 1.0、VPC和DNS，日志审计服务支持将各个主账号采集到的日志存储到中心主账号下的各个与SLB、ALB、OSS、PolarDB-X 1.0和VPC实例处于相同地域的日志服务Project中（例如：杭州的OSS访问日志，存储到杭州的日志服务Project中）。

  - 同步到中心

    针对SLB、ALB、OSS、PolarDB-X 1.0、VPC和DNS的区域化存储，支持将各个地域的Logstore同步到一个中心化的Logstore中，以便做中心化查询、分析、告警、可视化、二次开发等。



    **说明**





    同步机制依赖日志服务数据加工，建议用户根据数据加工 [性能指南](https://help.aliyun.com/zh/sls/performance-guide "") 及时调整区域化Logstore的Shard资源等，避免影响加工同步速率。
- 资源限制

  - 中心主账号下对应的中心化Project只有一个，名为slsaudit-center-_中心化主账号ID_-_配置的地域_，例如：slsaudit-center-117938634953\*\*\*\*-cn-beijing。无法通过控制台删除中心化Project，只能通过命令行、API删除。

  - 针对SLB、ALB、OSS、PolarDB-X 1.0、VPC和DNS，可以有多个区域化Project，名为slsaudit-region-_中心化主账号ID_-_各个采集的地域_，例如：slsaudit-region-117938634953\*\*\*\*-cn-beijing。无法通过控制台删除区域化Project，只能通过命令行、API删除。

  - 配置云产品日志采集后，日志审计服务会创建专属Logstore，具备日志服务Logstore所有的功能，除以下操作限制。

    - 保护数据不被篡改，您无法自行写入数据，修改或删除索引。

    - 只能通过日志审计服务的配置页面或接口修改存储周期、删除Logstore。

    - 针对SLB、ALB、OSS、PolarDB-X 1.0、VPC和DNS，如果开启了 **同步到中心** 功能，在对应的区域化Project中，会生成数据加工任务。

      - 数据加工任务名为Internal Job: SLS Audit Service Data Sync for OSS Access、Internal Job: SLS Audit Service Data Sync for SLB、Internal Job: SLS Audit Service Data Sync for ALB、Internal Job: SLS Audit Service Data Sync for DRDS、Internal Job: SLS Audit Service Data Sync for VPC、Internal Job: SLS Audit Service Data Sync for DNS。

      - 您只能通过日志审计服务的配置页面或接口关闭该数据加工任务。

      - 开启了 **同步到中心** 功能的区域化Logstore会同步为专属的Logstore，您无法进行任何操作，如果需要进行查询等操作时，可以直接在中心化Logstore中操作。
- 权限限制



通过日志审计服务采集Kubernetes日志（Kubernetes审计日志、Kubernetes事件中心、Ingress访问日志）时，您需要了解如下权限限制。



  - 日志审计服务仅支持采集中心账号下的Kubernetes日志，不支持采集多账号配置中的其他阿里云账号下的Kubernetes日志。

  - 日志审计服务采集Kubernetes日志依赖数据加工功能。如果您通过日志审计服务采集Kubernetes日志，则中心账号需完成如下授权。




    | **说明项** | **中心账号未升级** | **中心账号已升级** |
    | --- | --- | --- |



    |     |     |     |
    | --- | --- | --- |
    | **说明项** | **中心账号未升级** | **中心账号已升级** |
    | 当前中心账号角色 | sls-audit-service-monitor | AliyunServiceRoleForSLSAudit |
    | 额外授权 | sls-audit-service-monitor角色需具备 [AliyunLogAuditServiceMonitorAccess](https://help.aliyun.com/zh/sls/use-a-custom-policy-to-authorize-log-service-to-collect-and-synchronize-logs#section-jp5-4z3-jns "") 权限和如下自定义权限（AliyunLogAuditServiceK8sAccess）。<br>```json<br>{<br>    "Version": "1",<br>    "Statement": [<br>        {<br>            "Action": "log:*",<br>            "Resource": [<br>                "acs:log:*:*:project/k8s-log-*"<br>            ],<br>            "Effect": "Allow"<br>        }<br>    ]<br>}<br>``` | 只需具备AliyunServiceRoleForSLSAudit角色权限，无需额外授权。 |


- 存储天数联动说明


  - 日志审计服务中的内网DNS日志（中心化）、公网DNS解析日志、全局流量管理日志、都存储在同一个Logstore（dns\_log）中，如果同时开启采集且设置的存储天数不同，则日志存储天数为开启者中心化存储天数的最大值。

  - 日志审计服务中的RDS审计日志、慢日志和错误日志都存储在同一个Logstore（rds\_log）中，如果同时开启采集且设置的存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。

  - 日志审计服务中的PolarDB MySQL审计日志、慢日志和错误日志都存储在同一个Logstore（polardb\_log）中，如果同时开启采集且设置的存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。

  - 日志审计服务中的云防火墙的互联网边界防火墙流量日志、VPC边界防火墙流量日志都存储在同一个Logstore（cloudfirewall\_log）中，如果同时开启采集且设置的存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。

  - 日志审计服务中的DDoS高防（新BGP）访问日志、DDoS高防（国际）访问日志、DDoS原生防护访问日志都存储在同一个Logstore（ddos\_log）中，如果同时开启采集且设置的存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。

  - 日志审计服务中的K8s审计日志、K8s事件中心都存储在同一个Logstore（k8s\_log）中，如果同时开启采集且存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。

  - 日志审计服务中的IDaaS应用身份服务管理操作日志、应用身份服务用户行为日志都存储在同一个Logstore（idaas\_log）中，如果同时开启采集且存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。

  - 日志审计服务中的配置审计变更日志、配置审计资源不合规日志都存储在同一个Logstore（cloudconfig\_log）中，如果同时开启采集且存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。

  - 日志审计服务中的PAM运维审计日志、PAM操作审计日志都存储在同一个Logstore（pam\_log）中，如果同时开启采集且存储天数不同，则日志存储天数为开通者的中心化存储天数的最大值。


**说明**

针对上述存储天数存在联动的日志类型，如果同时开启日志采集及智能分层存储功能，则热存储天数为开通者的热存储天数的最大值；如果开启了日志采集但没有同时开启智能分层存储功能，则默认关闭智能分层存储功能。

例如您开启了RDS审计日志和错误日志的采集，如果同时开启了两者的智能分层存储功能，则热存储天数为二者中的最大值；如果您只开启RDS审计日志的智能分层存储功能，没有开启RDS错误日志的智能分层存储功能，则默认关闭其所在Logstore（rds\_log）的智能分层存储功能。

- 配置审计

  - 日志审计服务依赖配置审计服务提供的配置类信息，您需在[配置审计](https://config.console.aliyun.com/overview)控制台开通配置审计服务，并开启全部资源的监控范围。

  - 如果您需要在日志审计服务中采集、存储或查询配置审计日志，您需同意授权日志服务提取您在配置审计中记录的日志。授权后，您的配置审计日志将被自动推送到日志服务中。

  - 如果您通过资源目录管理模式进行多账号采集，在中心账号授权后日志审计服务将会自动对资源目录配置的账号开通配置审计并集成日志服务；如果您通过自定义鉴权管理模式进行多账号采集，在中心账号授权后，其他成员账号还需进行额外的授权。具体操作，请参见 [自定义授权日志采集与同步](https://help.aliyun.com/zh/sls/use-a-custom-policy-to-authorize-log-service-to-collect-and-synchronize-logs#task-2485328 "")。
- 智能分层存储



日志审计服务的专属Logstore支持智能分层存储功能。相对热存储而言，低频存储成本更低，其数据的查询与分析性能有所降低，其余功能（例如告警、可视化、加工、投递等）不受影响。更多信息，请参见 [管理智能存储分层](https://help.aliyun.com/zh/sls/data-tiered-storage-overview "")。





**说明**





目前已支持智能分层存储的审计中心区域为华北1（青岛）、华北2（北京）、华北5（呼和浩特）、华东1（杭州）、华东2（上海）、华南1（深圳）、中国（香港）和新加坡。







您可以在日志审计服务的 **全局配置** 页面开启智能分层存储，其中热存储时间必须大于等于7天且不能超过当前存储天数。例如当前中心化存储时间为180天，开启30天热存储，则日志将在保存30天之后转为低频存储。



**说明**





日志审计（旧版）不支持在 **全局配置** 里开启归档存储，如需开启归档存储请提[工单](https://selfservice.console.aliyun.com/ticket/category/sls/today)进行加白。一旦加白完成，全局配置所设置的存储天数，仅在日志库首次创建时生效，实际天数以Logstore控制台页面为准。

- 数据加密

日志审计服务支持通过日志服务自带的服务密钥加密，而非通过用户自带密钥（BYOK）加密。日志服务自带密钥的加密方式支持AES算法（默认）和国密算法SM4。更多信息，请参见 [数据传输加密](https://help.aliyun.com/zh/sls/data-encryption#concept-2081473 "")。

开启日志加密后，日志服务将自动对当前已开启采集的云产品专属Logstore进行加密，包括中心化Project和区域化Project下的云产品专属Logstore。具体操作，请参见 [开启加密](https://help.aliyun.com/zh/sls/enable-log-collection-1#section-lqi-ho3-9d0 "")。

- 索引限制

日志审计服务支持自动更新索引或手动修改索引。具体操作，请参见 [创建索引](https://help.aliyun.com/zh/sls/create-indexes#section-4wq-ui2-jsk "")。

修改索引时，如果系统提示 **该日志库是SLS应用日志审计专属库，不支持修改索引属性、关闭索引**，请在日志审计服务的 **全局配置** 页面，单击 **修改**，然后单击 **确定**，重建日志审计服务配置。



**重要**





手动修改索引可能导致内置仪表盘、内置告警等不可用，请谨慎使用。


## 费用说明

- 日志服务



中心主账号需要开通日志服务与日志审计服务App，从其他主账号采集日志到中心主账号下。除特定云产品日志依赖外，其他主账号默认无需开通日志服务，也不会在其账号的日志服务下产生特定费用。目前日志审计服务免费，其涉及的数据存储、读写流量、数据加工等按量付费。更多信息，请参见 [按使用功能计费模式计费项](https://help.aliyun.com/zh/sls/billable-items#concept-xzl-hjg-vgb "")。





**重要**





  - SLB、ALB、OSS、PolarDB-X 1.0、VPC、DNS、容器服务Kubernetes版的日志，在开启同步到中心后，会使用数据加工功能进行同步，其涉及的加工与跨网流量费用等按量付费。更多信息，请参见 [按使用功能计费模式计费项](https://help.aliyun.com/zh/sls/billable-items#concept-xzl-hjg-vgb "")。

  - 您可以通过日志审计服务或普通采集方式采集云产品日志，两种方式各自计算费用。如果使用了两种方式进行采集，日志服务将保存两份数据，但两者的应用场景不同。

    - 日志审计服务：支持多账户下实时自动化、中心化采集云产品日志。所采集到的日志主要用于合规审计。

    - 普通方式：分地域采集，分散化管理。所采集到的日志主要用于日志分析。更多信息，请参见 [云产品日志概述](https://help.aliyun.com/zh/sls/alibaba-cloud-service-logs#concept-lyb-4sn-vgb "")。

支持免费额度，支持用已购买的资源包抵扣相应的费用。

- 云产品



开通日志审计服务与对应云产品的日志采集后，在云产品侧可能会产生额外的费用，如下所示。






| **云产品** | **额外费用** |
| --- | --- |



|     |     |
| --- | --- |
| **云产品** | **额外费用** |
| Web应用防火墙（WAF） | 在Web应用防火墙控制台上购买 **日志服务** 模块，费用详情请参见 [计费方式](https://help.aliyun.com/zh/waf/web-application-firewall-2-0/user-guide/billing-2#concept-rbc-jqf-qfb "")。 |
| 云安全中心（SAS） | 在云安全中心控制台开通 **日志分析** 功能，费用详情请参见 [计费概述](https://help.aliyun.com/zh/security-center/product-overview/billing-overview#concept-z2v-2bc-zdb "")。 |
| 云防火墙（Cloud Firewall） | 在云防火墙控制台上购买 **日志分析** 模块，费用详情请参见 [日志分析计费方式](https://help.aliyun.com/zh/cloud-firewall/user-guide/billing-of-log-analysis#concept-187712 "")。 |
| 云数据库RDS | 开启云数据库RDS审计日志采集功能后，会自动开启符合条件（支持MySQL的非基础版本，PostgreSQL高可用版）的RDS实例的SQL洞察（SQL审计）功能，费用详情请参见 [计费项](https://help.aliyun.com/zh/rds/product-overview/billable-items-billing-methods-and-pricing#concept-qxr-pd2-vdb "")。<br>**说明**<br>  - 如果您已为RDS实例开通SQL洞察试用版，则开启采集后，日志审计服务将自动关闭SQL洞察试用版，并开通SQL洞察正式版。<br>    <br>  - SQL洞察存储时长默认为30天。如果您要修改，需在RDS控制台上操作。具体操作，请参见 [修改SQL日志的存储时长](https://help.aliyun.com/zh/rds/use-sql-explorer-features-on-apsaradb-rds-for-mysql-instances#section-xou-s8d-59s "")。该存储时长与日志审计服务中的RDS审计日志的存储天数互相独立，互不影响。<br>    <br>    如果您在RDS控制台上设置的SQL洞察存储时长低于30天，则未满足日志投递条件，日志审计服务会自动将其重置为30天。<br>    <br>  - 如果您已停止采集RDS审计日志，且希望关闭SQL洞察功能，可在RDS控制台上进行手动关闭。具体操作，请参见 [关闭SQL洞察](https://help.aliyun.com/zh/rds/use-sql-explorer-features-on-apsaradb-rds-for-mysql-instances#section-e12-do8-eix "")。 |
| 云数据库PolarDB | 开启云数据库PolarDB的审计日志采集功能后，会自动开启MySQL集群的SQL洞察（SQL审计）功能，费用详情请参见 [计费项概览](https://help.aliyun.com/zh/polardb/polardb-for-mysql/enterprise-billing-item-overview#concept-zbj-4pg-tdb "")。<br>**说明**<br>  - 如果您已为PolarDB实例开通SQL洞察试用版，则开启采集后，日志审计服务将自动关闭SQL洞察试用版，并开通SQL洞察正式版。<br>    <br>  - SQL洞察存储时长默认为30天。如果您要修改，需在PolarDB控制台上操作。具体操作，请参见 [修改SQL日志的存储时长](https://help.aliyun.com/zh/polardb/polardb-for-mysql/user-guide/sql-explorer-and-audit#section-sgz-q13-mfb "")。该存储时长与日志审计服务中的PolarDB审计日志的存储天数互相独立，互不影响。<br>    <br>    如果您在PolarDB控制台上设置的SQL洞察存储时长低于30天，则未满足日志投递条件，日志审计服务会自动将其重置为30天。<br>    <br>  - 如果您已停止采集PolarDB审计日志，且希望关闭SQL洞察功能，可在PolarDB控制台上进行手动关闭。具体操作，请参见 [关闭SQL洞察和审计](https://help.aliyun.com/zh/polardb/polardb-for-mysql/user-guide/sql-explorer-and-audit#section-myx-gws-2gb "")。 |
| DDoS防护 | 在DDoS高防（新BGP）控制台上购买 **全量日志分析** 模块，费用详情请参见 [概述](https://help.aliyun.com/zh/anti-ddos/anti-ddos-pro-and-premium/user-guide/overview-of-the-log-analysis-feature#task-98586-zh "")。 |
| VPC | 流日志的计费项由流日志生成费和日志服务的服务费组成。更多信息，请参见 [流日志计费说明](https://help.aliyun.com/zh/vpc/user-guide/billing-of-flow-logs#concept-2234514 "")。<br>**说明**<br>  - 您可以通过日志审计服务或VPC控制台开启VPC流日志的采集，两种方式相互独立（开启和关闭都互不影响），各自计算流日志费用（流日志生成费+日志服务的服务费）。<br>    <br>  - 删除日志审计相关Project前，需先关闭VPC流日志的采集，否则对应VPC实例的流日志功能仍将处于开启状态。 |
| PAM | 已购买堡垒机（开发者版、轻量版）实例。更多信息，请参见 [购买实例](https://help.aliyun.com/zh/bh/pam/product-overview/purchase-a-bastion-host "")。 |
| DNS | 流量分析费用， 请参见 [DNS](https://help.aliyun.com/zh/sls/additional-fees-for-some-cloud-services#fba797d56akcb "")。 |