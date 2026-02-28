### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/)[开发参考](https://help.aliyun.com/zh/sae/developer-reference/)[Terraform](https://help.aliyun.com/zh/sae/terraform-new/)使用Terraform管理SAE命名空间

# 使用Terraform管理SAE命名空间

更新时间：2025-02-20 03:15:44

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：Terraform概述](https://help.aliyun.com/zh/sae/terraform-overview)[下一篇：使用Terraform管理SAE应用](https://help.aliyun.com/zh/sae/use-terraform-to-manage-sae-applications)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

前提条件

使用的资源

创建命名空间

更新命名空间

删除命名空间

完整示例

相关文档

Serverless 应用引擎 SAE（Serverless App Engine）的命名空间可以将您的应用从逻辑上进行划分，例如测试环境、开发环境、预发环境和线上环境等。本文介绍如何通过Terraform创建、更新和删除SAE命名空间。

**说明**

本教程所含示例代码支持一键运行，您可以直接运行代码。 [一键运行](https://api.aliyun.com/api-tools/terraform?resource=alicloud_sae_namespace&exampleId=201-use-case-manage-sae-namespaces&activeTab=example)

## 前提条件

- 由于阿里云账号（主账号）具有资源的所有权限，一旦发生泄露将面临重大风险。建议您使用RAM用户，并为该RAM用户创建AccessKey，具体操作方式请参见 [创建RAM用户](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "") 和 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "")。

- 为运行Terraform命令的RAM用户绑定以下最小权限策略，以获取管理本示例所涉及资源的权限。更多信息，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user "")。


该权限策略允许用户管理SAE命名空间，包括创建、删除、更新、查看和列出命名空间。















```yaml
{
      "Version": "1",
      "Statement": [\
          {\
              "Effect": "Allow",\
              "Action": [\
                  "sae:CreateNamespace",\
                  "sae:DeleteNamespace",\
                  "sae:UpdateNamespace",\
                  "sae:GetNamespace",\
                  "sae:ListNamespaces"\
              ],\
              "Resource": "*"\
          }\
      ]
}
```

