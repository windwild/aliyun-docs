### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-行业算法版](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/)[开发指南](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/development-guide/)[SDK参考](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/sdk-reference/)[PhpSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/phpsdk/)使用教程

# 使用教程

更新时间：2023-07-26 05:14:05

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：PhpSDK（查询/推送）](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/phpsdk/)[下一篇：相关下载](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/downloads-2)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

快速开始

配置环境变量

准备工作

主要功能client集合<参考>

上传文档格式

调试

## 快速开始

使用OpenSearch提供搜索功能十分简单，下面带大家迅速上手。

## **配置环境变量**

配置环境变量 **ALIBABA\_CLOUD\_ACCESS\_KEY\_ID** 和 **ALIBABA\_CLOUD\_ACCESS\_KEY\_SECRET**。

**重要**

- 阿里云账号AccessKey拥有所有API的访问权限，建议您使用RAM用户进行API访问或日常运维，具体操作，请参见 [创建RAM用户](https://help.aliyun.com/zh/ram/user-guide/create-a-ram-user "")。

- 创建AccessKey ID和AccessKey Secret，请参考 [创建AccessKey](https://help.aliyun.com/zh/ram/user-guide/create-an-accesskey-pair "")。

- 如果您使用的是RAM用户的AccessKey，请确保主账号已授权AliyunServiceRoleForOpenSearch服务关联角色，请参考 [OpenSearch-行业算法版服务关联角色](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/aliyunserviceroleforopensearch "")，相关文档参考 [访问鉴权规则](https://help.aliyun.com/zh/open-search/industry-algorithm-edition/access-authorization-rules "")。

- 请不要将AccessKey ID和AccessKey Secret保存到工程代码里，否则可能导致AccessKey泄露，威胁您账号下所有资源的安全。


- **Linux** 和 **macOS系统** 配置方法：

执行以下命令，其中，`<access_key_id>`需替换为您RAM用户的AccessKey ID，`<access_key_secret>`替换为您RAM用户的AccessKey Secret。















```java
export ALIBABA_CLOUD_ACCESS_KEY_ID=<access_key_id>
export ALIBABA_CLOUD_ACCESS_KEY_SECRET=<access_key_secret>
```

- **Windows系统** 配置方法

1. 新建环境变量文件，添加环境变量 **ALIBABA\_CLOUD\_ACCESS\_KEY\_ID** 和 **ALIBABA\_CLOUD\_ACCESS\_KEY\_SECRET**，并写入已准备好的AccessKey ID和AccessKey Secret。

2. 重启Windows系统生效。

## 准备工作

**登录控制台创建应用**

- 手动在控制台根据实际业务需要创建对应表结构及其它相关配置，例如：索引，属性，数据源，过滤条件等。

- 下载此处我们提供的测试 [标准版应用结构模板](https://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/52287/cn_zh/1492597569202/app_schema_demo%E6%A0%B7%E4%BE%8B%E4%BB%A3%E7%A0%81demo%E6%A0%87%E5%87%86%E7%89%88%E5%BA%94%E7%94%A8%E7%BB%93%E6%9E%84.txt)，在创建应用结构时，选择“通过模板创建应用结构”，然后下一步，再选择左上角的“导入模板”，上传此处下载的应用结构模板，一直下一步直到完成。【此应用结构测试模板，可适用于标准版Php SDK文档中的搜索及推送数据Demo代码】


**下载php SDK并添加到项目中**

在左侧栏“相关下载”页面中下载v3版 php SDK包，并根据需编写具体功能需要，添加如下头文件内容到项目中，具体参考Demo中各功能实现的代码样例

**主要功能头文件集合<参考>**

主要功能包含，查询应用信息，查询应用文档，推送文档，下拉提示等，依赖的头文件，引用对应功能的头文件后就可以编写对应功能及对象方法调用。

```php
<?php
//Config 页面，头文件，包含AK，host，应用名，下拉名称及 options 等信息
require_once("../OpenSearch/Autoloader/Autoloader.php");
use OpenSearch\Client\OpenSearchClient;

//获取应用列表，头文件
require_once("Config.inc.php");
use OpenSearch\Client\AppClient;
use OpenSearch\Generated\Common\Pageable;

//查询文档，头文件
require_once("Config.inc.php");
use OpenSearch\Client\SearchClient;
use OpenSearch\Util\SearchParamsBuilder;

//推送文档，头文件
require_once("Config.inc.php");
use OpenSearch\Client\DocumentClient;

//下拉提示，头文件
require_once("Config.inc.php");
use OpenSearch\Client\SuggestClient;
use OpenSearch\Util\SuggestParamsBuilder;
```

## 主要功能client集合<参考>

我们先实例化一个SDK客户端client，在编写对应功能时会使用到它。

```php
<?php
//引用配置头文件
require_once("Config.inc.php");

//创建用于获取应用列表client
$appClient = new AppClient($client);

//创建用于查询文档client
require_once("Config.inc.php");
$searchClient = new SearchClient($client);

//创建用于推送文档client
require_once("Config.inc.php");
$documentClient = new DocumentClient($client);

//创建用于下拉查询client
require_once("Config.inc.php");
$suggestClient = new SuggestClient($client);
```

**创建Config配置头文件**

Config 页面中的内容将作为后续的查询推送文档的头文件，其中包含AK，host，应用名，下拉名称及 options 选项，等重要参数信息

```php
<?php
//引入头文件
require_once("../OpenSearch/Autoloader/Autoloader.php");
use OpenSearch\Client\OpenSearchClient;

// 用户识别信息
// 从环境变量读取配置的AccessKey ID和AccessKey Secret，
// 运行代码示例前必须先配置环境变量，参考文档上面“配置环境变量”步骤
// 替换对应的access key id
$accessKeyId = getenv('ALIBABA_CLOUD_ACCESS_KEY_ID');
//替换对应的access secret
$secret = getenv('ALIBABA_CLOUD_ACCESS_KEY_SECRET');
//替换为对应区域api访问地址，可参考应用控制台,基本信息中api地址
$endPoint = '<region endPoint>';
//替换为应用名
$appName = '<app name>';
//替换为下拉提示名称
$suggestName = '<suggest name>';
//开启调试模式
$options = array('debug' => true);
//创建OpenSearchClient客户端对象
$client = new OpenSearchClient($accessKeyId, $secret, $endPoint, $options);
```

## 上传文档格式

在上面代码的基础上我们继续使用DocumentClient类对象向刚创建的应用中上传一些文档，应用名称继续使用上面config页面中的$appName。OpenSearch应用中的文档是一个JSON类型的字符串，结构如下：

**说明**

此处的应用文档格式，在应用控制台中的，上传文件按钮，参考样例数据，可以下载对应的完整文档数据格式，可直接通过上传此处，下载的文件到应用中进行搜索。

```json
[\
    {\
        "fields":{},\
        "cmd":""\
    }\
...\
]
```

cmd字段可选的值为：ADD、DELETE、UPDATE（

标准版应用，不支持UPDATE，新增和更新都通过ADD实现，也不支持部分字段更新

），分别表示添加、删除以及更新一条文档；

fields字段内包含文档本身的字段属性，比如在一个小说应用的结构中可能包含以下字段：title：小说的名字，body：小说主体内容，url：访问小说的地址等。

**完整示例代码**

可以下载V3 版PhpSDK，并解压到下面代码文件的同级目录中，然后直接复制下面代码，将其中的access key和secret替换成自己的，以及替换其它关键信息，就可以体验一下OpenSearch了。

```php
<?php
header("Content-Type:text/html;charset=utf-8");
//引用头部文件
require_once("Config.inc.php");
use OpenSearch\Client\DocumentClient;
use OpenSearch\Client\SearchClient;
use OpenSearch\Util\SearchParamsBuilder;

//设置数据需推送到表名
$tableName = '替换为应用表名';
//创建文档操作client
$documentClient = new DocumentClient($client);
//添加文档数据
$docs_to_upload = array();
for ($i = 0; $i < 10; $i++){
    $item = array();
    $item['cmd'] = 'ADD';
    $item["fields"] = array(
        "id" => $i + 1,
        "name" => "搜索".$i
        );
    $docs_to_upload[] = $item;
}
// 编码
$json = json_encode($docs_to_upload);
//提交推送文档
$ret = $documentClient->push($json, $appName, $tableName);

// 实例化一个搜索类
$searchClient = new SearchClient($client);
// 实例化一个搜索参数类
$params = new SearchParamsBuilder();
//设置config子句的start值
$params->setStart(0);
//设置config子句的hit值
$params->setHits(20);
// 指定一个应用用于搜索
$params->setAppName('替换为应用名');
// 指定搜索关键词
$params->setQuery("name:'搜索'");
// 指定返回的搜索结果的格式为json
$params->setFormat("fulljson");
//添加排序字段
$params->addSort('RANK', SearchParamsBuilder::SORT_DECREASE);
// 执行搜索，获取搜索结果
$ret = $searchClient->execute($params->build());
// 将json类型字符串解码
print_r(json_decode($ret->result,true));
//打印调试信息
echo $ret->traceInfo->tracer;
```

## 调试

通过上面的操作我们已经可以使用基本的搜索功能了，但是优化搜索、提高搜索结果相关性是一个漫长的过程，需要我们不断试错和迭代来一点点改进。在这个过程中如果遇到问题或者发现结果与预期不一致时可以通过下面的接口获得请求的详细信息，可以通过这些信息排查问题。特别是当遇您到问题，在旺旺群、钉钉群中寻求帮助的时候，根据调试信息我们可以迅速帮您定位到问题所在。

```php
echo $ret->traceInfo->tracer;
```