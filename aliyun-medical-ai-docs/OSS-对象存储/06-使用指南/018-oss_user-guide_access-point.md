### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[权限与访问控制](https://help.aliyun.com/zh/oss/user-guide/permissions-and-access-controls/)接入点

# 通过接入点访问OSS

更新时间：2026-02-12 02:23:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用资源组进行精细化资源控制](https://help.aliyun.com/zh/oss/user-guide/fine-grained-resource-control-using-resource-groups-49)[下一篇：基于 OSS 接入点与 VPC 网关终端节点构建安全的多租户私网访问架构](https://help.aliyun.com/zh/oss/user-guide/build-a-secure-multi-tenant-private-network-access-architecture)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

工作原理

快速使用

步骤一：创建接入点

步骤二：接入点权限委派

步骤三：使用接入点访问

场景示例

场景描述

方案设计

AP Policy配置

Bucket Policy权限委派

权限判定逻辑

配额与限制

常见问题

相关文档

接入点（Access Point）为存储空间（Bucket）提供独立的访问入口。当一个Bucket需要被多个应用或团队以不同权限访问时，可为每个访问方创建独立的接入点，通过接入点策略（AP Policy）分别管理各自的权限，避免在单一Bucket Policy中维护复杂的权限规则。

## **工作原理**

接入点是Bucket的访问代理层。创建接入点后，OSS会生成一个唯一的 **接入点别名**，用户使用该别名替代Bucket名称发起请求。每个接入点可配置独立的 **AP Policy**（定义可执行的操作、可访问的资源和允许的身份）和 **网络来源**（互联网或仅限指定VPC），实现基于业务场景的隔离访问。

用户通过接入点访问时，系统会综合评估 [RAM Policy](https://help.aliyun.com/zh/oss/user-guide/ram-policy/ "")、 [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "") 和AP Policy三层策略，只有当RAM Policy与Bucket Policy的组合判定结果为Allow，且AP Policy也为Allow时，请求才会被允许。权限策略的详细判定逻辑请参见 [权限判定逻辑](https://help.aliyun.com/zh/oss/user-guide/access-point/#50961a1c83kgm "")。

接入点默认无法访问Bucket资源，需要先在Bucket Policy中配置 **权限委派**（通过`oss:DataAccessPointArn`、`oss:DataAccessPointAccount`或`oss:AccessPointNetworkOrigin`条件键），明确授权特定接入点访问该Bucket。

## **快速使用**

接下来将通过创建接入点、配置权限委派和使用接入点访问三个步骤，指导快速上手使用接入点功能。

### **步骤一：创建接入点**

创建接入点并配置接入点策略，定义“ **哪些身份**”、“ **在什么条件下**”，可以通过接入点“ **对哪些OSS资源**”、“ **执行何种操作**”。

1. 前往 [接入点列表](https://oss.console.aliyun.com/access-point)，单击 **创建接入点**。

2. 输入 **接入点名称**，选择关联的Bucket和网络来源，单击 **下一步**。



**说明**





   - **网络来源** 选择 **VPC** 时，需要输入 **VPC ID**，可前往 [VPC控制台](https://vpc.console.aliyun.com/vpc) 获取。

   - 输入的VPC地域必须与 [OSS支持的网关终端节点地域](https://help.aliyun.com/zh/oss/oss-supported-gateway-endpoint-regions "") 保持一致，地域不匹配将导致鉴权请求无法正确关联到指定VPC，从而引发鉴权失败。


3. 关闭 **阻止公共访问** 选项，并配置接入点策略。






按图形策略添加



按语法策略添加



















|     |     |
| --- | --- |
| **配置项** | **说明** |
| **授权资源** | 选择授权对象是 **整个Bucket** 还是 **指定资源**。 |
| **资源路径** | - **授权资源** 选择 **整个Bucket** 时， **资源路径** 为`accesspoint/{接入点名称}/*`。<br>     <br>   - **授权资源** 选择 **指定资源** 时，填写待授权资源的目录或单个Object，支持添加多条记录。 |
| **授权用户** | 指定被授权对象。<br>   - **子账号**：选择当前阿里云账号下的RAM用户。<br>     <br>     当前登录账号必须是阿里云主账号或拥有此Bucket管理权限及RAM控制台`ListUsers`权限的RAM用户，否则无法查看当前账号的RAM用户列表。<br>     <br>   - **其他账号**：填写其他待授权账号、子账号的UID或以`arn:sts`开头的临时授权用户（如`arn:sts::1798************:assumed-role/role-name/session-name`）。支持授权给多个用户，一行填写一个。 |
| **授权操作** | - **简单设置**：选择常见的授权操作组合，可选设置项包括 **只读（不包含ListObject操作）**、 **只读（包含ListObject操作）**、 **读/写**、 **完全控制**、 **拒绝访问**。<br>     <br>   - **高级设置**：自定义授权 **效力**（ **允许** 或 **拒绝**）和授权 **操作**。 |



在编辑框内输入JSON格式的授权策略。



> 示例授权策略：授予用户`20816353761158****`读/写权限。

















```json
{
     "Version": "1",
     "Statement": [{\
       "Effect": "Allow",\
       "Action": [\
         "oss:GetObject",\
         "oss:PutObject",\
         "oss:GetObjectAcl",\
         "oss:PutObjectAcl",\
         "oss:ListObjects",\
         "oss:AbortMultipartUpload",\
         "oss:ListParts",\
         "oss:RestoreObject",\
         "oss:ListObjectVersions",\
         "oss:GetObjectVersion",\
         "oss:GetObjectVersionAcl",\
         "oss:RestoreObjectVersion"\
       ],\
       "Principal": [\
         "20816353761158****"\
       ],\
       "Resource": [\
         "acs:oss:{region-id}:179882766168****:accesspoint/{ap-name}/object/*"\
       ]\
     }, {\
       "Effect": "Allow",\
       "Action": [\
         "oss:ListObjects",\
         "oss:GetObject"\
       ],\
       "Principal": [\
         "20816353761158****"\
       ],\
       "Resource": [\
         "acs:oss:{region-id}:179882766168****:accesspoint/{ap-name}"\
       ],\
       "Condition": {\
         "StringLike": {\
           "oss:Prefix": [\
             "*"\
           ]\
         }\
       }\
     }]
}
```





完整的授权策略包含 **Version**（版本号）和 **Statement**（授权语句）。



   - **Version**：权限策略版本，固定为`1`，不允许修改。

   - **Statement**：策略语句的主体，包含一条或多条具体的授权/拒绝规则。每条授权语句包含 **Effect**（授权效力）、 **Action**（授权操作）、 **Principal**（授权主体）、 **Resource**（授权资源）和 **Condition**（授权条件）。


     |     |     |
     | --- | --- |
     | **策略元素** | **说明** |
     | **Effect** | 策略的效力，可选值为`Allow`（允许）或`Deny`（拒绝）。 |
     | **Action** | 对资源执行的具体操作，支持使用通配符`*`。 |
     | **Principal** | 策略作用的主体（用户、账号、角色等）。 |
     | **Resource** | 策略作用的资源范围。 |
     | **Condition** | 策略生效的条件。<br>当配置多个条件时， **所有条件必须同时满足**（AND关系），策略才会生效。 |


     完整的授权元素列表请参见 [授权语法与元素](https://help.aliyun.com/zh/oss/user-guide/authorization-syntax-and-elements "")。


4. 单击 **提交**，等待接入点创建完成。


### **步骤二：接入点权限委派**

创建接入点后，还需要通过Bucket Policy设置接入点权限委派，即定义哪些接入点能够访问Bucket。接入点权限委派提供三种类型：

- `oss:DataAccessPointArn`：指定接入点的访问权限委派。

- `oss:DataAccessPointAccount`：当前主账号下所有接入点的访问权限委派。

- `oss:AccessPointNetworkOrigin`：指定网络来源的所有接入点访问权限委派。


指定接入点权限委派

所有接入点权限委派

指定网络来源权限委派

1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket。

2. 在左侧菜单栏单击**权限控制** \> **Bucket 授权策略**，选择 **按语法策略添加**。

3. 单击 **编辑**，在编辑框内输入JSON格式的授权策略。



**说明**





配置时请替换示例内的UID、Bucket名称、地域ID和接入点名称。如果原来的Bucket Policy不为空，请在原有的Bucket Policy中追加`Statement`元素。



















```json
{
     "Version": "1",
     "Statement": [{\
       "Effect": "Allow",\
       "Action": [\
         "oss:*"\
       ],\
       "Principal": [\
         "*"\
       ],\
       "Resource": [\
         "acs:oss:*:179882766168****:example-bucket",\
         "acs:oss:*:179882766168****:example-bucket/*"\
       ],\
       "Condition": {\
         "StringEquals": {\
           "oss:DataAccessPointArn": [\
             "acs:oss:oss-{region-id}:179882766168****:accesspoint/{ap-name}"\
           ]\
         }\
       }\
     }]
}
```

4. 单击 **保存**，完成Bucket Policy配置。


1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket。

2. 在左侧菜单栏单击**权限控制** \> **Bucket 授权策略**，选择 **按语法策略添加**。

3. 单击 **编辑**，在编辑框内输入JSON格式的授权策略。



**说明**





配置时请替换示例内的UID和Bucket名称。如果原有的Bucket Policy不为空，请在原有的Bucket Policy中追加`Statement`元素。



















```json
{
     "Version": "1",
     "Statement": [{\
       "Effect": "Allow",\
       "Action": [\
         "oss:*"\
       ],\
       "Principal": [\
         "*"\
       ],\
       "Resource": [\
         "acs:oss:*:179882766168****:example-bucket",\
         "acs:oss:*:179882766168****:example-bucket/*"\
       ],\
       "Condition": {\
         "StringEquals": {\
           "oss:DataAccessPointAccount": [\
             "179882766168****"\
           ]\
         }\
       }\
     }]
}
```

4. 单击 **保存**，完成Bucket Policy配置。


1. 前往 [Bucket列表](https://oss.console.aliyun.com/bucket)，单击目标Bucket。

2. 在左侧菜单栏单击**权限控制** \> **Bucket 授权策略**，选择 **按语法策略添加**。

3. 单击 **编辑**，在编辑框内输入JSON格式的授权策略。



**说明**





   - 配置时需替换示例中的UID和Bucket名称。若原有Bucket Policy已包含内容，需在现有策略的`Statement`数组中追加新元素。

   - 当`oss:AccessPointNetworkOrigin`设置为`internet`时，委派所有网络来源为互联网的接入点，此配置同时允许外网和VPC访问。如需限制仅允许VPC访问，需将该值修改为`vpc`。


```json
{
  "Version": "1",
  "Statement": [{\
    "Effect": "Allow",\
    "Action": [\
      "oss:*"\
    ],\
    "Principal": [\
      "*"\
    ],\
    "Resource": [\
      "acs:oss:*:179882766168****:example-bucket",\
      "acs:oss:*:179882766168****:example-bucket/*"\
    ],\
    "Condition": {\
      "StringEquals": {\
        "oss:AccessPointNetworkOrigin": [\
          "internet"\
        ]\
      }\
    }\
  }]
}
```

4. 单击 **保存**，完成Bucket Policy配置。


**说明**

如果提示“Bucket Policy 中包含公共访问语义”，请先关闭Bucket的 **阻止公共访问** 选项，再进行接入点权限委派。

### **步骤三：使用接入点访问**

创建接入点后，OSS会自动生成接入点别名。使用被授权的身份（如RAM用户）通过该别名即可访问对应的OSS资源。

**点击查看接入点兼容的操作**

|     |     |
| --- | --- |
| **接口** | **说明** |
| [PutAccessPointPolicy](https://help.aliyun.com/zh/oss/developer-reference/putaccesspointpolicy "") | 配置接入点策略。 |
| [GetAccessPointPolicy](https://help.aliyun.com/zh/oss/developer-reference/getaccesspointpolicy "") | 获取接入点策略配置。 |
| [DeleteAccessPointPolicy](https://help.aliyun.com/zh/oss/developer-reference/deleteaccesspointpolicy "") | 删除接入点策略。 |
| [ListObjects（GetBucket）](https://help.aliyun.com/zh/oss/developer-reference/listobjects "") | 列举Bucket中所有文件（Object）的信息。 |
| [ListObjectsV2（GetBucketV2）](https://help.aliyun.com/zh/oss/developer-reference/listobjects-v2 "") |
| [ListObjectVersions（GetBucketVersions）](https://help.aliyun.com/zh/oss/developer-reference/listobjectversions "") | 列出 Bucket 中包括删除标记（Delete Marker）在内的所有 Object 的版本信息。 |
| [PutObject](https://help.aliyun.com/zh/oss/developer-reference/putobject "") | 上传Object。 |
| [GetObject](https://help.aliyun.com/zh/oss/developer-reference/getobject "") | 获取Object。 |
| [CopyObject](https://help.aliyun.com/zh/oss/developer-reference/copyobject "") | 拷贝Object。 |
| [AppendObject](https://help.aliyun.com/zh/oss/developer-reference/appendobject "") | 以追加写的方式上传Object。 |
| [DeleteObject](https://help.aliyun.com/zh/oss/developer-reference/deleteobject "") | 删除单个Object。 |
| [DeleteMultipleObjects](https://help.aliyun.com/zh/oss/developer-reference/deletemultipleobjects "") | 删除多个Object。 |
| [HeadObject](https://help.aliyun.com/zh/oss/developer-reference/headobject "") | 只返回某个Object的所有元数据，不返回文件内容。 |
| [GetObjectMeta](https://help.aliyun.com/zh/oss/developer-reference/getobjectmeta "") | 返回Object的部分元数据，包括该Object的ETag、Size（文件大小）以及LastModified等，不返回文件内容。 |
| [PostObject](https://help.aliyun.com/zh/oss/developer-reference/postobject "") | 通过HTML表单上传的方式上传Object。 |
| [RestoreObject](https://help.aliyun.com/zh/oss/developer-reference/restoreobject "") | 解冻归档存储、冷归档存储或者深度冷归档存储类型的Object。 |
| [SelectObject](https://help.aliyun.com/zh/oss/developer-reference/selectobject "") | 对目标文件执行SQL语句，返回执行结果。 |
| [InitiateMultipartUpload](https://help.aliyun.com/zh/oss/developer-reference/initiatemultipartupload "") | 初始化一个Multipart Upload事件。 |
| [UploadPart](https://help.aliyun.com/zh/oss/developer-reference/uploadpart "") | 根据指定的Object名和uploadId来分块（Part）上传数据。 |
| [UploadPartCopy](https://help.aliyun.com/zh/oss/developer-reference/uploadpartcopy "") | 通过在UploadPart请求的基础上增加一个请求头x-oss-copy-source来调用UploadPartCopy接口，实现从一个已存在的Object中拷贝数据来上传一个Part。 |
| [CompleteMultipartUpload](https://help.aliyun.com/zh/oss/developer-reference/completemultipartupload "") | 在将所有数据Part都上传完成后，必须调用该接口来完成整个文件的分片上传。 |
| [AbortMultipartUpload](https://help.aliyun.com/zh/oss/developer-reference/abortmultipartupload "") | 取消Multipart Upload事件并删除对应的Part数据。 |
| [ListMultipartUploads](https://help.aliyun.com/zh/oss/developer-reference/listmultipartuploads "") | 列举所有执行中的Multipart Upload事件，即已经初始化但还未完成（Complete）或者还未中止（Abort）的Multipart Upload事件。 |
| [ListParts](https://help.aliyun.com/zh/oss/developer-reference/listparts "") | 列举指定uploadId所属的所有已经上传成功Part。 |
| [PutObjectACL](https://help.aliyun.com/zh/oss/developer-reference/putobjectacl "") | 修改Object的访问权限。 |
| [GetObjectACL](https://help.aliyun.com/zh/oss/developer-reference/getobjectacl "") | 查看Object的访问权限。 |
| [PutSymlink](https://help.aliyun.com/zh/oss/developer-reference/putsymlink "") | 创建软链接。 |
| [GetSymlink](https://help.aliyun.com/zh/oss/developer-reference/getsymlink "") | 获取软链接。 |
| [PutObjectTagging](https://help.aliyun.com/zh/oss/developer-reference/putobjecttagging "") | 设置或更新对象标签。 |
| [GetObjectTagging](https://help.aliyun.com/zh/oss/developer-reference/getobjecttagging "") | 获取对象标签信息。 |
| [DeleteObjectTagging](https://help.aliyun.com/zh/oss/developer-reference/deleteobjecttagging "") | 删除指定的对象标签。 |

SDK

ossutil

REST API

目前仅Java SDK和Python SDK支持通过接入点别名访问OSS资源。

Java

Python

Java

```java
import com.aliyun.sdk.service.oss2.OSSClient;
import com.aliyun.sdk.service.oss2.credentials.CredentialsProvider;
import com.aliyun.sdk.service.oss2.credentials.StaticCredentialsProvider;
import com.aliyun.sdk.service.oss2.models.GetObjectRequest;

import java.io.File;

/**
 * OSS Java SDK V2 示例：使用接入点下载对象到本地文件
 */
public class DownloadObjectWithAccessPoint {

    public static void main(String[] args) {
        // 创建OSS客户端
        String accessKeyId = System.getenv("OSS_ACCESS_KEY_ID");
        String accessKeySecret = System.getenv("OSS_ACCESS_KEY_SECRET");
        CredentialsProvider provider = new StaticCredentialsProvider(accessKeyId, accessKeySecret);
        OSSClient client = OSSClient.newBuilder()
                .credentialsProvider(provider)
                .region("<region-id>")
                .build();

        // 使用接入点别名下载对象到本地文件
        String bucket = "example-ap-b156d01070a10322664d6704cd1d47****-ossalias";
        String key = "example.jpg";
        File file = new File("example.jpg");
        client.getObjectToFile(GetObjectRequest.newBuilder()
                .bucket(bucket)
                .key(key)
                .build(), file);
        System.out.println("文件下载完成: " + key + " -> " + file.getPath());

        // 关闭客户端
        try {
            client.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

Python

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""OSS Python SDK V2 示例：使用接入点下载对象到本地文件"""

import alibabacloud_oss_v2 as oss

def main() -> None:
    """主函数"""
    # 创建OSS客户端
    credentials_provider = oss.credentials.EnvironmentVariableCredentialsProvider()
    config = oss.config.load_default()
    config.credentials_provider = credentials_provider
    config.region = "<region-id>"
    config.endpoint = "oss-<region-id>.aliyuncs.com"
    client = oss.Client(config)

    # 使用接入点别名下载对象到本地文件
    bucket = "example-ap-b156d01070a10322664d6704cd1d47****-ossalias"
    key = "example.jpg"
    file_path = "example.jpg"
    request = oss.GetObjectRequest(bucket, key)
    client.get_object_to_file(request, file_path)
    print(f"文件下载完成: {key} -> {file_path}")

if __name__ == "__main__":
    main()
```

使用ossutil访问OSS资源时，将接入点别名作为Bucket名称。

```bash
ossutil cp oss://example-ap-b156d01070a10322664d6704cd1d47****-ossalias/example.jpg /tmp
```

使用REST API访问OSS资源时，需要在Host中使用接入点别名。示例如下：

```http
GET /ObjectName HTTP/1.1
Host: example-ap-b156d01070a10322664d6704cd1d47****-ossalias.oss-{region-id}.aliyuncs.com
Date: GMT Date
Authorization: SignatureValue
```

## **场景示例**

以下示例展示了如何为大数据分析场景设计接入点方案，通过细粒度权限控制实现多部门安全隔离访问。

### **场景描述**

某公司（阿里云账号UID为`137918634953****`）将统一采集的数据存放在存储空间`examplebucket`中，该Bucket需要被10个不同业务部门访问，具体需求如下：

| **部门** | **访问范围** | **权限要求** | **网络来源** |
| --- | --- | --- | --- |

|     |     |     |     |
| --- | --- | --- | --- |
| **部门** | **访问范围** | **权限要求** | **网络来源** |
| 部门1~3 | `dir1/`目录 | 只读 | 互联网 |
| 部门4 | 整个Bucket | 读写 | 互联网 |
| 部门5~10 | `dir2/`目录 | 读写 | 仅VPC |

### **方案设计**

基于业务隔离和安全边界需求，设计3个接入点分别对应不同的访问场景，通过接入点策略实现精确的权限控制和网络访问限制。

| **接入点** | **名称** | **网络来源** | **授权用户** | **授权资源** | **权限** |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
| **接入点** | **名称** | **网络来源** | **授权用户** | **授权资源** | **权限** |
| 接入点1 | `ap-01` | 互联网 | 部门1~3的RAM用户（UID：`26571698800555****`） | `dir1/*` | 只读 |
| 接入点2 | `ap-02` | 互联网 | 部门4的RAM用户（UID：`25770968794578****`） | `*`（整个Bucket） | 读写 |
| 接入点3 | `ap-03` | VPC | 部门5~10的RAM用户（UID：`26806658794579****`） | `dir2/*` | 读写 |

### **AP Policy配置**

ap-01（部门1~3只读访问）

ap-02（部门4读写整个Bucket）

ap-03（部门5~10通过VPC读写）

```json
{
  "Version": "1",
  "Statement": [{\
    "Effect": "Allow",\
    "Action": [\
      "oss:GetObject",\
      "oss:GetObjectAcl",\
      "oss:ListObjects",\
      "oss:RestoreObject",\
      "oss:ListObjectVersions",\
      "oss:GetObjectVersion",\
      "oss:GetObjectVersionAcl",\
      "oss:RestoreObjectVersion"\
    ],\
    "Principal": [\
      "26571698800555****"\
    ],\
    "Resource": [\
      "acs:oss:{region-id}:137918634953****:accesspoint/ap-01/object/dir1/*"\
    ]\
  },{\
    "Effect": "Allow",\
    "Action": [\
      "oss:ListObjects",\
      "oss:GetObject"\
    ],\
    "Principal": [\
      "26571698800555****"\
    ],\
    "Resource": [\
      "acs:oss:{region-id}:137918634953****:accesspoint/ap-01"\
    ],\
    "Condition": {\
      "StringLike": {\
        "oss:Prefix": [\
          "dir1/*"\
        ]\
      }\
    }\
  }]
}
```

```json
{
  "Version": "1",
  "Statement": [{\
    "Effect": "Allow",\
    "Action": [\
      "oss:GetObject",\
      "oss:PutObject",\
      "oss:GetObjectAcl",\
      "oss:PutObjectAcl",\
      "oss:ListObjects",\
      "oss:AbortMultipartUpload",\
      "oss:ListParts",\
      "oss:RestoreObject",\
      "oss:ListObjectVersions",\
      "oss:GetObjectVersion",\
      "oss:GetObjectVersionAcl",\
      "oss:RestoreObjectVersion"\
    ],\
    "Principal": [\
      "25770968794578****"\
    ],\
    "Resource": [\
      "acs:oss:{region-id}:137918634953****:accesspoint/ap-02/object/*"\
    ]\
  },{\
    "Effect": "Allow",\
    "Action": [\
      "oss:ListObjects",\
      "oss:GetObject"\
    ],\
    "Principal": [\
      "25770968794578****"\
    ],\
    "Resource": [\
      "acs:oss:{region-id}:137918634953****:accesspoint/ap-02"\
    ],\
    "Condition": {\
      "StringLike": {\
        "oss:Prefix": [\
          "*"\
        ]\
      }\
    }\
  }]
}
```

```json
{
  "Version": "1",
  "Statement": [{\
    "Effect": "Allow",\
    "Action": [\
      "oss:GetObject",\
      "oss:PutObject",\
      "oss:GetObjectAcl",\
      "oss:PutObjectAcl",\
      "oss:ListObjects",\
      "oss:AbortMultipartUpload",\
      "oss:ListParts",\
      "oss:RestoreObject",\
      "oss:ListObjectVersions",\
      "oss:GetObjectVersion",\
      "oss:GetObjectVersionAcl",\
      "oss:RestoreObjectVersion"\
    ],\
    "Principal": [\
      "26806658794579****"\
    ],\
    "Resource": [\
      "acs:oss:{region-id}:137918634953****:accesspoint/ap-03/object/dir2/*"\
    ]\
  },{\
    "Effect": "Allow",\
    "Action": [\
      "oss:ListObjects",\
      "oss:GetObject"\
    ],\
    "Principal": [\
      "26806658794579****"\
    ],\
    "Resource": [\
      "acs:oss:{region-id}:137918634953****:accesspoint/ap-03"\
    ],\
    "Condition": {\
      "StringLike": {\
        "oss:Prefix": [\
          "dir2/*"\
        ]\
      }\
    }\
  }]
}
```

### **Bucket Policy权限委派**

由于该场景涉及同一账号下的多个接入点，建议使用`oss:DataAccessPointAccount`进行统一委派，简化Bucket Policy配置。如需更精细的控制，也可使用`oss:DataAccessPointArn`为每个接入点单独委派。

统一委派

单独委派

```json
{
  "Version": "1",
  "Statement": [{\
    "Effect": "Allow",\
    "Action": [\
      "oss:*"\
    ],\
    "Principal": [\
      "*"\
    ],\
    "Resource": [\
      "acs:oss:*:137918634953****:examplebucket",\
      "acs:oss:*:137918634953****:examplebucket/*"\
    ],\
    "Condition": {\
      "StringEquals": {\
        "oss:DataAccessPointAccount": [\
          "137918634953****"\
        ]\
      }\
    }\
  }]
}
```

```json
{
  "Version": "1",
  "Statement": [{\
    "Effect": "Allow",\
    "Action": [\
      "oss:*"\
    ],\
    "Principal": [\
      "*"\
    ],\
    "Resource": [\
      "acs:oss:*:137918634953****:examplebucket",\
      "acs:oss:*:137918634953****:examplebucket/*"\
    ],\
    "Condition": {\
      "StringEquals": {\
        "oss:DataAccessPointArn": [\
          "acs:oss:oss-{region-id}:137918634953****:accesspoint/ap-01",\
          "acs:oss:oss-{region-id}:137918634953****:accesspoint/ap-02",\
          "acs:oss:oss-{region-id}:137918634953****:accesspoint/ap-03"\
        ]\
      }\
    }\
  }]
}
```

## 权限判定逻辑

| **RAM Policy和Bucket Policy的合并结果** | **AP Policy结果** | **最终结果** |
| --- | --- | --- |

|     |     |     |
| --- | --- | --- |
| **RAM Policy和Bucket Policy的合并结果** | **AP Policy结果** | **最终结果** |
| Allow | Allow | Allow |
| Allow | Deny | Deny |
| Allow | Ignore | Ignore |
| Deny | Allow | Deny |
| Deny | Deny | Deny |
| Deny | Ignore | Deny |
| Ignore | Allow | Ignore |
| Ignore | Deny | Deny |
| Ignore | Ignore | Ignore |

- **Allow（允许）**：访问请求命中了权限策略中的Allow语句，且没有命中Deny语句。

- **Deny（显式拒绝）**：访问请求命中了权限策略中的Deny语句。即使同时命中了Allow语句，遵循Deny优先原则，判定结果仍为显式拒绝。

- **Ignore（隐式拒绝）**：访问请求既没有命中Allow语句，也没有命中Deny语句。RAM身份默认没有执行任何操作的权限，未被显式允许的操作都会被隐式拒绝。


## **配额与限制**

| **限制项** | **说明** |
| --- | --- |

|     |     |
| --- | --- |
| **限制项** | **说明** |
| 创建方式 | 支持通过OSS控制台、API和ossutil创建接入点，不支持通过SDK创建接入点。 |
| 数量 | 单个阿里云账号最多可创建1000个接入点。 |
| 修改规则 | 接入点创建后，仅支持修改接入点策略，不支持修改接入点基础信息（如接入点名称、接入点别名等）。 |
| 访问方式 | 不支持匿名访问。 |

## **常见问题**

#### **接入点的权限设置是否支持IP白名单？**

支持。可按语法策略添加接入点策略，添加`"IpAddress": {"acs:SourceIp": ["xxx"]}`条件限制。

#### **通过RAM用户创建接入点时需具备哪些权限？**

需要具备以下权限：`oss:CreateAccessPoint`、`oss:GetAccessPoint`、`oss:DeleteAccessPoint`、`oss:ListAccessPoints`、`oss:PutAccessPointPolicy`、`oss:GetAccessPointPolicy`、`oss:DeleteAccessPointPolicy`、`oss:PutBucketPolicy`、`oss:GetBucketPolicy`、`oss:DeleteBucketPolicy`。

## **相关文档**

- [CreateAccessPoint](https://help.aliyun.com/zh/oss/developer-reference/createaccesspoint "")、 [PutAccessPointPolicy](https://help.aliyun.com/zh/oss/developer-reference/putaccesspointpolicy "")、 [PutBucketPolicy](https://help.aliyun.com/zh/oss/developer-reference/putbucketpolicy "")

- [授权语法与元素](https://help.aliyun.com/zh/oss/user-guide/authorization-syntax-and-elements "")

- [RAM Policy](https://help.aliyun.com/zh/oss/user-guide/ram-policy/ "")

- [Bucket Policy](https://help.aliyun.com/zh/oss/user-guide/oss-bucket-policy/ "")