- 准备Terraform运行环境，您可以选择以下任一方式来使用Terraform。



  - ROS提供了Terraform托管服务，因此您可以直接在 [ROS控制台](https://ros.console.aliyun.com/cn-hangzhou/welcome) 部署Terraform模板。详细操作，请参见 [创建Terraform类型资源栈](https://help.aliyun.com/zh/ros/user-guide/create-a-terraform-stack "")。

  - [在Terraform Explorer中使用Terraform](https://help.aliyun.com/zh/terraform/using-terraform-in-terraform-explorer "")：阿里云提供了Terraform的在线运行环境，您无需安装Terraform，登录后即可在线使用和体验Terraform。适用于零成本、快速、便捷地体验和调试Terraform的场景。

  - [Cloud Shell](https://help.aliyun.com/zh/terraform/use-terraform-in-cloud-shell "")：阿里云Cloud Shell中预装了Terraform的组件，并已配置好身份凭证，您可直接在Cloud Shell中运行Terraform的命令。适用于低成本、快速、便捷地访问和使用Terraform的场景。

  - [在本地安装和配置Terraform](https://help.aliyun.com/zh/terraform/install-and-configure-terraform-locally "")：适用于网络连接较差或需要自定义开发环境的场景。


## 使用的资源

- [alicloud\_sae\_namespace](https://help.aliyun.com/zh/terraform/alicloud-sae-namespace "")：用于创建和管理阿里云SAE的命名空间。


## 创建命名空间

本示例以在华东1（杭州）地域下创建命名空间为例，命名空间名称为admin、命名空间ID为`cn-hangzhou:admin`。

1. 创建一个用于存放Terraform资源的项目文件夹，命名为terraform。
2. 执行以下命令，进入项目目录。
















```plaintext
cd terraform
```

3. 执行以下命令，创建名为main.tf的配置文件。

















```terraform
provider "alicloud" {
     region = var.region_id
}

# 定义区域变量，默认值为 cn-hangzhou
variable "region_id" {
     type    = string
     default = "cn-hangzhou"
}

# 定义命名空间描述变量，默认值为 "a namespace sample"
variable "namespace_description" {
     description = "Namespace Description"
     default     = "a namespace sample"
}

# 定义命名空间名称变量，默认值为 "admin"
variable "namespace_name" {
     description = "Namespace Name"
     type        = string
     default     = "admin"
}

# 定义命名空间ID变量，默认值为 "cn-hangzhou:admin"
variable "namespace_id" {
     description = "Namespace ID"
     type        = string
     default     = "cn-hangzhou:admin"
}

resource "alicloud_sae_namespace" "default" {
     namespace_description = var.namespace_description
     namespace_id          = var.namespace_id
     namespace_name        = var.namespace_name
}

output "namespace_id" {
     value       = alicloud_sae_namespace.default.namespace_id
     description = "The ID of the created namespace."
}
```

4. 执行以下命令，初始化Terraform运行环境。















```terraform
terraform init
```

5. 预期输出：



















```terraform
Initializing the backend...

Initializing provider plugins...
- Checking for available provider plugins...
- Downloading plugin for provider "alicloud" (hashicorp/alicloud) 1.233.0...

The following providers do not have any version constraints in configuration,
so the latest version was installed.

To prevent automatic upgrades to new major versions that may contain breaking
changes, it is recommended to add version = "..." constraints to the
corresponding provider blocks in configuration, with the constraint strings
suggested below.

* provider.alicloud: version = "~> 1.233"

Warning: registry.terraform.io: For users on Terraform 0.13 or greater, this provider has moved to aliyun/alicloud. Please update your source in required_providers.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

6. 依次执行以下命令，创建SAE命名空间。


1. 执行以下命令，执行配置文件。在执行过程中，根据提示输入`yes`并按下 **Enter** 键，等待命令执行完成，若出现以下信息，则表示授权完成。

















      ```terraform
      terraform apply
      ```









      预期输出：

















      ```terraform
      Apply complete! Resources: 1 added, 0 changed, 1 destroyed.

      Outputs:

      namespace_id = cn-hangzhou:admin
      ```


命名空间已成功创建。

7. 验证结果


执行terraform show命令

Serverless应用引擎SAE控制台

您可以使用以下命令查询Terraform已创建的资源详细信息：

```shell
terraform show
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3926489371/p869166.png)

登录 [Serverless应用引擎SAE控制台](https://saenext.console.aliyun.com/cn-hangzhou/namespace)，查看创建命名空间。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3439300471/p869168.png)

## 更新命名空间

本示例以更新命名空间名称为例，将华东1（杭州）地域下命名空间的名称从admin更新为`prod`。

1. 打开 main.tf 文件，将 namespace\_name 变量的默认值从 "admin" 修改为 "prod"。


```terraform
provider "alicloud" {
region = var.region_id
}

# 定义区域变量，默认值为 cn-hangzhou
variable "region_id" {
type    = string
default = "cn-hangzhou"
}

# 定义命名空间描述变量，默认值为 "a namespace sample"
variable "namespace_description" {
description = "Namespace Description"
default     = "a namespace sample"
}

# 修改定义命名空间名称变量为 "prod"
variable "namespace_name" {
description = "Namespace Name"
type        = string
default     = "prod"
}

# 定义命名空间ID变量，默认值为 "cn-hangzhou:dev"
variable "namespace_id" {
description = "Namespace ID"
type        = string
default     = "cn-hangzhou:admin"
}

resource "alicloud_sae_namespace" "default" {
namespace_description = var.namespace_description
namespace_id          = var.namespace_id
namespace_name        = var.namespace_name
}

output "namespace_id" {
value       = alicloud_sae_namespace.default.namespace_id
description = "The ID of the created namespace."
}
```

2. 执行如下命令，初始化Terraform运行环境。

















```shell
terraform init
```





返回信息如下，Terraform初始化成功。

















```json
Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```

3. 继续运行以下 命令来应用更改，在执行过程中，根据提示输入 yes 并按下 **Enter** 键，等待命令执行完成。


```shell
terraform apply
```

预期输出：

```terraform
alicloud_sae_namespace.default: Modifying... [id=cn-hangzhou:admin]
alicloud_sae_namespace.default: Modifications complete after 1s [id=cn-hangzhou:admin]

Apply complete! Resources: 0 added, 1 changed, 0 destroyed.

Outputs:

namespace_id = "cn-hangzhou:admin"
```

命名空间名称已成功更新为`prod`。

执行terraform show命令

Serverless应用引擎SAE控制台

您可以使用以下命令查询Terraform已创建的资源详细信息：

```shell
terraform show
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3926489371/p869323.png)

登录 [Serverless应用引擎SAE控制台](https://saenext.console.aliyun.com/cn-hangzhou/namespace)，查看修改后的命名空间。

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3439300471/p869308.png)

## 删除命名空间

本示例以在华东1（杭州）地域下删除命名空间为例，命名空间名称为`prod`、命名空间ID为`cn-hangzhou:admin`。

1. 在目标项目目录内执行以下命令，运行配置文件。关于`terraform destroy`的更多信息，请参见 [Terraform常用命令](https://help.aliyun.com/zh/terraform/terraform-common-commands "")。















```terraform
terraform destroy
```







预期输出：

















```terraform
alicloud_sae_namespace.default: Refreshing state... [id=cn-hangzhou:admin]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

# alicloud_sae_namespace.default will be destroyed
  - resource "alicloud_sae_namespace" "default" {
      - enable_micro_registration = true -> null
      - id                        = "cn-hangzhou:admin" -> null
      - namespace_description     = "a namespace sample" -> null
      - namespace_id              = "cn-hangzhou:admin" -> null
      - namespace_name            = "prod" -> null
      - namespace_short_id        = "admin" -> null
    }

Plan: 0 to add, 0 to change, 1 to destroy.

Changes to Outputs:
  - namespace_id = "cn-hangzhou:admin" -> null

Do you really want to destroy all resources?
Terraform will destroy all your managed infrastructure, as shown above.
There is no undo. Only 'yes' will be accepted to confirm.

Enter a value: yes

alicloud_sae_namespace.default: Destroying... [id=cn-hangzhou:admin]
alicloud_sae_namespace.default: Destruction complete after 1s

Destroy complete! Resources: 1 destroyed.
```

命名空间已成功删除。

## **完整示例**

**说明**

当前示例代码支持一键运行，您可以直接运行代码。 [一键运行](https://api.aliyun.com/api-tools/terraform?resource=alicloud_sae_namespace&exampleId=201-use-case-manage-sae-namespaces&activeTab=example)

```terraform
provider "alicloud" {
region = var.region_id
}

# 定义区域变量，默认值为 cn-hangzhou
variable "region_id" {
type    = string
default = "cn-hangzhou"
}

# 定义命名空间描述变量，默认值为 "a namespace sample"
variable "namespace_description" {
description = "Namespace Description"
default     = "a namespace sample"
}

# 定义命名空间名称变量，默认值为 "admin"
variable "namespace_name" {
description = "Namespace Name"
type        = string
default     = "admin"
}

# 定义命名空间ID变量，默认值为 "cn-hangzhou:admin"
variable "namespace_id" {
description = "Namespace ID"
type        = string
default     = "cn-hangzhou:admin"
}

resource "alicloud_sae_namespace" "default" {
namespace_description = var.namespace_description
namespace_id          = var.namespace_id
namespace_name        = var.namespace_name
}

output "namespace_id" {
value       = alicloud_sae_namespace.default.namespace_id
description = "The ID of the created namespace."
}
```

## **相关文档**

- Terrafrom介绍，请参见 [Terraform产品介绍](https://help.aliyun.com/zh/terraform/what-is-terraform "")。

- ROS提供了Terraform托管服务，因此您可以直接在 [ROS控制台](https://ros.console.aliyun.com/cn-hangzhou/welcome) 部署Terraform模板。详细操作，请参见 [创建Terraform类型资源栈](https://help.aliyun.com/zh/ros/user-guide/create-a-terraform-stack "")。

- 当您遇到由于网络延迟等原因造成的 terraform init 超时，导致无法正常下载 Provider 等情况时，请参见 [Terraform Init 加速方案配置](https://help.aliyun.com/zh/terraform/terraform-init-acceleration-solution-configuration "")。

- 关于如何配置Terraform的身份认证信息，请参见 [静配置身份认证](https://help.aliyun.com/zh/terraform/terraform-authentication#75fb0fdd14jef "")。