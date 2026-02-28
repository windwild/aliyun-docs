### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[开始使用](https://help.aliyun.com/zh/oss/start-using-faq/)[基础入门](https://help.aliyun.com/zh/oss/start-faq/)OSS入门问题

# OSS入门常见问题

更新时间：2026-02-05 06:36:26

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：常见问题概览](https://help.aliyun.com/zh/oss/faq-overview)[下一篇：OSS与文件系统的对比](https://help.aliyun.com/zh/oss/comparison-between-oss-and-traditional-file-systems)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

一般常见问题

阿里云地域

计费

数据安全与保护

数据复制

数据查询

存储管理

本文列举了对象存储OSS的用户经常咨询和关注的一些问题，帮助您快速了解OSS。

## 一般常见问题

- 什么是阿里云OSS？

阿里云对象存储服务OSS（Object Storage Service），是阿里云提供的海量、安全、低成本、高持久性的云存储服务，并可无限扩展。其数据设计持久性不低于99.9999999999%（12个9），服务可用性（或业务连续性）不低于99.995%。

- OSS能做什么？

OSS具有与平台无关的RESTful API接口，您可以在任何应用、任何时间、任何地点存储和访问任意类型的数据。由于OSS具有高度可扩展性，且您只需为实际用量付费，因此您可以从较小用量起步，并根据业务需要进行扩展，而不影响性能和持久性。

您可以使用阿里云提供的API、SDK包或者OSS迁移工具轻松地将海量数据移入或移出阿里云OSS。数据存储到阿里云OSS以后，您可以选择标准存储（Standard）作为移动应用、大型网站、图片分享或热点音视频的主要存储方式，也可以选择成本更低、存储期限更长的低频访问存储（Infrequent Access）、归档存储（Archive）、冷归档存储（Cold Archive）或者深度冷归档（Deep Cold Archive）作为不经常访问数据的存储方式。

关于OSS功能的更多信息，请参见 [OSS功能概览](https://help.aliyun.com/zh/oss/functions-and-features#concept-ilc-x31-tdb "")。

- OSS适合谁使用？

OSS适合社区、多媒体分享、电子商务等各类形式规模的网站站长，App应用和软件应用开发者，游戏开发企业以及有大规模数据存储需求的用户使用。

  - 互联网音视频、图片应用：如短视频存储、直播视频录制、视频点播、图片社交、图片或、视频相册等等，可利用OSS提供的丰富的RESTful API，实现海量的分布式数据存储方案。

  - 教育行业：K12、在线英语等在线教育，将数据存储到OSS，结合OSS传输加速或CDN加速产品，实现海量数据的存储以及内容分发方案。

  - AI/物联网：自动驾驶、物联网等场景。自动驾驶将采集的训练数据通过闪电立方采集与迁移到OSS。物联网家庭视频监控或社会类视频监控等场景，将摄像头采集的视频数据直接上传到OSS，不仅可以实时在APP上进行视频观看，同时可以根据生命周期将存储的数据进行冷热分层，以达成降本+合规的要求。

  - 影视渲染行业：影视制作、媒资管理的素材等数据存储，帮助客户提供高弹性、海量的数据存储空间；同时，结合IMM（智能媒体处理产品）可以实现存储+数据智能处理的解决方案。

  - 基因行业：基因测序、交付、诊断等基因上下游业务的数据存储需求，结合云上强大的计算能力，可以实现大数据的存储+计算+分析方案。
- OSS适合存储什么？

OSS适合存储论坛网站与软件应用中的附件、高清图片、音视频、备份文件等，以及各种App应用、多终端同步软件、网盘下载站的文件。

- 使用OSS，开发人员能够解决哪些使用本地解决方案无法解决的问题？

OSS让任何开发人员都可以充分利用阿里云的规模优势，而无需前期投资，也不会影响性能。开发人员可以解放出来专注于创新，而无需担心因业务增长带来的性能瓶颈以及安全性等问题。OSS不仅成本低，而且操作非常简单。

- OSS可以存储多少数据，有上限吗？

OSS总存储容量不限制，单个Bucket容量也不限制。通过OSS控制台仅可以上传小于5 GB的文件。对于大于5 GB的文件，需要使用 [分片上传](https://help.aliyun.com/zh/oss/user-guide/multipart-upload#concept-wzs-2gb-5db "") 功能，或者使用 [图形化管理工具ossbrowser 2.0（预览版）](https://help.aliyun.com/zh/oss/developer-reference/ossbrowser-2-0-overview/#5e106bb4ea9if "")、 [命令行工具ossutil 2.0](https://help.aliyun.com/zh/oss/developer-reference/ossutil-overview/#2a4b2fbc2f0a3 "") 直接上传。

- OSS提供哪些存储类型？

OSS提供标准、低频访问、归档、冷归档、深度冷归档多种存储类型，全面覆盖从热到冷的各种数据存储场景。更多信息，请参见 [存储类型](https://help.aliyun.com/zh/oss/user-guide/overview-53/#concept-fcn-3xt-tdb "")。

- 如何选择OSS存储类型？

OSS的五种存储类型，在计量大小、存储时长、解冻时间、数据取回等方面存在差异。您可以根据数据访问频率和应用场景来选择将数据存放在不同的存储类型中，从而达到降低存储成本的目的。

例如，您有70%的数据在30天以上都不会被访问到，那么这部分数据可以被称为较冷的数据。建议您将这部分较冷的数据存放在低频或者归档类型中，从而降低成本。同时您也可以为自己存储的数据设置生命周期管理的规则，OSS将自动根据客户设置的规则将较冷的数据自动转为低频或归档的存储类型。数据越冷，存储的成本可以做到越低。

需要注意的是，如果您需要读取存放在归档或冷归档的数据时，需要等待分钟级甚至小时级别的解冻时间，而无法实时读取。与此同时，OSS也将收取额外的解冻费用。

- 阿里云会使用我在OSS上存储的数据吗？

就用户业务数据，阿里云除执行您的服务要求或者法律法规要求外，不进行任何未获授权的使用及披露。更多信息，请参见 [服务条款](https://help.aliyun.com/zh/oss/user-guide/terms-of-service)。

- 阿里云是否会将自己的数据存储在OSS上？

是的。阿里云内部的开发人员也在很多项目中使用OSS作为授权数据存储。这些项目依赖OSS执行关键业务操作。

- 如果来自应用程序的流量突然激增，OSS如何保证业务的可用性？

OSS一开始就将处理来自任何互联网应用程序的高流量作为设计目标，提供按量计费的定价策略以及无限制的容量，确保您的服务不会因流量激增而中断。OSS能够均衡地分布负载，任何应用程序都不会受到流量峰值的影响。

- OSS的数据是如何组织的？

OSS是一个分布式的对象存储服务，提供的是一个Key-Value形式的对象存储服务。当您存储文件（Object）时，需要指定此Object的名称（Key），后续您将通过这个Key来获取该Object的内容。

Key也可以用来模拟文件夹的一些属性。OSS中文件夹的概念仅是一个逻辑概念，在通过API或SDK的方式设置文件夹的时候可以指定Object对应的Key值包括前面的目录即可模拟文件夹功能。例如，定义Object的Key为`dir/example.jpg`，就会在当前Bucket下创建一个名为`dir`的文件夹，并在该文件夹下创建一个名为`example.jpg`的文件。如果用户删除了`dir/example.jpg`，将不会再存在`dir`这个文件夹。

- OSS的智能特性如何？

OSS无缝集成了众多计算框架，涵盖了Hadoop、Spark、MaxCompute、BatchCompute、高性能计算（HPC）以及EMR等。此外，为了降低用户的操作复杂度，OSS提供了易于使用的SaaS服务，包括图片处理、内容检测等。此外，OSS还提供了智能媒体管理功能，能够快速集成各类智能媒体处理算法，从而极大地提升媒体内容的管理和分发效率。

- 如何开始使用OSS？

1. 在使用阿里云OSS服务之前，请确保您已经注册了阿里云账号并完成实名认证。具体操作，请参见 [注册阿里云账号](https://help.aliyun.com/zh/document_detail/324609.html#task-2012947 "") 和 [个人实名认证](https://help.aliyun.com/zh/document_detail/324614.html#task-2020003 "")、 [企业实名认证](https://help.aliyun.com/zh/account/overview "")。

2. 在注册阿里云账号后，请您单击此处[开通OSS服务](https://oss.console.aliyun.com/overview)。

3. **可选：**开通OSS服务后，默认的计费方式是按量计费。如果想进一步降低OSS费用，建议您购买OSS资源包。具体操作，请参见 [资源包购买指南](https://help.aliyun.com/zh/oss/purchase-resource-plans#task-2190990 "")。

4. 您可以通过控制台、图形化管理工具、命令行管理工具以及各种语言的SDK使用OSS。具体操作，请参见 [快速入门](https://help.aliyun.com/zh/oss/user-guide/get-started-with-oss/#concept-ptc-g24-tdb "")。
- OSS有哪些资质与认证？

阿里云几乎已经拿到了合规领域的“全满贯”。包括亚洲、欧洲等地的海外重要合规认证，以及中国的重要测评、安全审查，阿里云基本都是率先获得认可。其中，ISO 22301，CSA STAR Gold，德国C5附加条款都是全球首家，德国C5和ISO27001是亚太首家。MTCS Level3和ISO20000是中国首家。阿里云还是BSI在中国审核通过ISO27001的第一家云计算安全服务提供商（2012年）。当前阿里云对象存储服务OSS已经符合美国证券交易委员会（SEC）和金融业监管局（FINRA）合规要求。当前阿里云是继AWS、Azure、GCP、IBM之后又一个，同时也是中国第一个通过Cohasset Associates Ins审计认证的云厂商。详情请参见 [合规认证](https://help.aliyun.com/zh/oss/user-guide/compliance-certifications "")。

- 为什么要设计数据解冻？

在数据管理中，常常面临需要长期存储但不常访问的数据，即冷数据。OSS通过底层技术能力，使得冷数据可以以非常低的成本存储，同时在需要时可恢复到可访问状态，这就是数据解冻。通过牺牲实时访问的便利性，换取显著降低的存储成本，从而实现了成本的极致优化。


## 阿里云地域

- 我的数据存储在哪里？

您在创建OSS存储空间时，可以指定一个阿里云地域。OSS默认将您的数据存放在指定地域的某个可用区（AZ）。如果您开启了同城冗余存储，OSS会采用多可用区（AZ）内的数据冗余存储机制，将用户的数据冗余存储在同一地域（Region）的多个可用区。当某个可用区不可用时，仍然能够保障数据的正常访问。

- 什么是阿里云地域？

阿里云地域是一个地理位置，阿里云在其中提供多个在物理上独立且隔离的可用区，这些可用区通过延迟低、吞吐量高且冗余性高的网络连接在一起。

- 什么是可用区（AZ）？

可用区是指在同一地域内，电力和网络互相独立的物理区域。同一可用区内实例之间的网络延时更小。在同一地域内可用区与可用区之间内网互通，可用区之间能做到故障隔离。

- 如何确定将数据存储在哪个阿里云地域中？

选择地域时，建议您综合考虑地理位置、云产品之间的关系、资源价格等因素。更多信息，请参见 [如何选择OSS地域](https://help.aliyun.com/zh/oss/choose-an-oss-region#concept-2465513 "")。


## 计费

- OSS的费用是多少？

使用OSS，您可以按实际使用量付费（先使用，后付费），没有最低费用限制。您也可以预先购买资源包，之后使用资源时，扣除相应的额度。一般情况下，资源包更加优惠。详细的价格信息请参见[OSS产品定价](https://www.aliyun.com/price/product?spm=a2c4g.11186623.0.0.628c4d22ZdP2B0#/oss/detail/oss)。

- 如果其他账号访问我的OSS资源，应该如何付费？

当其他账号访问您的OSS资源，我们将按正常的OSS定价收费。您也可以选择将存储空间配置为请求者付费模式，在这种模式下，将由请求方支付OSS数据的相关请求和下载费用。具体操作，请参见 [请求者付费](https://help.aliyun.com/zh/oss/user-guide/enable-pay-by-requester-1#concept-yls-jm2-2fb "")。

- 如何关闭OSS？

考虑到一键关闭会导致客户的业务受到影响，OSS暂时没有提供此功能。您可以使用其他替代方案达到关闭OSS服务或者停止OSS计费的目的。更多信息，请参见 [如何关闭OSS服务或停止计费？](https://help.aliyun.com/zh/oss/product-overview/how-do-i-deactivate-oss-or-stop-oss-charging-my-resources#concept-4937 "")


## 数据安全与保护

- 数据存储在OSS上安全吗？

OSS本身是非常安全的。创建完成后，只有资源所有者才能访问其OSS资源。OSS提供用户身份验证，以控制对数据的访问。您可以使用各种访问控制策略，例如存储空间级别和文件级别的访问控制列表（ACL），选择性地向用户和用户组授予权限。OSS控制台会显示您可公开访问的存储空间。您可以将不希望公开访问的存储空间及文件设置为私有读写。如果您将私有读写的存储空间或文件的ACL设置为公共读或公共读写，则OSS会向您发出警告。关于OSS安全性的更多信息，请参见 [OSS安全与合规白皮书](https://help.aliyun.com/zh/oss/user-guide/security-and-compliance-overview#concept-1322552 "")。

- 如何控制存储在OSS中数据的访问权限？

针对存放在Bucket的Object的访问，OSS提供了多种权限控制方式，包括ACL、RAM Policy和Bucket Policy。更多信息，请参见 [权限与访问控制概述](https://help.aliyun.com/zh/oss/user-guide/permissions-and-access-control-overview#concept-e4s-mhv-tdb "")。

- OSS提供哪些数据加密的方式？

服务器端加密：上传文件时，OSS对收到的文件进行加密，再将得到的加密文件持久化保存；下载文件时，OSS自动将加密文件解密后返回给用户，并在返回的HTTP请求Header中，声明该文件进行了服务器端加密。更多信息，请参见 [服务端加密](https://help.aliyun.com/zh/oss/user-guide/server-side-encryption-8#concept-lqm-fkd-5db "")。

客户端加密：将文件上传到OSS之前在本地进行加密。更多信息，请参见 [客户端加密](https://help.aliyun.com/zh/oss/user-guide/client-side-encryption#concept-2323737 "")。

- 如何防止Bucket的数据被误删除或覆盖？

版本控制是针对存储空间（Bucket）级别的数据保护功能。开启版本控制后，针对数据的覆盖和删除操作将会以历史版本的形式保存下来。您在错误覆盖或者删除文件（Object）后，能够将Bucket中存储的Object恢复到任意时刻的历史版本。更多信息，请参见 [版本控制](https://help.aliyun.com/zh/oss/user-guide/overview-78/#concept-jdg-4rx-bgb "")。

- 什么是合规保留策略？

OSS支持WORM（Write Once Read Many）特性，允许您以不可删除、不可篡改的方式保存和使用数据。用户可针对Bucket设置基于时间的合规保留策略。当策略锁定后，用户可以在Bucket中上传和读取Object，但是在Object的保留时间到期之前，任何用户都无法删除Object和策略。Object的保留时间到期后，才可以删除Object。

当您需要长期存储且不允许修改或删除重要数据时，例如医疗档案、技术文件、合同文书等，可以将此类数据存放在指定的Bucket内，并通过开启合规保留策略保护您的重要数据。

- OSS是否支持在线修改文件？

OSS不支持对已上传的文件进行在线修改。如果您需要对文件进行修改，您可以先将已上传的文件下载到本地，修改后重新上传。

- OSS是三副本吗？

不是。OSS采用的是纠删码（erasure coding，EC），而不是三副本。纠删码在性能和可靠性方面并不会比三副本差。

- 可用性99.995%是怎么计算的？

OSS的可用性SLA的定义不同于实例型产品，其服务可用性将根据服务周期内每5分钟错误率之和除以服务周期内5分钟的总个数计算出每5分钟错误率的平均值，按照如下方式计算：


  - 每5分钟错误率=每5分钟失败请求数/每5分钟有效总请求数x100%

  - 服务可用性=（1-服务周期内∑每5分钟错误率/服务周期内5分钟总个数×100%


更多信息，请参见 [对象存储OSS服务等级协议](https://terms.aliyun.com/legal-agreement/terms/suit_bu1_ali_cloud/suit_bu1_ali_cloud201803021527_93160.html?spm=a2c4g.11186623.0.0.47a350f9jxxAM0)

## 数据复制

- 如何将某个Bucket数据复制到不同地域的Bucket？

当您希望在不同地域保存某个Bucket中数据的精确副本时，可对该Bucket配置多条跨区域复制规则。跨区域复制是跨不同OSS数据中心（地域）的Bucket自动、异步（近实时）复制Object，它会将Object的创建、更新和删除等操作从源存储空间复制到不同地域下的目标存储空间。

- 跨区域复制都有哪些应用场景？

  - 合规性要求：虽然OSS默认对每个存储的对象在物理盘上有多份副本，但合规性要求所规定的数据需要跨一定距离保存一份副本。通过跨区域复制，可以在远距离的OSS数据中心之间复制数据以满足这些合规性要求。

  - 最大限度减少延迟：客户处于两个地理位置。为了最大限度缩短访问对象时的延迟，可以在地理位置与用户较近的OSS数据中心中维护对象副本。

  - 数据备份与容灾：您对数据的安全性和可用性有极高的要求，对所有写入的数据，都希望在另一个数据中心显式地维护一份副本，以备发生特大灾难，如地震、海啸等导致一个OSS数据中心损毁时，还能启用另一个OSS数据中心的备份数据。

  - 数据复制：由于业务原因，需要将数据从OSS的一个数据中心迁移到另一个数据中心。

  - 操作原因：您在两个不同数据中心拥有分析同一组对象的计算集群，可以选择在两个不同区域中维护对象副本。
- 跨区域复制如何收费？

开启跨区域复制功能后，在备份源Bucket中的文件到目标Bucket时会产生跨区域间的数据流量，OSS会收取跨区域复制流量费用。每同步1个Object，OSS会累计计算请求次数并进行按量计费。目前跨区域复制流量仅支持按量计费，不提供资源包。


## 数据查询

如何查询数据？

OSS SelectObject支持您使用简单的SQL表达式轻松检索CSV或JSON格式对象中的具体数据，而无需检索整个对象。SelectObject简化了扫描对象内容并将其筛选成更小且具有针对性的数据集的流程，适用于大文件分片查询、JSON文件查询、日志文件分析等场景。更多信息，请参见 [查询文件](https://help.aliyun.com/zh/oss/user-guide/query-objects#concept-ghk-xz2-4gb "")。

## 存储管理

- 什么是OSS生命周期管理？如何利用生命周期管理来帮助降低OSS存储成本？



生命周期规则可以定期将非热门数据转换为低频访问、归档、冷归档或者深度冷归档存储，将不再需要访问的数据删除，让您更高效地管理您存储的数据，节省大量人力及存储成本。例如：



  - 某医疗机构的医疗档案，上传至OSS后半年内需要偶尔访问，半年后基本不再访问。可以通过设置生命周期规则，将已上传180天的医疗档案转为归档存储。

  - 某公司服务热线的录音文件，上传至OSS后2个月内，需要作为数据统计及核查的依据，2个月后偶尔访问，半年后基本不再访问，2年后数据不再需要存储。可以通过设置生命周期规则，设置录音文件上传60天后转为低频访问存储，180天后转为归档存储，730天后删除。

  - 某存储空间内有大量文件需要全部删除，但是手动删除每次仅可以删除最多1000个文件，比较麻烦。此时可以配置一条匹配整个Bucket的生命周期规则，设置一天后删除所有文件。此Bucket内的数据会在第二天被全部删除。


更多信息，请参见 [基于最后一次修改时间的生命周期规则](https://help.aliyun.com/zh/oss/user-guide/lifecycle-rules-based-on-the-last-modified-time#concept-y2g-szy-5db "")。

- 如何定期获取Bucket中Object的信息？

OSS清单功能支持您以天或周为单位，定期获取Bucket中指定Object的数量、大小、存储类型、加密状态等信息。更多信息，请参见 [存储空间清单](https://help.aliyun.com/zh/oss/user-guide/bucket-inventory#concept-2381539 "")。