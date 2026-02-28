### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [Serverless 应用引擎](https://help.aliyun.com/zh/sae/) [操作指南](https://help.aliyun.com/zh/sae/user-guide/) [运维管理](https://help.aliyun.com/zh/sae/operation-and-maintenance-management-2-0/) [告警管理](https://help.aliyun.com/zh/sae/alert-management-overview2-0/) 管理联系人

# 管理联系人

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查看告警事件历史](https://help.aliyun.com/zh/sae/view-historical-alert-events)[下一篇：通知策略](https://help.aliyun.com/zh/sae/notification-policy)

该文章对您有帮助吗？

反馈

通知策略的匹配规则被触发时，可以向您指定的联系人发送通知。本文介绍如何设置联系人、联系人组、钉钉机器人，以及如何获取钉钉机器人Webhook地址创建Webhook告警。

## **联系人**

### **创建联系人**

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在左侧导航栏，选择**通知告警** \> **联系人管理**。

3. 在 **通知对象** 页面的 **联系人** 页签，单击 **新建联系人**。

4. 在 **新建联系人** 对话框，配置相关信息，然后单击 **确认**。



|     |     |
| --- | --- |
| **配置项** | **说明** |
| **姓名** | 自定义联系人姓名。 |
| **手机号** | 设置联系人的手机号后，可以通过电话和短信的方式接收告警通知。<br>**说明** <br>仅验证过的手机号可以在通知策略中使用电话的通知方式。验证手机号的操作，请参见 [验证手机号](https://help.aliyun.com/zh/sae/contact#section-3nz-61e-fty "")。 |
| **邮箱** | 设置联系人的邮箱地址后，可以通过邮箱接收告警通知。 |
| **联系人组** | 选择联系人需要加入的联系人组。创建联系人组的操作，请参见 [联系人组](https://help.aliyun.com/zh/sae/contact#section-1ck-txa-u4z "")。 |
| **电话通知失败补发类型** | 选择电话通知失败后，通知补发类型。您可以在 **联系人** 页签设置全局默认值。具体操作，请参见 [设置联系人默认配置](https://help.aliyun.com/zh/sae/contact#section-awy-3vp-15x "")。 |
| **用户标识** | 可以帮助系统区分不同的用户，并且在处理数据、查询信息或者进行其他操作时提供方便。 |









**说明**

   - 手机号码和邮箱至少填写一项，每个手机号码或邮箱只能用于一个联系人。

   - 如果您需要创建钉钉机器人，请在 **钉钉/飞书/企微** 页签新建钉钉机器人。具体操作，请参见 [钉钉机器人](https://help.aliyun.com/zh/sae/contact#82d189504cpe7 "")。


创建联系人后，您可以在 **联系人** 页签查询、编辑或删除联系人。

### **验证手机号**

仅验证过的手机号可以在通知策略中使用电话的通知方式。

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在左侧导航栏，选择**通知告警** \> **联系人管理**。

3. 在 **通知对象** 页面的 **联系人** 页签，选择为一个或多个联系人验证手机号。


   - 如需为单个联系人验证手机号：单击未验证手机号右侧的 **未验证**。

   - 如需为多个联系人批量验证手机号：在复选框选中需要验证手机号的联系人，然后单击 **批量验证**。


系统将会给各联系人发送验证手机号短信。

4. 使用浏览器打开短信中的链接。



![验证手机号短信](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5969260261/p253635.png)

5. 在验证页面确认手机号信息，然后单击 **验证**。


### **设置联系人默认配置**

告警通过电话通知失败后，您可以设置通知补发类型。

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在左侧导航栏，选择**通知告警** \> **联系人管理**。

3. 在 **通知对象** 页面的 **联系人** 页签，选择**更多操作** \> **联系人默认配置**。

4. 在弹出的对话框，选择通知补发类型，然后单击 **确认**。


## 联系人组

创建通知策略时，您可以将联系人组指定为通知对象。当通知策略的匹配规则被触发时，SAE告警管理会向该联系人组中的联系人通过电话、短信、邮件和钉钉等方式发送告警通知。

### **前提条件**

[创建联系人](https://help.aliyun.com/zh/sae/contact#section-yfw-gno-cad "")

### **创建联系人组**

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8816013371/p878314.png)

2. 在左侧导航栏，选择**通知告警** \> **联系人管理**。

3. 在 **通知对象** 页面的 **联系人** 页签，单击 **新建联系人组**。

4. 在 **新建联系组** 对话框，输入 **组名**，选择 **告警联系人**，并单击 **确认**。

创建成功后，对应的联系人组将显示在 **联系人** 页签的左侧列表中。


### **管理联系人组**

创建联系人组后，您可以在 **联系人** 页签查询、编辑或删除联系人组。

- 编辑联系人组：在目标联系人组右侧选择**![更多图标 ](<Base64-Image-Removed>)** \> **编辑组**，在弹出的对话框中修改联系人组的名称或包含的联系人，然后单击 **确认**。

- 查看联系人组详情：单击联系人组左侧的![Down arrow](<Base64-Image-Removed>)图标展开联系人组。

- 删除联系人组：在目标联系人组右侧选择**![更多图标 ](<Base64-Image-Removed>)** \> **删除组**，然后在弹出的提示对话框中单击 **确认**。







**重要**

  - 删除联系人组之前，请确保目标联系人组没有添加至通知策略中，否则可能导致告警通知无法发送。

  - 仅当前用户创建的联系人组支持删除。


## **钉钉机器人**

在SAE通知告警中创建钉钉机器人后，您可以在通知策略中指定对应的钉钉群用于接收告警。当通知策略的规则被触发时，系统会自动向您指定的钉钉群发送告警通知。钉钉群收到通知后，您可以在钉钉群中对告警进行管理。

### **在SAE控制台创建告警通知钉钉群**

1. 在钉钉群中创建自定义机器人并获取机器人Webhook地址。具体操作，请参见 [获取钉钉机器人Webhook地址](https://help.aliyun.com/zh/sae/contact#da1e52604cdg7 "")。

2. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](<Base64-Image-Removed>)

3. 在左侧导航栏，选择**通知告警** \> **联系人管理**，在 **通知对象** 页面的 **钉钉/飞书/企微** 页签，单击 **钉钉** 卡片。

4. 在 **创建钉钉机器人** 面板，设置相关信息，然后单击 **确定**。







**说明**

在通知策略中需要选择 **通知方式** 为 **钉钉** 才能在钉钉群中接收告警。具体操作，请参见 [通知策略](https://help.aliyun.com/zh/sae/notification-policy "")。






|     |     |
| --- | --- |
| **配置项** | **说明** |
| **名称** | 自定义钉钉机器人的名称。 |
| **签名密钥** | 可选，如配置了密钥则会通过加签的方式进行钉钉认证。如果没有配置密钥，默认使用关键字白名单的方式进行认证，白名单关键字为告警。更多信息，请参见 [钉钉官方文档](https://open.dingtalk.com/document/robots/customize-robot-security-settings)。 |
| **机器人地址** | 输入钉钉机器人的Webhook地址。 |
| **机器人是否发送每日统计** | 选中后，需要输入每日统计信息发送的时间点，使用英文半角逗号（,）分隔多个发送时间点，时间点格式为`HH:SS`。告警管理将在设置的时间点发送今日产生告警的总数、解决数和待解决数。 |
| **卡片内容配置** | 自定义告警通知卡片样式和内容。 |


### **在钉钉群管理告警**

在钉钉群中收到告警通知后，您可以在钉钉群里查看并管理告警。更多信息，请参见 [在告警通知群中处理告警](https://help.aliyun.com/zh/arms/alarm-operation-center/handle-alerts-in-group-chats#ul-orh-9ip-3qh "")。

## **获取钉钉机器人Webhook地址**

设置钉钉群或在联系人中设置钉钉机器人时，需要先在钉钉群中获取自定义机器人Webhook地址。本文介绍如何获取钉钉机器人Webhook地址。请按照以下步骤在钉钉群中添加自定义钉钉机器人并获取Webhook地址。

1. 在PC版钉钉上打开您想要添加报警机器人的钉钉群，并单击右上角的群设置图标。

2. 在 **群设置** 面板中单击 **机器人**，然后单击 **添加机器人**。

3. 在 **智能群助手** 面板单击 **添加机器人**，继续单击 **添加机器人**，然后选择添加 **自定义**。 ![image.png](<Base64-Image-Removed>)

4. 在 **群机器人** 对话框单击 **添加机器人** 区域的设置图标，然后选择添加 **自定义**。

5. 在 **机器人详情** 对话框单击 **添加**。

6. 在 **添加机器人** 对话框中执行以下操作。![db_add_custom_robot.png](<Base64-Image-Removed>)


1. 设置机器人头像和名字。

2. **安全设置** 选中 **自定义关键词**，设置关键词为SAE。

3. 选中 **我已阅读并同意《自定义机器人服务及免责条款》**。

4. 单击 **完成**。


**说明**

更多关于钉钉机器人的操作，请参见 [自定义机器人接入](https://developers.dingtalk.com/document/robots/custom-robot-access)。

7. 在 **添加机器人** 对话框中复制生成的机器人Webhook地址，然后单击 **完成**。



生成的Webhook地址可匹配联系人的通知方式，并用于设置事件中心的订阅规则。具体操作，请参见 [联系人管理](https://help.aliyun.com/zh/sae/contact-management "") 和 [事件中心](https://help.aliyun.com/zh/sae/event-center-new#DAS "")。![sc_create_a_new_contact_and_add_dingding_robot_webhook](<Base64-Image-Removed>)


## **通过Webhook自定义告警通知联系人**

创建通知策略时，您可以将告警通知发送到自定义的Webhook地址中。通知告警支持对飞书、微信、钉钉等群组发送Webhook告警。本文以飞书为例，介绍如何创建Webhook告警。

### **步骤一：获取Webhook地址**

1. 打开并登录飞书。

2. 单击 **+** 图标，然后单击 **创建群组**，新建一个用于发送告警的群组。

3. 单击群组设置图标，然后单击 **群机器人** 页签，在 **群机器人** 页签，单击 **添加机器人**。

4. 在 **添加机器人** 面板，选择 **Custom Bot**，然后在配置页，输入 **机器人名称** 与 **描述**，单击 **添加**。

5. 复制Webhook地址，然后选中 **自定义关键词** 并输入关键词为 **告警**，然后单击 **完成**。


### **步骤二：创建Webhook联系人**

1. 登录 [SAE控制台](https://saenext.console.aliyun.com/overview)，在左侧导航栏选择**应用管理** \> **应用列表**，然后选择目标地域和目标命名空间，最后单击目标应用名称。

![IXAcRBAUok](<Base64-Image-Removed>)

2. 在左侧导航栏，选择**通知告警** \> **联系人管理**。

3. 在 **通知对象** 页面的 **Webhook集成** 页签，单击 **新建Webhook**。

4. 在 **新建Webhook** 对话框，配置以下信息，然后单击 **确定**。



信息配置完成后，您可以先单击 **发送测试**，验证配置是否成功，然后再单击 **确定**。



|     |     |
| --- | --- |
| **配置项** | **说明** |
| **Webhook名称** | 自定义Webhook名称。 |
| **Post/Get** | 设置请求方法。URL不超过100个字符。<br>此例中选择Post，并将 [步骤一：获取Webhook地址](https://help.aliyun.com/zh/sae/contact#title-yie-3za-klc "") 中保存的Webhook地址粘贴至右侧文本框。 |
| **Header/Param** | 设置请求头，不可超过200个字符。 单击 **添加**，可以添加其他Header信息或Param信息。默认请求头为`Content-Type: text/plain; charset=UTF-8`，Header和Param个数总数不能超过6个。<br>此例中设置以下两个Header：<br>   - Arms-Content-Type : json<br>     <br>   - Content-Type : application/json |
| **通知模板** | 告警触发时发送的通知模板，在Post方法下出现，可使用$content占位符输出通知内容，不可超过500个字符。更多信息，请参见 [配置通知模板和Webhook模板](https://help.aliyun.com/zh/arms/alarm-operation-center/configure-notification-templates-and-webhook-templates#task-2082508 "")。<br>通知模板如下：<br>```json<br>{<br>"告警名称":"{{ .commonLabels.alertname }}{{if .commonLabels.clustername }}",<br>"集群名称":"{{ .commonLabels.clustername }} {{ end }}{{if eq "app" .commonLabels._aliyun_arms_involvedObject_kind }}",<br>"应用名称":"{{ .commonLabels._aliyun_arms_involvedObject_name }} {{ end }}",<br>"通知策略":"{{ .dispatchRuleName }}",<br>"告警时间":"{{ .startTime }}",<br>"告警内容":"{{ for .alerts }} {{ .annotations.message }} {{ end }}"<br>}<br>```<br>此处以飞书为例，可以设置如下文本格式：<br>```json<br>{<br>  "msg_type": "text",<br>  "content": {<br>    "text": "告警名称: {{ .commonLabels.alertname }}\n{{if .commonLabels.clustername }}集群名称: {{ .commonLabels.clustername }}\n{{ end }}{{if eq "app" .commonLabels._aliyun_arms_involvedObject_kind }}应用名称: {{ .commonLabels._aliyun_arms_involvedObject_name }}\n{{ end }}通知策略: {{ .dispatchRuleName }} \n告警时间: {{ .startTime }} \n告警内容: {{ for .alerts }} {{ .annotations.message }}\n {{ end }}"<br>  }<br>}<br>``` |
| **恢复模板** | 告警恢复时发送的通知模板，在Post方法下出现，可使用$content占位符输出通知内容，不超过500个字符。更多信息，请参见 [配置通知模板和Webhook模板](https://help.aliyun.com/zh/arms/alarm-operation-center/configure-notification-templates-and-webhook-templates#task-2082508 "")。<br>恢复模板如下：<br>```json<br>{<br>"告警名称":"{{ .commonLabels.alertname }}{{if .commonLabels.clustername }}",<br>"集群名称":"{{ .commonLabels.clustername }} {{ end }}{{if eq "app" .commonLabels._aliyun_arms_involvedObject_kind }}",<br>"应用名称":"{{ .commonLabels._aliyun_arms_involvedObject_name }} {{ end }}",<br>"通知策略":"{{ .dispatchRuleName }}",<br>"恢复时间":"{{ .endTime }}",<br>"告警内容":"{{ for .alerts }} {{ .annotations.message }} {{ end }}"<br>}<br>```<br>此处以飞书为例，可以设置如下文本格式：<br>```json<br>{<br>  "msg_type": "text",<br>  "content": {<br>    "text": "告警名称: {{ .commonLabels.alertname }}\n{{if .commonLabels.clustername }}集群名称: {{ .commonLabels.clustername }}\n{{ end }}{{if eq "app" .commonLabels._aliyun_arms_involvedObject_kind }}应用名称: {{ .commonLabels._aliyun_arms_involvedObject_name }}\n{{ end }}恢复时间: {{ .startTime }} \n通知策略: {{ .dispatchRuleName }} \n恢复告警内容: {{ for .alerts }} {{ .annotations.message }}\n {{ end }}"<br>  }<br>}<br>``` |


### **步骤三：设置通知策略**

新建或编辑通知策略，选择 **通知对象** 为 **通用Webhook**，然后选择对应的Webhook集成。具体操作，请参见 [通知策略](https://help.aliyun.com/zh/sae/notification-policy "")。

**说明**

Webhook告警的超时时间为5秒，如果发出请求后5秒内没有返回，即没有收到告警信息，则表示发送失败。