### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[成本优化](https://help.aliyun.com/zh/oss/user-guide/expense-optimization/)[存储类型](https://help.aliyun.com/zh/oss/user-guide/overview-53/)转换存储类型

# 转换文件存储类型

更新时间：2025-12-22 01:26:40

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：存储类型](https://help.aliyun.com/zh/oss/user-guide/overview-53/)[下一篇：深度冷归档存储使用最佳实践](https://help.aliyun.com/zh/oss/user-guide/deep-cold-archive-storage-usage-best-practices)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

通过生命周期规则自动转换Object的存储类型

基于最后一次修改时间的存储类型转换

基于最后一次访问时间的存储类型转换

通过生命周期规则转换存储类型操作方式

通过CopyObject接口手动转换Object的存储类型

基于CopyObject转换存储类型规则

通过CopyObject转换存储类型操作方式

注意事项

最小计量空间

最低存储时长

解冻时间

请求费用

数据取回费用

临时存储费用

常见问题

基于最后一次修改时间的生命周期规则是否支持将Object从低频访问类型转换为标准类型？

OSS支持标准、低频访问、归档、冷归档、深度冷归档多种存储类型，您可以通过预先设定的生命周期规则，自动转换文件（对象）的存储类型。或者，您也可以通过CopyObject的方式，手动随时转换文件（Object）的存储类型。

**警告**

- 对开通了OSS-HDFS服务的Bucket，建议不要修改OSS-HDFS的数据存储目录`.dlsdata/`下任意Object的存储类型。

- 如果您将`.dlsdata/`下任意Object的存储类型修改为低频类型时，通过OSS-HDFS可正常访问数据。如果您将Object存储类型修改为归档、冷归档、深度冷归档后，通过OSS-HDFS无法访问数据。如需访问，您需要对数据进行解冻操作，解冻完成后再尝试访问数据。


## 通过生命周期规则自动转换Object的存储类型

### 基于最后一次修改时间的存储类型转换

- 本地冗余存储（LRS）![本地冗余](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8980723861/p179966.png)

本地冗余类型文件转换规则如下：


  - 标准存储（LRS）类型可转换为低频访问（LRS）、归档存储（LRS）、冷归档存储（LRS）或者深度冷归档存储（LRS）类型。

  - 低频访问（LRS）类型可转换为归档存储（LRS）、冷归档存储（LRS）类型或者深度冷归档存储（LRS）类型。

  - 归档存储（LRS）类型可转换为冷归档存储（LRS）类型或者深度冷归档存储（LRS）类型。

  - 冷归档存储（LRS）类型可转换为深度冷归档存储（LRS）类型。


当Bucket同时配置了转换为低频访问、归档存储、冷归档存储以及深度冷归档存储的策略时，其转换周期必须满足以下条件：

转换为低频访问的周期<转换为归档的周期<转换为冷归档的周期<转换为深度冷归档的周期

- 同城冗余存储（ZRS）![同城](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7548184861/p179968.png)

同城冗余类型文件转换规则如下：

  - 标准存储（ZRS）类型可转换为低频访问（ZRS）类型、归档存储（ZRS）类型、冷归档存储（LRS）类型和深度冷归档存储（LRS）类型。

  - 低频访问（ZRS）类型可转换为归档存储（ZRS）类型、冷归档存储（LRS）类型和深度冷归档存储（LRS）类型。

  - 归档存储（ZRS）类型可转换为冷归档存储（LRS）类型和深度冷归档存储（LRS）类型。

  - 冷归档存储（LRS）类型可转换为深度冷归档存储（LRS）类型。

更多信息，请参见 [基于最后一次修改时间的生命周期规则](https://help.aliyun.com/zh/oss/user-guide/lifecycle-rules-based-on-the-last-modified-time#concept-y2g-szy-5db "")。

### 基于最后一次访问时间的存储类型转换

**重要**

- 如果您需要将Object从标准存储或低频访问类型转换为归档、冷归档或深度冷归档存储类型，请[提交工单](https://selfservice.console.aliyun.com/ticket/createIndex)申请转换权限，申请通过后您需要指定转换的目标存储类型。

- 工单申请通过后，如果您基于最后一次访问时间策略将Object从标准存储或低频访问类型转为归档、冷归档或深度冷归档类型，则Bucket中归档、冷归档或深度冷归档类型Object的最后一次访问时间默认为该Bucket开启访问跟踪的时间。


- 本地冗余存储（LRS）

![1.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0296428171/p807570.jpg)

本地冗余类型文件转换规则如下：

  - 标准存储（LRS）类型可转换为低频访问（LRS）、归档存储（LRS）、冷归档存储（LRS）或者深度冷归档存储（LRS）类型。

  - 标准存储（LRS）类型转为低频访问（LRS）后，还可以选择当Object被访问后是否自动转回标准存储（LRS）类型。

  - 低频访问（LRS）类型可转换为归档存储（LRS）、冷归档存储（LRS）类型或者深度冷归档存储（LRS）类型。

  - 归档存储（LRS）类型可转换为冷归档存储（LRS）类型或者深度冷归档存储（LRS）类型。

  - 冷归档存储（LRS）类型可转换为深度冷归档存储（LRS）类型。
- 同城冗余存储（ZRS）

![2.jpg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0296428171/p807571.jpg)

同城冗余类型文件转换规则如下：

  - 标准存储（ZRS）类型可转换为低频访问（ZRS）类型、归档存储（ZRS）类型、冷归档存储（LRS）类型和深度冷归档存储（LRS）类型。

  - 标准存储（ZRS）类型转为低频访问（ZRS）后，还可以选择当Object被访问后是否自动转回标准存储（ZRS）类型。

  - 低频访问（ZRS）类型可转换为归档存储（ZRS）类型、冷归档存储（LRS）类型和深度冷归档存储（LRS）类型。

  - 归档存储（ZRS）类型可转换为冷归档存储（LRS）类型和深度冷归档存储（LRS）类型。

  - 冷归档存储（LRS）类型可转换为深度冷归档存储（LRS）类型。

更多信息，请参见 [基于最后一次访问时间的生命周期规则](https://help.aliyun.com/zh/oss/user-guide/lifecycle-rules-based-on-the-last-access-time#concept-2116588 "")。

### 通过生命周期规则转换存储类型操作方式

您可以通过多种方式设置生命周期规则。生命周期规则可用于将多个Object在指定时间内转储为指定存储类型，或者将过期的Object和碎片删除。以下是通过生命周期规则将Object转储为指定存储类型的步骤。

使用OSS管理控制台

1. 登录[OSS管理控制台](https://oss.console.aliyun.com/)。

2. 单击 **Bucket 列表**，然后单击目标Bucket名称。

3. 在左侧导航栏， 选择**数据管理** \> **生命周期**。

4. **可选：**如果您需要创建基于最后一次访问时间策略的生命周期规则，请在 **生命周期** 页面，打开 **启用访问跟踪** 开关。

5. 在 **生命周期** 页面，单击 **创建规则**。

6. 在 **创建生命周期规则** 面板，按如下说明配置生命周期规则。

   - 存储空间未开启版本控制


     |     |     |     |
     | --- | --- | --- |
     | **区域** | **配置项** | **说明** |
     | **基础设置** | **状态** | 设置生命周期规则的状态，可选择 **启动** 或 **禁用**。<br>     - 启动生命周期规则后，将按照配置的生命周期规则转换数据存储类型或删除数据。<br>       <br>     - 禁用生命周期规则后，将中断生命周期任务。 |
     | **策略** | 选择生命周期规则作用的Object。您可以选择 **按前缀匹配** 或 **配置到整个Bucket**。<br>**说明**<br>选择按前缀匹配时，需要填写前缀的完整路径。例如，您希望仅作用于src/dir1下的所有文件，则前缀需要填写为src/dir1，仅填写dir1则不生效。 |
     | **是否允许前缀重叠** | OSS默认会检查各个生命周期规则的前缀是否重叠。例如，您设置了以下两条包含重叠前缀的生命周期规则：<br>     - 规则1<br>       <br>       指定该Bucket内所有前缀为dir1/的Object在距离最后一次修改时间180天后删除。<br>       <br>     - 规则2<br>       <br>       指定该Bucket内所有前缀为dir1/dir2/的Object在距离最后一次修改时间30天后转低频访问类型，60天后删除。<br>       <br>在配置规则2时未选中该选项的情况下，因后台检测到dir1/dir2/目录下的Object同时匹配两条删除规则，因此会拒绝设置规则2，并报错Overlap for same action type Expiration.。<br>在配置规则2时选中该选项的情况下，dir1/dir2/下的Object会在30天后转低频访问类型，60天后删除。dir1/下的其他Object会在180天删除。<br>**说明**<br>如果配置了多条规则，且其中一条为基于整个Bucket的规则时，会被视为前缀重叠的情况。 |
     | **前缀** | 输入规则要匹配的Object名称的前缀。<br>     - 前缀设置为 `img`，表示匹配名称以img开头的所有Object，例如imgtest.png、img/example.jpg等。<br>       <br>     - 前缀设置为 `img/`，表示匹配名称以img/开头的所有Object，例如img/example.jpg、img/test.jpg等。 |
     | **标签** | 生命周期规则仅针对拥有指定标签Object生效。<br>     - 如果没有设置前缀，只设置了标签，且标签的key为a，value为1。则该规则将匹配Bucket内所有标签为a=1的Object。<br>       <br>     - 如果设置了前缀，前缀设置为img，同时设置了标签，标签的key为a，value为1，则该规则将匹配Bucket内所有名称以img开头，标签为a=1的Object。<br>       <br>更多信息，请参见 [对象标签](https://help.aliyun.com/zh/oss/user-guide/object-tagging-8#concept-zxf-jpy-pgb "")。 |
     | **NOT** | NOT选项用于设置生命周期规则对指定前缀和标签的Object不生效。<br>**重要**<br>     - 开启NOT选项时，前缀和标签必须至少存在一项，即同时设置前缀和标签或者只设置前缀或标签。<br>       <br>     - NOT语义定义标签中的key不支持与 **标签** 配置项中定义的key相同。<br>       <br>     - 开启NOT选项后，不支持设置碎片过期策略。 |
     | **文件大小** | 指定生命周期规则生效的文件大小。<br>     - **指定最小文件**：生命周期规则对大于该值的文件大小生效。取值大于0 B，小于5 TB。<br>       <br>     - **指定最大文件**：生命周期规则对小于该值的文件大小生效。取值大于0 B，小于等于5 TB。<br>       <br>**重要**<br>如果在同一条生命周期中，同时配置了指定最小文件和指定最大文件：<br>     - 确保指定最大文件的值大于指定最小文件的值。<br>       <br>     - 不支持配置碎片执行策略。<br>       <br>     - 不支持配置清除删除标记策略。 |
     | **文件执行策略设置** | **文件时间策略** | 选择Object过期策略，可选择 **指定天数**、 **指定日期** 和 **不启用**。选择 **不启用** 时，文件过期策略不生效。 |
     | **生命周期管理规则** | 配置转换Object存储类型或者删除过期Object的规则，可选择 **低频访问**、 **归档存储**、 **冷归档存储**、 **深度冷归档存储** 和 **数据删除**。<br>例如，当您将 **文件时间策略** 设置为 **指定日期**，并将日期设置为2023年9月24日，则最后一次修改时间在2023年9月24日之前的Object会被自动删除，且删除后不可恢复。 |
     | **碎片执行策略设置** | **碎片过期策略** | 配置碎片执行策略。如果选中了 **标签**，则无法配置该选项。您可以选择按 **指定天数** 或 **指定日期** 执行碎片过期策略，也可以选择 **不启用** 碎片过期策略。当选择 **不启用** 时，碎片过期策略不生效。<br>**重要**<br>生命周期规则至少包含文件过期策略或碎片过期策略。 |
     | **碎片规则** | 根据碎片过期策略选择的过期天数或过期日期设定碎片何时过期，碎片过期后会被自动删除，且删除后不可恢复。 |

   - 存储空间已开启版本控制

     开启版本控制后， **基础设置** 与 **碎片执行策略设置** 区域涉及的配置项，与未开启版本控制的配置方法相同。以下表格仅介绍与未开启版本控制相比，开启版本控制后配置项存在的差异。



     **重要**





     在配置生命周期规则前，请确认：如果Bucket已开启了版本控制并作为跨区域复制的目标端，从源端同步过来的删除标记（Delete Marker）会将本Bucket内的同名对象从当前版本转变为历史版本。因此，请谨慎配置针对历史版本的清理规则，避免当前Bucket中的数据被非预期删除。






     |     |     |     |
     | --- | --- | --- |
     | **区域** | **配置项** | **说明** |
     | **当前版本文件执行策略设置** | **清理对象删除标记** | 开启版本控制后，清除策略中增加了 **清理对象删除标记** 选项，其他选项与未开启版本控制时相同。<br>选择此选项后，如果当前Object仅有一个版本且为删除标记时，则OSS将删除过期Object的删除标记。如果当前Object有多个版本，且Object的最新版本为删除标记时，则OSS将保留该删除标记。关于删除标记的更多信息，请参见 [删除标记](https://help.aliyun.com/zh/oss/user-guide/delete-marker#concept-azw-shj-dgb "")。<br>**重要**<br>当有历史版本存在时，该规则不会清理对象删除标记。因此建议及时清理对象删除标记和非必要的历史版本，否则Bucket内因存储过多的删除标记，导致List性能下降。 |
     | **历史版本文件执行策略设置** | **文件时间策略** | 设置历史版本文件的过期策略，可选择 **指定天数** 和 **不启用**。当选择 **不启用** 时，文件过期策略不生效。 |
     | **生命周期管理规则** | 设定一个过期天数N，历史版本的Object会在其被转换为历史版本的N天后过期，并在过期的第二天执行指定操作。例如设置为30，则在2023年09月01日被转为历史版本的Object会在2023年10月01日被转换为指定存储类型或被删除。<br>**重要**<br>您可以通过Object下一个版本的最后一次修改时间确定 Object被转为历史版本的时间。 |
7. 单击 **确定**。

生命周期规则保存成功后，您可以在策略列表中查看已设置的生命周期规则。


使用阿里云SDK

以下仅列举常见SDK的配置生命周期规则的代码示例。关于其他SDK的配置生命周期规则的代码示例，请参见 [简介](https://help.aliyun.com/zh/oss/developer-reference/overview-21#concept-dcn-tp1-kfb "")。

Java

PHP

Node.js

Python

C#

Android-Java

Go

C++

C

Ruby

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.common.utils.DateUtil;
import com.aliyun.oss.model.LifecycleRule;
import com.aliyun.oss.model.SetBucketLifecycleRequest;
import com.aliyun.oss.model.StorageClass;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Demo {

    public static void main(String[] args) throws Exception {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写Bucket所在地域。以华东1（杭州）为例，Region填写为cn-hangzhou。
        String region = "cn-hangzhou";

        // 创建OSSClient实例。
        // 当OSSClient实例不再使用时，调用shutdown方法以释放资源。
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
        .endpoint(endpoint)
        .credentialsProvider(credentialsProvider)
        .clientConfiguration(clientBuilderConfiguration)
        .region(region)
        .build();

        try {
            // 创建SetBucketLifecycleRequest。
            SetBucketLifecycleRequest request = new SetBucketLifecycleRequest(bucketName);

            // 设置规则ID。
            String ruleId0 = "rule0";
            // 设置文件匹配前缀。
            String matchPrefix0 = "A0/";
            // 设置要匹配的标签。
            Map<String, String> matchTags0 = new HashMap<String, String>();
            // 依次填写要匹配标签的键（例如owner）和值（例如John）。
            matchTags0.put("owner", "John");

            String ruleId1 = "rule1";
            String matchPrefix1 = "A1/";
            Map<String, String> matchTags1 = new HashMap<String, String>();
            matchTags1.put("type", "document");

            String ruleId2 = "rule2";
            String matchPrefix2 = "A2/";

            String ruleId3 = "rule3";
            String matchPrefix3 = "A3/";

            String ruleId4 = "rule4";
            String matchPrefix4 = "A4/";

            String ruleId5 = "rule5";
            String matchPrefix5 = "A5/";

            String ruleId6 = "rule6";
            String matchPrefix6 = "A6/";

            // 距最后修改时间3天后过期。
            LifecycleRule rule = new LifecycleRule(ruleId0, matchPrefix0, LifecycleRule.RuleStatus.Enabled, 3);
            rule.setTags(matchTags0);
            request.AddLifecycleRule(rule);

            // 指定日期之前创建的文件过期。
            rule = new LifecycleRule(ruleId1, matchPrefix1, LifecycleRule.RuleStatus.Enabled);
            rule.setCreatedBeforeDate(DateUtil.parseIso8601Date("2022-10-12T00:00:00.000Z"));
            rule.setTags(matchTags1);
            request.AddLifecycleRule(rule);

            // 分片3天后过期。
            rule = new LifecycleRule(ruleId2, matchPrefix2, LifecycleRule.RuleStatus.Enabled);
            LifecycleRule.AbortMultipartUpload abortMultipartUpload = new LifecycleRule.AbortMultipartUpload();
            abortMultipartUpload.setExpirationDays(3);
            rule.setAbortMultipartUpload(abortMultipartUpload);
            request.AddLifecycleRule(rule);

            // 指定日期之前的分片过期。
            rule = new LifecycleRule(ruleId3, matchPrefix3, LifecycleRule.RuleStatus.Enabled);
            abortMultipartUpload = new LifecycleRule.AbortMultipartUpload();
            abortMultipartUpload.setCreatedBeforeDate(DateUtil.parseIso8601Date("2022-10-12T00:00:00.000Z"));
            rule.setAbortMultipartUpload(abortMultipartUpload);
            request.AddLifecycleRule(rule);

            // 距最后修改时间10天后转低频访问存储类型，距最后修改时间30天后转归档存储类型。
            rule = new LifecycleRule(ruleId4, matchPrefix4, LifecycleRule.RuleStatus.Enabled);
            List<LifecycleRule.StorageTransition> storageTransitions = new ArrayList<LifecycleRule.StorageTransition>();
            LifecycleRule.StorageTransition storageTransition = new LifecycleRule.StorageTransition();
            storageTransition.setStorageClass(StorageClass.IA);
            storageTransition.setExpirationDays(10);
            storageTransitions.add(storageTransition);
            storageTransition = new LifecycleRule.StorageTransition();
            storageTransition.setStorageClass(StorageClass.Archive);
            storageTransition.setExpirationDays(30);
            storageTransitions.add(storageTransition);
            rule.setStorageTransition(storageTransitions);
            request.AddLifecycleRule(rule);

            // 指定最后修改日期在2022年10月12日之前的文件转为归档存储。
            rule = new LifecycleRule(ruleId5, matchPrefix5, LifecycleRule.RuleStatus.Enabled);
            storageTransitions = new ArrayList<LifecycleRule.StorageTransition>();
            storageTransition = new LifecycleRule.StorageTransition();

            storageTransition.setCreatedBeforeDate(DateUtil.parseIso8601Date("2022-10-12T00:00:00.000Z"));

            storageTransition.setStorageClass(StorageClass.Archive);
            storageTransitions.add(storageTransition);
            rule.setStorageTransition(storageTransitions);
            request.AddLifecycleRule(rule);

            // rule6针对版本控制状态下的Bucket。
            rule = new LifecycleRule(ruleId6, matchPrefix6, LifecycleRule.RuleStatus.Enabled);
            // 设置Object相对最后修改时间365天之后自动转为归档文件。
            storageTransitions = new ArrayList<LifecycleRule.StorageTransition>();
            storageTransition = new LifecycleRule.StorageTransition();
            storageTransition.setStorageClass(StorageClass.Archive);
            storageTransition.setExpirationDays(365);
            storageTransitions.add(storageTransition);
            rule.setStorageTransition(storageTransitions);
            // 设置自动移除过期删除标记。
            rule.setExpiredDeleteMarker(true);
            // 设置非当前版本的object距最后修改时间10天之后转为低频访问类型。
            LifecycleRule.NoncurrentVersionStorageTransition noncurrentVersionStorageTransition =
                    new LifecycleRule.NoncurrentVersionStorageTransition().withNoncurrentDays(10).withStrorageClass(StorageClass.IA);
            // 设置非当前版本的Object距最后修改时间20天之后转为归档类型。
            LifecycleRule.NoncurrentVersionStorageTransition noncurrentVersionStorageTransition2 =
                    new LifecycleRule.NoncurrentVersionStorageTransition().withNoncurrentDays(20).withStrorageClass(StorageClass.Archive);
            // 设置非当前版本Object 30天后删除。
            LifecycleRule.NoncurrentVersionExpiration noncurrentVersionExpiration = new LifecycleRule.NoncurrentVersionExpiration().withNoncurrentDays(30);
            List<LifecycleRule.NoncurrentVersionStorageTransition> noncurrentVersionStorageTransitions = new ArrayList<LifecycleRule.NoncurrentVersionStorageTransition>();
            noncurrentVersionStorageTransitions.add(noncurrentVersionStorageTransition2);
            rule.setStorageTransition(storageTransitions);
            rule.setNoncurrentVersionExpiration(noncurrentVersionExpiration);
            rule.setNoncurrentVersionStorageTransitions(noncurrentVersionStorageTransitions);
            request.AddLifecycleRule(rule);

            // 发起设置生命周期规则请求。
            ossClient.setBucketLifecycle(request);

            // 查看生命周期规则。
            List<LifecycleRule> listRules = ossClient.getBucketLifecycle(bucketName);
            for(LifecycleRule rules : listRules){
                System.out.println("ruleId="+rules.getId()+", matchPrefix="+rules.getPrefix());
            }
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }
    }
}
```

```php
<?php
if (is_file(__DIR__ . '/../autoload.php')) {
    require_once __DIR__ . '/../autoload.php';
}
if (is_file(__DIR__ . '/../vendor/autoload.php')) {
    require_once __DIR__ . '/../vendor/autoload.php';
}

use OSS\Credentials\EnvironmentVariableCredentialsProvider;
use OSS\OssClient;
use OSS\CoreOssException;
use OSS\Model\LifecycleConfig;
use OSS\Model\LifecycleRule;
use OSS\Model\LifecycleAction;

// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
$provider = new EnvironmentVariableCredentialsProvider();
// Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
$endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
// 填写存储空间名称。
$bucket= "examplebucket";

// 设置规则ID和文件前缀。
$ruleId0 = "rule0";
$matchPrefix0 = "A0/";
$ruleId1 = "rule1";
$matchPrefix1 = "A1/";

$lifecycleConfig = new LifecycleConfig();
$actions = array();
// 距最后修改时间3天后过期。
$actions[] = new LifecycleAction(OssClient::OSS_LIFECYCLE_EXPIRATION, OssClient::OSS_LIFECYCLE_TIMING_DAYS, 3);
$lifecycleRule = new LifecycleRule($ruleId0, $matchPrefix0, "Enabled", $actions);
$lifecycleConfig->addRule($lifecycleRule);
$actions = array();
// 指定日期之前创建的文件过期。
$actions[] = new LifecycleAction(OssClient::OSS_LIFECYCLE_EXPIRATION, OssClient::OSS_LIFECYCLE_TIMING_DATE, '2022-10-12T00:00:00.000Z');
$lifecycleRule = new LifecycleRule($ruleId1, $matchPrefix1, "Enabled", $actions);
$lifecycleConfig->addRule($lifecycleRule);
try {
    $config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        "region"=> "cn-hangzhou"
    );
    $ossClient = new OssClient($config);

    $ossClient->putBucketLifecycle($bucket, $lifecycleConfig);
} catch (OssException $e) {
    printf(__FUNCTION__ . ": FAILED\n");
    printf($e->getMessage() . "\n");
    return;
}
print(__FUNCTION__ . ": OK" . "\n");
```

```nodejs
const OSS = require('ali-oss')

const client = new OSS({
  // yourregion填写Bucket所在地域。以华东1（杭州）为例，Region填写为oss-cn-hangzhou。
  region: 'yourregion',
  // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  accessKeyId: process.env.OSS_ACCESS_KEY_ID,
  accessKeySecret: process.env.OSS_ACCESS_KEY_SECRET,
  authorizationV4: true,
  // 填写存储空间名称。
  bucket: 'yourbucketname'
});

async function getBucketLifecycle () {
  try {
    const result = await client.getBucketLifecycle('Yourbucketname');
    console.log(result.rules); // 获取生命周期规则。

    result.rules.forEach(rule => {
      console.log(rule.id) //  查看生命周期规则ID。
      console.log(rule.status) // 查看生命周期规则状态。
      console.log(rule.tags) // 查看生命周期规则标签。
      console.log(rule.expiration.days) // 查看过期天数规则。
      console.log(rule.expiration.createdBeforeDate) // 查看过期日期规则。
      // 查看过期分片规则。
      console.log(rule.abortMultipartUpload.days || rule.abortMultipartUpload.createdBeforeDate)
      // 查看存储类型转换规则。
      console.log(rule.transition.days || rule.transition.createdBeforeDate) // 查看存储类型转换时间。
      console.log(rule.transition.storageClass) // 转换存储类型。
      // 查看是否自动删除过期删除标记。
      console.log(rule.transition.expiredObjectDeleteMarker)
      // 查看非当前版本Object存储类型转换规则。
      console.log(rule.noncurrentVersionTransition.noncurrentDays) // 查看非当前版本Object存储类型转换时间。
      console.log(rule.noncurrentVersionTransition.storageClass) // 查看非当前版本Object转换的存储类型。
    })
  } catch (e) {
    console.log(e);
  }
}
getBucketLifecycle();
```

```python
# -*- coding: utf-8 -*-
import oss2
from oss2.credentials import EnvironmentVariableCredentialsProvider
import datetime
from oss2.models import (LifecycleExpiration, LifecycleRule,
                        BucketLifecycle, AbortMultipartUpload,
                        TaggingRule, Tagging, StorageTransition,
                        NoncurrentVersionStorageTransition,
                        NoncurrentVersionExpiration)

# 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
auth = oss2.ProviderAuthV4(EnvironmentVariableCredentialsProvider())

# 填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
endpoint = "https://oss-cn-hangzhou.aliyuncs.com"
# 填写Endpoint对应的Region信息，例如cn-hangzhou。注意，v4签名下，必须填写该参数
region = "cn-hangzhou"

# examplebucket填写存储空间名称。
bucket = oss2.Bucket(auth, endpoint, "examplebucket", region=region)

# 设置Object距其最后修改时间3天后过期。
rule1 = LifecycleRule('rule1', 'tests/',
                      status=LifecycleRule.ENABLED,
                      expiration=LifecycleExpiration(days=3))

# 设置Object过期规则，指定日期之前创建的文件过期。
rule2 = LifecycleRule('rule2', 'tests2/',
                      status=LifecycleRule.ENABLED,
expiration = LifecycleExpiration(created_before_date=datetime.date(2023, 12, 12)))

# 设置分片过期规则，分片3天后过期。
rule3 = LifecycleRule('rule3', 'tests3/',
                      status=LifecycleRule.ENABLED,
            abort_multipart_upload=AbortMultipartUpload(days=3))

# 设置分片过期规则，指定日期之前的分片过期。
rule4 = LifecycleRule('rule4', 'tests4/',
                      status=LifecycleRule.ENABLED,
                      abort_multipart_upload = AbortMultipartUpload(created_before_date=datetime.date(2022, 12, 12)))

# 设置存储类型转换规则，指定Object在其最后修改时间20天之后转为低频访问类型，在其最后修改时间30天之后转为归档类型。
rule5 = LifecycleRule('rule5', 'tests5/',
                      status=LifecycleRule.ENABLED,
                      storage_transitions=[StorageTransition(days=20,storage_class=oss2.BUCKET_STORAGE_CLASS_IA),\
                            StorageTransition(days=30,storage_class=oss2.BUCKET_STORAGE_CLASS_ARCHIVE)])

# 设置匹配的标签。
tagging_rule = TaggingRule()
tagging_rule.add('key1', 'value1')
tagging_rule.add('key2', 'value2')
tagging = Tagging(tagging_rule)

# 设置存储类型转换规则，指定Object在其最后修改时间超过365天后转为ARCHIVE类型。
# rule6与以上几个规则不同的是它指定了匹配的标签，同时拥有key1=value1,key2=value2两个标签的object才会匹配此规则。
rule6 = LifecycleRule('rule6', 'tests6/',
                      status=LifecycleRule.ENABLED,
                      storage_transitions=[StorageTransition(created_before_date=datetime.date(2022, 12, 12),storage_class=oss2.BUCKET_STORAGE_CLASS_IA)],
                      tagging = tagging)

# rule7针对版本控制状态下的Bucket。
# 设置Object在其最后修改时间365天之后自动转为ARCHIVE类型。
# 设置自动移除过期删除标记。
# 设置非当前版本Object 12天后转为IA类型。
# 设置非当前版本Object 20天后转为ARCHIVE类型。
# 设置非当前版本Object 30天后删除。
rule7 = LifecycleRule('rule7', 'tests7/',
              status=LifecycleRule.ENABLED,
              storage_transitions=[StorageTransition(days=365, storage_class=oss2.BUCKET_STORAGE_CLASS_ARCHIVE)],
              expiration=LifecycleExpiration(expired_detete_marker=True),
              noncurrent_version_sotrage_transitions =
                    [NoncurrentVersionStorageTransition(12, oss2.BUCKET_STORAGE_CLASS_IA),\
                     NoncurrentVersionStorageTransition(20, oss2.BUCKET_STORAGE_CLASS_ARCHIVE)],
              noncurrent_version_expiration = NoncurrentVersionExpiration(30))

lifecycle = BucketLifecycle([rule1, rule2, rule3, rule4, rule5, rule6, rule7])

bucket.put_bucket_lifecycle(lifecycle)
```

```csharp
using Aliyun.OSS;
using Aliyun.OSS.Common;
// 填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
var endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
var accessKeyId = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_ID");
var accessKeySecret = Environment.GetEnvironmentVariable("OSS_ACCESS_KEY_SECRET");
// 填写Bucket名称，例如examplebucket。
var bucketName = "examplebucket";
// 填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。
const string region = "cn-hangzhou";

// 创建ClientConfiguration实例，按照您的需要修改默认参数。
var conf = new ClientConfiguration();

// 设置v4签名。
conf.SignatureVersion = SignatureVersion.V4;

// 创建OssClient实例。
var client = new OssClient(endpoint, accessKeyId, accessKeySecret, conf);
client.SetRegion(region);
try
{
    var setBucketLifecycleRequest = new SetBucketLifecycleRequest(bucketName);
    // 创建第1条生命周期规则。
    LifecycleRule lcr1 = new LifecycleRule()
    {
        ID = "delete obsoleted files",
        Prefix = "obsoleted/",
        Status = RuleStatus.Enabled,
        ExpriationDays = 3,
        Tags = new Tag[1]
    };
    // 设置标签。
    var tag1 = new Tag
    {
        Key = "project",
        Value = "projectone"
    };

    lcr1.Tags[0] = tag1;

    // 创建第2条生命周期规则。
    LifecycleRule lcr2 = new LifecycleRule()
    {
        ID = "delete temporary files",
        Prefix = "temporary/",
        Status = RuleStatus.Enabled,
        ExpriationDays = 20,
        Tags = new Tag[1]
    };
    // 设置标签。
    var tag2 = new Tag
    {
        Key = "user",
        Value = "jsmith"
    };
    lcr2.Tags[0] = tag2;

    // 设置碎片在距最后修改时间30天后过期。
    lcr2.AbortMultipartUpload = new LifecycleRule.LifeCycleExpiration()
    {
        Days = 30
    };

    LifecycleRule lcr3 = new LifecycleRule();
    lcr3.ID = "only NoncurrentVersionTransition";
    lcr3.Prefix = "test1";
    lcr3.Status = RuleStatus.Enabled;
    lcr3.NoncurrentVersionTransitions = new LifecycleRule.LifeCycleNoncurrentVersionTransition[2]
    {
        // 设置非当前版本的Object距最后修改时间90天之后转为低频访问类型。
        new LifecycleRule.LifeCycleNoncurrentVersionTransition(){
            StorageClass = StorageClass.IA,
            NoncurrentDays = 90
        },
        // 设置非当前版本的Object距最后修改时间180天之后转为归档类型。
        new LifecycleRule.LifeCycleNoncurrentVersionTransition(){
            StorageClass = StorageClass.Archive,
            NoncurrentDays = 180
        }
    };
    setBucketLifecycleRequest.AddLifecycleRule(lcr1);
    setBucketLifecycleRequest.AddLifecycleRule(lcr2);
    setBucketLifecycleRequest.AddLifecycleRule(lcr3);

    // 设置生命周期规则。
    client.SetBucketLifecycle(setBucketLifecycleRequest);
    Console.WriteLine("Set bucket:{0} Lifecycle succeeded ", bucketName);
}
catch (OssException ex)
{
    Console.WriteLine("Failed with error code: {0}; Error info: {1}. \nRequestID:{2}\tHostID:{3}",
        ex.ErrorCode, ex.Message, ex.RequestId, ex.HostId);
}
catch (Exception ex)
{
    Console.WriteLine("Failed with error info: {0}", ex.Message);
}
```

```androidjava
PutBucketLifecycleRequest request = new PutBucketLifecycleRequest();
request.setBucketName("examplebucket");

BucketLifecycleRule rule1 = new BucketLifecycleRule();
// 设置规则ID和文件前缀。
rule1.setIdentifier("1");
rule1.setPrefix("A");
// 设置是否执行生命周期规则。如果值为true，则OSS会定期执行该规则；如果值为false，则OSS会忽略该规则。
rule1.setStatus(true);
// 距最后修改时间200天后过期。
rule1.setDays("200");
// 30天后自动转为归档存储类型（Archive）
rule1.setArchiveDays("30");
// 未完成分片3天后过期。
rule1.setMultipartDays("3");
// 15天后自动转为低频存储类型（IA）。
rule1.setIADays("15");

BucketLifecycleRule rule2 = new BucketLifecycleRule();
rule2.setIdentifier("2");
rule2.setPrefix("B");
rule2.setStatus(true);
rule2.setDays("300");
rule2.setArchiveDays("30");
rule2.setMultipartDays("3");
rule2.setIADays("15");

ArrayList<BucketLifecycleRule> lifecycleRules = new ArrayList<BucketLifecycleRule>();
lifecycleRules.add(rule1);
lifecycleRules.add(rule2);
request.setLifecycleRules(lifecycleRules);
OSSAsyncTask task = oss.asyncPutBucketLifecycle(request, new OSSCompletedCallback<PutBucketLifecycleRequest, PutBucketLifecycleResult>() {
    @Override
    public void onSuccess(PutBucketLifecycleRequest request, PutBucketLifecycleResult result) {
        OSSLog.logInfo("code::"+result.getStatusCode());

    }

    @Override
    public void onFailure(PutBucketLifecycleRequest request, ClientException clientException, ServiceException serviceException) {
        OSSLog.logError("error: "+serviceException.getRawMessage());

    }
});

task.waitUntilFinished();
```

```go
package main

import (
	"fmt"
	"os"

	"github.com/aliyun/aliyun-oss-go-sdk/oss"
)

func main() {
	// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
	provider, err := oss.NewEnvironmentVariableCredentialsProvider()
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(-1)
	}
	// 创建OSSClient实例。
	// yourEndpoint填写Bucket对应的Endpoint，以华东1（杭州）为例，填写为https://oss-cn-hangzhou.aliyuncs.com。其它Region请按实际情况填写。
	// yourRegion填写Bucket所在地域，以华东1（杭州）为例，填写为cn-hangzhou。其它Region请按实际情况填写。
	clientOptions := []oss.ClientOption{oss.SetCredentialsProvider(&provider)}
	clientOptions = append(clientOptions, oss.Region("yourRegion"))
	// 设置签名版本
	clientOptions = append(clientOptions, oss.AuthVersion(oss.AuthV4))
	client, err := oss.New("yourEndpoint", "", "", clientOptions...)
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(-1)
	}
	// 填写存储空间名称。
	bucketName := "examplebucket"
	// 指定生命周期规则1，并在规则中指定前缀为foo的文件在距离最后一次修改时间3天后过期。
	rule1 := oss.BuildLifecycleRuleByDays("rule1", "foo/", true, 3)

	// 在受版本控制状态下的Object仅有删除标记的情况下，自动删除删除标记。
	deleteMark := true
	expiration := oss.LifecycleExpiration{
		ExpiredObjectDeleteMarker: &deleteMark,
	}

	// 非当前版本Object超过30天后过期删除。
	versionExpiration := oss.LifecycleVersionExpiration{
		NoncurrentDays: 30,
	}

	// 非当前版本Object超过10天后转为IA存储类型。
	versionTransition := oss.LifecycleVersionTransition{
		NoncurrentDays: 10,
		StorageClass:   "IA",
	}

	// 指定生命周期规则2。
	rule2 := oss.LifecycleRule{
		ID:                   "rule2",
		Prefix:               "yourObjectPrefix",
		Status:               "Enabled",
		Expiration:           &expiration,
		NonVersionExpiration: &versionExpiration,
		NonVersionTransitions: []oss.LifecycleVersionTransition{
			versionTransition,
		},
	}

	// 指定生命周期规则3，对标签键为tag1、标签值为value1的文件，距文件最后一次修改时间3天后过期。
	rule3 := oss.LifecycleRule{
		ID:     "rule3",
		Prefix: "",
		Status: "Enabled",
		Tags: []oss.Tag{
			oss.Tag{
				Key:   "tag1",
				Value: "value1",
			},
		},
		Expiration: &oss.LifecycleExpiration{Days: 3},
	}

	// 设置生命周期规则。
	rules := []oss.LifecycleRule{rule1, rule2, rule3}
	err = client.SetBucketLifecycle(bucketName, rules)
	if err != nil {
		fmt.Println("Error:", err)
		os.Exit(-1)
	}
}
```

```c
#include <alibabacloud/oss/OssClient.h>
using namespace AlibabaCloud::OSS;

int main(void)
{
    /*初始化OSS账号信息。*/

    /* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
    std::string Endpoint = "yourEndpoint";
    /* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
    std::string Region = "yourRegion";
    /*填写Bucket名称，例如examplebucket。*/
    std::string BucketName = "examplebucket";

    /*初始化网络等资源。*/
    InitializeSdk();

    ClientConfiguration conf;
    conf.signatureVersion = SignatureVersionType::V4;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);
    client.SetRegion(Region);

    SetBucketLifecycleRequest request(BucketName);
    std::string date("2022-10-12T00:00:00.000Z");

    /*设置标签。*/
    Tagging tagging;
    tagging.addTag(Tag("key1", "value1"));
    tagging.addTag(Tag("key2", "value2"));

    /*指定生命周期规则。*/
    auto rule1 = LifecycleRule();
    rule1.setID("rule1");
    rule1.setPrefix("test1/");
    rule1.setStatus(RuleStatus::Enabled);
    rule1.setExpiration(3);
    rule1.setTags(tagging.Tags());

    /*指定过期时间。*/
    auto rule2 = LifecycleRule();
    rule2.setID("rule2");
    rule2.setPrefix("test2/");
    rule2.setStatus(RuleStatus::Disabled);
    rule2.setExpiration(date);

    /*rule3为针对版本控制状态下的Bucket的生命周期规则。*/
    auto rule3 = LifecycleRule();
    rule3.setID("rule3");
    rule3.setPrefix("test3/");
    rule3.setStatus(RuleStatus::Disabled);

    /*设置Object距其最后修改时间365天之后自动转为归档类型。*/
    auto transition = LifeCycleTransition();
    transition.Expiration().setDays(365);
    transition.setStorageClass(StorageClass::Archive);
    rule3.addTransition(transition);

    /*设置自动移除过期删除标记。*/
    rule3.setExpiredObjectDeleteMarker(true);

    /*设置非当前版本的Object距最后修改时间10天之后转为低频访问类型。*/
    auto transition1 = LifeCycleTransition();
    transition1.Expiration().setDays(10);
    transition1.setStorageClass(StorageClass::IA);

    /*设置非当前版本的Object距最后修改时间20天之后转为归档类型。*/
    auto transition2 = LifeCycleTransition();
    transition2.Expiration().setDays(20);
    transition2.setStorageClass(StorageClass::Archive);

    /*设置Object在其成为非当前版本30天之后删除。*/
    auto expiration  = LifeCycleExpiration(30);
    rule3.setNoncurrentVersionExpiration(expiration);

    LifeCycleTransitionList noncurrentVersionStorageTransitions{transition1, transition2};
    rule3.setNoncurrentVersionTransitionList(noncurrentVersionStorageTransitions);

    /*设置生命周期规则。*/
    LifecycleRuleList list{rule1, rule2, rule3};
    request.setLifecycleRules(list);
    auto outcome = client.SetBucketLifecycle(request);

    if (!outcome.isSuccess()) {
        /*异常处理 */
        std::cout << "SetBucketLifecycle fail" <<
        ",code:" << outcome.error().Code() <<
        ",message:" << outcome.error().Message() <<
        ",requestId:" << outcome.error().RequestId() << std::endl;
        return -1;
    }

    /*释放网络等资源。*/
    ShutdownSdk();
    return 0;
}
```

```c
#include "oss_api.h"
#include "aos_http_io.h"
/* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
const char *endpoint = "yourEndpoint";
/* 填写Bucket名称，例如examplebucket。*/
const char *bucket_name = "examplebucket";
/* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
const char *region = "yourRegion";
void init_options(oss_request_options_t *options)
{
    options->config = oss_config_create(options->pool);
    /* 用char*类型的字符串初始化aos_string_t类型。*/
    aos_str_set(&options->config->endpoint, endpoint);
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    aos_str_set(&options->config->access_key_id, getenv("OSS_ACCESS_KEY_ID"));
    aos_str_set(&options->config->access_key_secret, getenv("OSS_ACCESS_KEY_SECRET"));
    //需要额外配置以下两个参数
    aos_str_set(&options->config->region, region);
    options->config->signature_version = 4;
    /* 是否使用cname域名访问OSS服务。0表示不使用。*/
    options->config->is_cname = 0;
    /* 用于设置网络相关参数，比如超时时间等。*/
    options->ctl = aos_http_controller_create(options->pool, 0);
}
int main(int argc, char *argv[])
{
    /* 在程序入口调用aos_http_io_initialize方法来初始化网络、内存等全局资源。*/
    if (aos_http_io_initialize(NULL, 0) != AOSE_OK) {
        exit(1);
    }
    /* 用于内存管理的内存池（pool），等价于apr_pool_t。其实现代码在apr库中。*/
    aos_pool_t *pool;
    /* 重新创建一个内存池，第二个参数是NULL，表示没有继承其它内存池。*/
    aos_pool_create(&pool, NULL);
    /* 创建并初始化options，该参数包括endpoint、access_key_id、acces_key_secret、is_cname、curl等全局配置信息。*/
    oss_request_options_t *oss_client_options;
    /* 在内存池中分配内存给options。*/
    oss_client_options = oss_request_options_create(pool);
    /* 初始化Client的选项oss_client_options。*/
    init_options(oss_client_options);
    /* 初始化参数。*/
    aos_string_t bucket;
    aos_table_t *resp_headers = NULL;
    aos_status_t *resp_status = NULL;
    aos_str_set(&bucket, bucket_name);
    aos_list_t lifecycle_rule_list;
    aos_str_set(&bucket, bucket_name);
    aos_list_init(&lifecycle_rule_list);
    /* 指定过期天数。*/
    oss_lifecycle_rule_content_t *rule_content_days = oss_create_lifecycle_rule_content(pool);
    aos_str_set(&rule_content_days->id, "rule-1");
    /* 设置文件前缀。*/
    aos_str_set(&rule_content_days->prefix, "dir1");
    aos_str_set(&rule_content_days->status, "Enabled");
    rule_content_days->days = 3;
    aos_list_add_tail(&rule_content_days->node, &lifecycle_rule_list);
    /* 指定过期时间。*/
    oss_lifecycle_rule_content_t *rule_content_date = oss_create_lifecycle_rule_content(pool);
    aos_str_set(&rule_content_date->id, "rule-2");
    aos_str_set(&rule_content_date->prefix, "dir2");
    aos_str_set(&rule_content_date->status, "Enabled");
    /* 过期时间格式为UTC。
    aos_str_set(&rule_content_date->date, "2023-10-11T00:00:00.000Z");
    aos_list_add_tail(&rule_content_date->node, &lifecycle_rule_list);
    /* 设置生命周期规则。*/
    resp_status = oss_put_bucket_lifecycle(oss_client_options, &bucket, &lifecycle_rule_list, &resp_headers);
    if (aos_status_is_ok(resp_status)) {
        printf("put bucket lifecycle succeeded\n");
    } else {
        printf("put bucket lifecycle failed, code:%d, error_code:%s, error_msg:%s, request_id:%s\n",
            resp_status->code, resp_status->error_code, resp_status->error_msg, resp_status->req_id);
    }
    /* 释放内存池，相当于释放了请求过程中各资源分配的内存。*/
    aos_pool_destroy(pool);
    /* 释放之前分配的全局资源。*/
    aos_http_io_deinitialize();
    return 0;
}
```

```ruby
require 'aliyun/oss'

client = Aliyun::OSS::Client.new(
  # Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
  endpoint: 'https://oss-cn-hangzhou.aliyuncs.com',
  # 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  access_key_id: ENV['OSS_ACCESS_KEY_ID'],
  access_key_secret: ENV['OSS_ACCESS_KEY_SECRET']
)
# 填写Bucket名称。
bucket = client.get_bucket('examplebucket')
# 设置生命周期规则。
bucket.lifecycle = [\
  Aliyun::OSS::LifeCycleRule.new(\
    :id => 'rule1', :enable => true, :prefix => 'foo/', :expiry => 3),\
  Aliyun::OSS::LifeCycleRule.new(\
    :id => 'rule2', :enable => false, :prefix => 'bar/', :expiry => Date.new(2016, 1, 1))\
]
```

使用命令行工具ossutil

关于使用ossutil设置生命周期规则的具体操作， 请参见 [put-bucket-lifecycle](https://help.aliyun.com/zh/oss/developer-reference/put-bucket-lifecycle#11295131d8csu "")。

使用REST API

如果您的程序自定义要求较高，您可以直接发起REST API请求。直接发起REST API请求需要手动编写代码计算签名。更多信息，请参见 [PutBucketLifecycle](https://help.aliyun.com/zh/oss/developer-reference/putbucketlifecycle#reference-xlw-dbv-tdb "")。

## 通过CopyObject接口手动转换Object的存储类型

您可以通过CopyObject接口，将Object覆写为指定的存储类型。

- 如果将Object修改为低频访问、归档存储、冷归档存储、深度冷归档存储类型，Object会涉及最小计量空间64 KB、最短存储周期、数据取回费用等。更多信息，请参见 [注意事项](https://help.aliyun.com/zh/oss/user-guide/convert-storage-classes#section-ku2-807-o44 "")。

- 归档存储、冷归档存储、深度冷归档存储类型的Object需要解冻后才可以修改存储类型。关于解冻Object的具体操作，请参见 [解冻Object](https://help.aliyun.com/zh/oss/user-guide/restore-objects-for-access#concept-wx5-szt-tdb "")。如果您已开启归档直读，则归档存储数据无需解冻就可以修改存储类型。直接读取会产生归档直读数据取回容量费用，请参见 [归档直读](https://help.aliyun.com/zh/oss/user-guide/archive-direct-reading#main-2356182 "")。


**说明**

- 在已开启版本控制的Bucket中，通过CopyObject转换Object的存储类型时，OSS将会为新拷贝的Object自动生成唯一的版本ID，此版本ID将会在响应Header中的`x-oss-version-id`返回。

- 在未开启或者暂停版本控制的Bucket中，通过CopyObject转换Object的存储类型时，OSS将会为新拷贝的Object自动生成version ID为null的版本，且会覆盖原有versionId为null的版本。如果被覆盖的文件类型为低频、归档、冷归档或者深度冷归档，可能会涉及存储不足规定时长容量费用。更多信息，请参见 [Object在存储不足规定时长时如何计费？](https://help.aliyun.com/zh/oss/billing-method-for-objects-whose-storage-duration-is-less-than-the-minimum-storage-duration "")。


### 基于CopyObject转换存储类型规则

- 本地冗余（LRS）

标准存储（LRS）、低频访问（LRS）、归档存储（LRS）、冷归档存储（LRS）和深度冷归档存储（LRS）各存储类型之间可任意转换。

- 同城冗余（ZRS）

标准存储（ZRS）、低频访问（ZRS）和归档存储（ZRS）各存储类型之间可任意转换。

将归档存储（ZRS）类型的Object转换为标准存储（ZRS）或低频访问（ZRS）类型时，需根据Object所在Bucket的设置情况采取不同操作：

  - 如果Bucket已开启 [归档直读](https://help.aliyun.com/zh/oss/user-guide/archive-direct-reading "") 功能，可以直接转换归档Object的存储类型，无需解冻。

  - 如果Bucket未开启归档直读功能，需要先 [解冻](https://help.aliyun.com/zh/oss/user-guide/restore-objects-for-access "") 归档存储Object，才能转换存储类型。

### 通过CopyObject转换存储类型操作方式

启用 [禁止文件覆盖写](https://help.aliyun.com/zh/oss/user-guide/prevent-file-overwrite "") 后，将无法通过 OSS 控制台、SDK、ossutil 等客户端方式调用 CopyObject 接口转换文件的存储类型。如需转换存储类型，请使用生命周期自动转换。

使用OSS管理控制台

通过控制台修改Object存储类型时，Object大小不能超过1 GB。超过1 GB的Object，建议通过SDK或者命令行工具ossutil。

1. 登录[OSS管理控制台](https://oss.console.aliyun.com/)。

2. 单击 **Bucket 列表**，然后单击目标Bucket名称。

3. 在左侧导航栏，选择**文件管理** \> **文件列表**。

4. 在 **文件列表** 页面，选择目标Object右侧的**![more ](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0119586661/p508856.jpg)** \> **修改存储类型**。

5. 建议您打开 **保留用户自定义元数据** 开关，修改存储类型后，Object的自定义元数据信息会被保留。

6. 选择您希望修改的存储类型后，单击 **确定**。


使用阿里云SDK

Java

PHP

Node.js

Python

Go

Object C

C++

Java

```java
import com.aliyun.oss.*;
import com.aliyun.oss.common.auth.*;
import com.aliyun.oss.common.comm.SignVersion;
import com.aliyun.oss.model.CopyObjectRequest;
import com.aliyun.oss.model.CopyObjectResult;
import com.aliyun.oss.model.ObjectMetadata;
import com.aliyun.oss.model.StorageClass;

public class Demo {
    public static void main(String[] args) throws Exception {
        // Endpoint以华东1（杭州）为例，其它Region请按实际情况填写。
        String endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
        // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
        EnvironmentVariableCredentialsProvider credentialsProvider = CredentialsProviderFactory.newEnvironmentVariableCredentialsProvider();
        // 本示例中的Bucket与Object需提前创建好, 且Object类型为标准或低频访问存储类型。
        // 填写Bucket名称，例如examplebucket。
        String bucketName = "examplebucket";
        // 填写不包含Bucket名称在内的Object完整路径，例如exampleobject.txt。
        String objectName = "exampleobject.txt";
        // 填写Bucket所在地域。以华东1（杭州）为例，Region填写为cn-hangzhou。
        String region = "cn-hangzhou";

        // 创建OSSClient实例。
        // 当OSSClient实例不再使用时，调用shutdown方法以释放资源。
        ClientBuilderConfiguration clientBuilderConfiguration = new ClientBuilderConfiguration();
        clientBuilderConfiguration.setSignatureVersion(SignVersion.V4);
        OSS ossClient = OSSClientBuilder.create()
        .endpoint(endpoint)
        .credentialsProvider(credentialsProvider)
        .clientConfiguration(clientBuilderConfiguration)
        .region(region)
        .build();

        try {
            // 创建CopyObjectRequest对象。
            CopyObjectRequest request = new CopyObjectRequest(bucketName, objectName, bucketName, objectName) ;

            // 创建ObjectMetadata对象。
            ObjectMetadata objectMetadata = new ObjectMetadata();

            // 将Object存储类型转换为归档类型。
            objectMetadata.setHeader("x-oss-storage-class", StorageClass.Archive);
            // 将Object存储类型转换为冷归档类型。
            // objectMetadata.setHeader("x-oss-storage-class", StorageClass.ColdArchive);
            // 将Object存储类型转换为深度冷归档类型。
            // objectMetadata.setHeader("x-oss-storage-class", StorageClass.DeepColdArchive);
            request.setNewObjectMetadata(objectMetadata);

            // 更改文件存储类型。
            CopyObjectResult result = ossClient.copyObject(request);
        } catch (OSSException oe) {
            System.out.println("Caught an OSSException, which means your request made it to OSS, "
                    + "but was rejected with an error response for some reason.");
            System.out.println("Error Message:" + oe.getErrorMessage());
            System.out.println("Error Code:" + oe.getErrorCode());
            System.out.println("Request ID:" + oe.getRequestId());
            System.out.println("Host ID:" + oe.getHostId());
        } catch (ClientException ce) {
            System.out.println("Caught an ClientException, which means the client encountered "
                    + "a serious internal problem while trying to communicate with OSS, "
                    + "such as not being able to access the network.");
            System.out.println("Error Message:" + ce.getMessage());
        } finally {
            if (ossClient != null) {
                ossClient.shutdown();
            }
        }
    }
}
```

PHP

```php
<?php
if (is_file(__DIR__ . '/../autoload.php')) {
    require_once __DIR__ . '/../autoload.php';
}
if (is_file(__DIR__ . '/../vendor/autoload.php')) {
    require_once __DIR__ . '/../vendor/autoload.php';
}

use OSS\Credentials\EnvironmentVariableCredentialsProvider;
use OSS\OssClient;
use OSS\CoreOssException;

// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
$provider = new EnvironmentVariableCredentialsProvider();
// Endpoint以杭州为例，其它Region请按实际情况填写。
$endpoint = "https://oss-cn-hangzhou.aliyuncs.com";
// 填写Bucket名称。
$bucket= "<yourBucketName>";
// 填写不包含Bucket名称在内的Object的完整路径，例如destfolder/exampleobject.txt。
$object = "<yourObjectName>";

$config = array(
        "provider" => $provider,
        "endpoint" => $endpoint,
        "signatureVersion" => OssClient::OSS_SIGNATURE_VERSION_V4,
        "region"=> "cn-hangzhou"
    );
    $ossClient = new OssClient($config);

try {

    // 指定转换后的文件存储类型，例如指定为归档存储类型（Archive）。
    $copyOptions = array(
        OssClient::OSS_HEADERS => array(
            'x-oss-storage-class' => 'Archive',
            'x-oss-metadata-directive' => 'REPLACE',
        ),
    );

    $ossClient->copyObject($bucket, $object, $bucket, $object, $copyOptions);

} catch (OssException $e) {
    printf(__FUNCTION__ . ": FAILED\n");
    printf($e->getMessage() . "\n");
    return;
}

print(__FUNCTION__ . ": OK" . "\n");
```

Node.js

```nodejs
const OSS = require('ali-oss');

const client = new OSS({
  // yourregion填写Bucket所在地域。以华东1（杭州）为例，Region填写为oss-cn-hangzhou。
  region: 'yourregion',
  // 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
  accessKeyId: process.env.OSS_ACCESS_KEY_ID,
  accessKeySecret: process.env.OSS_ACCESS_KEY_SECRET,
  authorizationV4: true,
  // yourbucketname填写存储空间名称。
  bucket: 'yourbucketname'
})
const options = {
    headers:{'x-oss-storage-class':'Archive'}
}
client.copy('Objectname','Objectname',options).then((res) => {
    console.log(res);
}).catch(err => {
    console.log(err)
})
```

Python

```python
# -*- coding: utf-8 -*-
import oss2
from oss2.credentials import EnvironmentVariableCredentialsProvider
import os
# 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
auth = oss2.ProviderAuthV4(EnvironmentVariableCredentialsProvider())

# 填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。
endpoint = "https://oss-cn-hangzhou.aliyuncs.com"

# 填写Endpoint对应的Region信息，例如cn-hangzhou。注意，v4签名下，必须填写该参数
region = "cn-hangzhou"

# yourBucketName填写存储空间名称。
bucket = oss2.Bucket(auth, endpoint, "yourBucketName", region=region)

# 填写Object的完整路径，完整路径中不能包含Bucket名称，例如exampledir/exampleobject.txt。
# 需确保该Object的存储类型为标准存储或低频访问类型。
object_name = 'exampledir/exampleobject.txt'

# 通过添加存储类型Header，将Object存储类型转换为归档类型。
headers = {'x-oss-storage-class': oss2.BUCKET_STORAGE_CLASS_ARCHIVE}
# 通过添加存储类型Header，将Object存储类型转换为冷归档类型。
# headers = {'x-oss-storage-class': oss2.BUCKET_STORAGE_CLASS_COLD_ARCHIVE}
# 通过添加存储类型Header，将Object存储类型转换为深度冷归档类型。
# headers = {'x-oss-storage-class': oss2.models.BUCKET_STORAGE_CLASS_DEEP_COLD_ARCHIVE}
# 更改文件存储类型。
bucket.copy_object(bucket.bucket_name, object_name, object_name, headers)
```

Go

```go
package main

import (
	"log"

	"github.com/aliyun/aliyun-oss-go-sdk/oss"
)

func main() {
	// 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。
	provider, err := oss.NewEnvironmentVariableCredentialsProvider()
	if err != nil {
		log.Fatalf("Failed to create credentials provider: %v", err)
	}

	// 创建OSSClient实例。
	// yourEndpoint填写Bucket对应的Endpoint，以华东1（杭州）为例，填写为https://oss-cn-hangzhou.aliyuncs.com。其它Region请按实际情况填写。
	// yourRegion填写Bucket所在地域，以华东1（杭州）为例，填写为cn-hangzhou。其它Region请按实际情况填写。
	clientOptions := []oss.ClientOption{oss.SetCredentialsProvider(&provider)}
	clientOptions = append(clientOptions, oss.Region("yourRegion"))
	// 设置签名版本
	clientOptions = append(clientOptions, oss.AuthVersion(oss.AuthV4))
	client, err := oss.New("yourEndpoint", "", "", clientOptions...)
	if err != nil {
		log.Fatalf("Failed to create OSS client: %v", err)
	}

	// yourBucketName填写存储空间名称。
	bucketName := "yourBucketName" // 请替换为实际的Bucket名称
	// yourObjectName填写不包含Bucket名称在内的Object的完整路径。
	objectName := "yourObjectName" // 请替换为实际的对象路径

	bucket, err := client.Bucket(bucketName)
	if err != nil {
		log.Fatalf("Failed to get bucket: %v", err)
	}

	// 更改文件存储类型，例如修改为归档存储类型。
	_, err = bucket.CopyObject(objectName, objectName, oss.ObjectStorageClass(oss.StorageArchive))
	if err != nil {
		log.Fatalf("Failed to change storage class of object: %v", err)
	}

	log.Println("Storage class changed successfully.")
}
```

Object C

```objectc
OSSCopyObjectRequest * copy = [OSSCopyObjectRequest new];
copy.sourceBucketName = @"examplebucket";
copy.sourceObjectKey = @"exampleobject.txt";
copy.bucketName = @"examplebucket";
copy.objectKey = @"exampleobject.txt";
// 将exampleobject.txt的存储类型指定为归档类型Archive。
copy.objectMeta = @{@"x-oss-storage-class" : @"Archive"};

OSSTask * task = [client copyObject:copy];
[task continueWithBlock:^id(OSSTask *task) {\
    if (!task.error) {\
        NSLog(@"copy object success!");\
    } else {\
        NSLog(@"copy object failed, error: %@" , task.error);\
    }\
    return nil;\
}];
// 实现同步阻塞等待任务完成。
// [task waitUntilFinished];
```

C++

```cpp
#include <iostream>
#include <alibabacloud/oss/OssClient.h>

using namespace AlibabaCloud::OSS;

int main(void)
{

    /* yourEndpoint填写Bucket所在地域对应的Endpoint。以华东1（杭州）为例，Endpoint填写为https://oss-cn-hangzhou.aliyuncs.com。*/
    std::string Endpoint = "yourEndpoint";
    /* yourRegion填写Bucket所在地域对应的Region。以华东1（杭州）为例，Region填写为cn-hangzhou。*/
    std::string Region = "yourRegion";
    /* 填写Bucket名称，例如examplebucket。*/
    std::string BucketName = "examplebucket";
    /* 填写Object完整路径，完整路径中不能包含Bucket名称，例如exampledir/exampleobject.txt。*/
    std::string ObjectName = "exampledir/exampleobject.txt";

    /* 初始化网络等资源。*/
    InitializeSdk();
    ClientConfiguration conf;
    conf.signatureVersion = SignatureVersionType::V4;
    /* 从环境变量中获取访问凭证。运行本代码示例之前，请确保已设置环境变量OSS_ACCESS_KEY_ID和OSS_ACCESS_KEY_SECRET。*/
    auto credentialsProvider = std::make_shared<EnvironmentVariableCredentialsProvider>();
    OssClient client(Endpoint, credentialsProvider, conf);
    client.SetRegion(Region);

    /* 设置修改后的文件存储类型，例如将修改后的文件存储类型设置为归档类型。*/
    ObjectMetaData objectMeta;
    objectMeta.addHeader("x-oss-storage-class", "Archive");

    std::string SourceBucketName = BucketName;
    std::string SourceObjectName = ObjectName;

    CopyObjectRequest request(SourceBucketName, ObjectName, objectMeta);
    request.setCopySource(SourceBucketName, SourceObjectName);

    /* 修改为上述指定的文件存储类型。*/
    auto outcome = client.CopyObject(request);
    if (!outcome.isSuccess()) {
        /* 异常处理。*/
        std::cout << "CopyObject fail" <<
        ",code:" << outcome.error().Code() <<
        ",message:" << outcome.error().Message() <<
        ",requestId:" << outcome.error().RequestId() << std::endl;
        return -1;
    }

    /* 释放网络等资源。*/
    ShutdownSdk();
    return 0;
}
```

使用命令行工具ossutil

关于使用ossutil转换Object存储类型的具体步骤， 请参见 [copy-object](https://help.aliyun.com/zh/oss/developer-reference/copy-objects-by-calling-an-api-operation#58f1d6bbb6x22 "")。

使用REST API

如果您的程序自定义要求较高，您可以直接发起REST API请求。直接发起REST API请求需要手动编写代码计算签名。更多信息，请参见 [CopyObject](https://help.aliyun.com/zh/oss/developer-reference/copyobject#reference-mvx-xxc-5db "")。

## 注意事项

当Object被转换为低频访问、归档存储、冷归档存储或者深度冷归档存储类型后，需注意以下事项：

### 最小计量空间

对于小于64 KB的Object，会按照64 KB计算空间大小。

### 最低存储时长

低频访问类型的Object需至少存储30天，归档存储类型的Object需至少存储60天，冷归档存储类型的Object需至少存储180天，深度冷归档存储类型的Object需至少存储180天。如果存储未满指定周期，会对应收取存储不足规定时长容量费用。更多信息，请参见 [存储费用](https://help.aliyun.com/zh/oss/storage-fees#concept-2558327 "")。

- 通过生命周期自动转换Object存储类型

  - 将Object存储类型转换为低频、归档类型时，不会重新计算Object的存储时间。

    例如，a.txt作为标准存储类型已在OSS中存储了10天，通过生命周期转换为低频访问类型，则继续存储20天即可满足最低存储时长30天的要求。

  - 将Object存储类型转换为冷归档或者深度冷归档类型时，会重新计算Object的存储时间。

    - 示例1：a.txt作为标准存储类型或者低频访问类型已在OSS中存储了10天，通过生命周期规则转换为冷归档或者深度冷归档类型，需继续存储180天才满足最低存储时长180天的要求。

    - 示例2：a.txt作为冷归档类型已在OSS中存储了30天，通过生命周期规则转换为深度冷归档，将收取冷归档存储不足规定时长180天的费用。此外，转为深度冷归档后，需继续存储180天后才满足最低存储时长180天的要求。
- 通过CopyObject手动转换Object存储类型

通过CopyObject手动转换Object为任意存储类型时，会重新计算Object的存储时间。

例如，a.txt作为标准存储类型已在OSS中存储了10天，通过CopyObject手动将Object转换为低频访问类型，需继续存储30天才满足最低存储时长30天的要求。


**说明**

如果您在低频访问、归档、冷归档或者深度冷归档类型的Object存储未满规定时长前，进行重命名或者通过上传同名文件进行覆写等操作，会产生存储不足规定时长容量费用。例如，您在低频访问类型Object存储29天后执行了重命名操作，OSS将重新计算Object的最后修改时间，即您需要继续存储30天才能满足低频访问最低存储时长的要求。

### 解冻时间

归档存储、冷归档存储和深度冷归档存储类型Object恢复为可读取状态需要一定的解冻时间，如果业务场景需要实时读取Object时，不建议将Object转换成归档存储、冷归档存储或深度冷归档存储类型。

### **请求费用**

| **转换存储类型的方式** | **Object源存储类型** | **请求费用** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **转换存储类型的方式** | **Object源存储类型** | **请求费用** |
| 通过生命周期规则 | 标准、低频访问、归档、冷归档 | 按照Object的源存储类型收取Put类请求费用，计量到当前Bucket。 |
| 通过CopyObject | 归档存储 | - ①已开启归档直读<br>  <br>  - 按Object源存储类型收取Get类请求费用，计量到源Bucket。<br>    <br>  - 按Object的目标存储类型收取Put类请求费用，计量到目标Bucket。<br>- ②未开启归档直读<br>  <br>  按Object源存储类型收取Put类请求费用，计量到目标Bucket。 |
| 标准、低频访问、冷归档、深度冷归档 | 按Object源存储类型收取Put类请求费用，计量到目标Bucket。 |

①在已开启归档直读的情况下，通过CopyObject将归档存储类型的源Object转换为其他存储类型时，无需提前解冻，不会产生归档存储数据取回容量费用，但会产生归档直读数据取回容量费用。

②在未开启归档直读的情况下，通过CopyObject将归档存储类型的源Object转换为其他存储类型时，需提前解冻，会产生归档存储数据取回容量费用，不会产生归档直读数据取回容量费用。

更多信息，请参见 [数据处理费用](https://help.aliyun.com/zh/oss/data-processing-fees "")。

### 数据取回费用

访问低频访问类型的Object时，会根据实际访问量额外收取数据取回费用。解冻归档存储、冷归档存储和深度冷归档存储类型的Object会额外收取数据解冻费用。开启归档直读后，直接访问归档存储数据的Object会额外收取归档直读费用。这些费用与流出流量费用是两个独立计费项。如果Object每月平均访问频率高于1次，Object转换成低频访问、归档存储、冷归档存储或深度冷归档存储类型后的使用成本可能高于标准存储类型。

### 临时存储费用

冷归档存储和深度冷归档存储类型Object在数据解冻时会生成一份标准存储类型的Object副本用于访问。该Object在解冻时间结束前会以标准存储的存储费率计算临时存储费用。

## 常见问题

### 基于最后一次修改时间的生命周期规则是否支持将Object从低频访问类型转换为标准类型？

不支持。您可以通过以下方式将Object从低频访问类型转为标准类型：

- 通过CopyObject的方式

CopyObject接口支持将单个Object从低频访问类型转为标准类型。具体操作，请参见 [通过CopyObject接口手动转换Object的存储类型](https://help.aliyun.com/zh/oss/user-guide/convert-storage-classes#section-6ir-ldn-d7s "")。

- 通过ossutil工具

ossutil支持通过set-props命令添加--storage-class选项将Object从低频访问类型转换为标准类型。具体操作，请参见 [set-props（设置对象属性）](https://help.aliyun.com/zh/oss/developer-reference/set-props-set-object-properties#615a9e87baeeo "")。