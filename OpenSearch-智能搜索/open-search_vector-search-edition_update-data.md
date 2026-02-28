### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [智能开放搜索 OpenSearch](https://help.aliyun.com/zh/open-search/)[OpenSearch-向量检索版](https://help.aliyun.com/zh/open-search/vector-search-edition/)[开发指南](https://help.aliyun.com/zh/open-search/vector-search-edition/development-guide/)[SDK 参考](https://help.aliyun.com/zh/open-search/vector-search-edition/sdk-example/)更新数据

# 更新数据

更新时间：2025-09-11 22:36:41

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/opensearch)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：版本说明](https://help.aliyun.com/zh/open-search/vector-search-edition/version-description-test)[下一篇：查询数据](https://help.aliyun.com/zh/open-search/vector-search-edition/query-vector-data)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

相关依赖

参数说明

数据更新demo

add 操作示例

delete 操作示例

说明

本文档介绍如何使用Java、Python语言进行更新表数据，支持的更新操作有add、delete。

## 相关依赖

Java

python

Go

Java异步

```java
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-sdk-ha3engine-vector</artifactId>
    <version>1.1.17</version>
</dependency>
```

```python
# Requires: Python >=3.6
pip install alibabacloud_ha3engine_vector==1.1.17
```

```go
go get github.com/aliyun/alibabacloud-ha3-go-sdk@v1.1.17-vector
```

```java
<dependency>
  <groupId>com.aliyun</groupId>
  <artifactId>aliyun-sdk-ha3engine-async</artifactId>
  <version>1.1.7</version>
</dependency>
```

## **参数说明**

Java、Python SDK中都需要配置如下5个必要参数（endpoint **、** instance\_id、access\_user\_name、access\_pass\_word、data\_source\_name）：

- endpoint：私网/公网域名


可在实例详情页中网络信息和API入口查看：

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7694904961/p717834.png)

**重要**

开启公网访问后可以在本地通过 **公网域名（包含public的域名）** 调用实例，需要参考 [添加白名单](https://help.aliyun.com/zh/open-search/vector-search-edition/instance-detail#c36f65c1296n9 "") 配置访问的白名单IP，否则会报禁止访问的错误，建议您使用前先ping下，确定可访问。

若有ECS机器，可通过配置相同的交换机通过 **API域名** 调用实例。

- instance\_id：实例ID

- access\_user\_name：用户名

- access\_pass\_word：密码


用户名和密码可以在实例详情页中API入口处进行查看：（密码是购买实例时设置的，可以修改）

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/7694904961/p717836.png)

- data\_source\_name：API推送数据的数据源名称，默认为实例id\_表名：


![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/8055904961/p717837.png)

如上图所示，data\_source\_name=ha-cn-zpr3dgzxg04\_test\_image\_vector

## **数据更新demo**

### **add 操作示例**

Java

Python

Go

Java异步

```java
import com.aliyun.ha3engine.vector.Client;
import com.aliyun.ha3engine.vector.models.Config;
import com.aliyun.ha3engine.vector.models.PushDocumentsRequest;
import com.aliyun.ha3engine.vector.models.PushDocumentsResponse;
import com.aliyun.tea.TeaException;
import org.junit.Before;
import org.junit.Test;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

/**
 * @author alibaba
 */
public class PushDoc {

    /**
     * 问天引擎client
     */
    private Client client;

    @Before
    public void clientInit() throws Exception {
        /*
          初始化问天引擎client
         */
        Config config = new Config();
        // 实例名称，可在实例详情页左上角查看，例:ha-cn-i7*****605
        config.setInstanceId("ha-cn-i7*****605");
        // 用户名，可在实例详情页>API入口 查看
        config.setAccessUserName("username");
        // 密码，可在实例详情页>API入口 修改
        config.setAccessPassWord("password");
        // API域名，可在实例详情页>API入口 查看
        config.setEndpoint("ha-cn-i7*****605.public.ha.aliyuncs.com");
        client = new Client(config);
    }

    @Test
    public void add() throws Exception {
        // 文档推送的表名称，是实例id与表名的拼接，中间用下划线连接
        String tableName = "<instance_id>_<table_name>";

        // 文档推送的文档主键字段.
        String pkField = "<field_pk>";

        try {
            // 文档推送外层结构, 可添加对文档操作的结构体. 结构内支持一个或多个文档操作内容.
            ArrayList<Map<String, ?>> documents = new ArrayList<>();

            // 添加文档
            Map<String, Object> add2Document = new HashMap<>();
            Map<String, Object> add2DocumentFields = new HashMap<>();

            // 插入文档内容信息, keyValue 成对匹配.
            // field_pk 字段需与 pkField 字段配置一致.
            add2DocumentFields.put("<field_pk>", "<field_pk_value>");
            add2DocumentFields.put("<field_map_key_1>", "<field_map_value_1>");
            add2DocumentFields.put("<field_map_key_2>", "<field_map_value_2>");

            // 问天引擎支持的多值属性类型,索引内配置为"multi_value": true
            ArrayList<Object> addDocumentMultiFields = new ArrayList<>();
            addDocumentMultiFields.add("multi_value_1");
            addDocumentMultiFields.add("multi_value_2");
            add2DocumentFields.put("<multi_value_key>", addDocumentMultiFields);

            // 将文档内容添如 add2Document 结构.
            add2Document.put("fields", add2DocumentFields);
            // 新增对应的文档命令: add
            add2Document.put("cmd", "add");
            documents.add(add2Document);

            // 推送数据
            PushDocumentsRequest request = new PushDocumentsRequest();
            // 推送数据时，默认校验是否存在主键字段。如需关闭校验，请设置请求头 X-Opensearch-Validate-Data: false
//            request.headers = new HashMap<>();
//            request.headers.put("X-Opensearch-Validate-Data", "false");
            request.setBody(documents);
            PushDocumentsResponse response = client.pushDocuments(tableName, pkField, request);
            String responseBody = response.getBody();

            System.out.println("result：" + responseBody);
        } catch (TeaException e) {
            System.out.println(e.getCode());
            System.out.println(e.getMessage());
            Map<String, Object> exceptionData = e.getData();
            System.out.println(com.aliyun.teautil.Common.toJSONString(exceptionData));
        }
    }
}
```

```python
from alibabacloud_ha3engine_vector.client import Client
from alibabacloud_ha3engine_vector.models import Config
from alibabacloud_ha3engine_vector import models
from Tea.exceptions import TeaException, RetryError

config = Config(
    # API域名，可在实例详情页>API入口 查看
    endpoint="http://ha-cn-i7*****605.public.ha.aliyuncs.com",
    # 用户名，可在实例详情页>API入口 查看
    access_user_name="username",
    # 密码，可在实例详情页>API入口 修改
    access_pass_word="password")

# 初始化 引擎客户端
client = Client(config)

def push():
    # 文档推送的表名称，是实例id与表名的拼接，中间用下划线连接
    tableName = "<instance_id>_<table_name>";

    try:
        # 添加文档
        # 添加一篇文档，如果文档已经存在会先删除然后再添加。
        # =====================================================
        # 更新文档内容信息
        add2DocumentFields = {
            "id": 1,                          # 主键id，INT单值类型
            "name": "搜索",                    # STRING单值类型
            "str_arr": "a\x1Db\x1Dc\x1Dd"     # STRING多值类型
        }

        # 将文档内容添入 add2Document结构
        add2Document = {
            "fields": add2DocumentFields,
            "cmd": "add"                      # 新增对应的文档命令: add
        }

        optionsHeaders = {}
        # 文档推送外层结构, 可添加对文档操作的结构体.结构内支持 一个或多个文档操作内容.
        documentArrayList = []
        documentArrayList.append(add2Document)
        pushDocumentsRequest = models.PushDocumentsRequest(optionsHeaders, documentArrayList)
        # 推送数据时，默认校验是否存在主键字段。如需关闭校验，请设置请求头 X - Opensearch - Validate - Data: false
        # pushDocumentsRequest.headers = {"X-Opensearch-Validate-Data": "false"}

        # 文档推送的文档主键字段.
        pkField = "id"
        # 使用默认 运行时参数进行请求
        response = client.push_documents(tableName, pkField, pushDocumentsRequest)
        print(response.body)

    except TeaException as e:
        print(f"send request with TeaException : {e}")
    except RetryError as e:
        print(f"send request with Connection Exception  : {e}")

if __name__ == "__main__":
    push()
```

主要是在程序中动态将对应的文档数据封装到Map对象中，然后通过add方法将这些Map对象添加到缓存中，最后调用pushDocuments方法，批量提交这些Map对象的文档数据。

```go
package main

import (
	"fmt"
	"github.com/alibabacloud-go/tea/tea"
	ha3engine "github.com/aliyun/alibabacloud-ha3-go-sdk/client"
)

func main() {
	// 创建请求客户端实例
	config := &ha3engine.Config{
		// API域名，可在实例详情页>API入口 查看
		Endpoint: tea.String("ha-cn-i7*****605.public.ha.aliyuncs.com"),
		// 用户名，可在实例详情页>API入口 查看
		AccessUserName: tea.String("username"),
		// 密码，可在实例详情页>API入口 修改
		AccessPassWord: tea.String("password"),
	}

	// 初始化一个client, 用以发送请求.
	client, _clientErr := ha3engine.NewClient(config)

	// 如果 NewClient 过程中出现异常. 则 返回 _clientErr 且输出 错误信息.
	if _clientErr != nil {
		fmt.Println(_clientErr)
		return
	}
	docPush(client)
}

func docPush(client *ha3engine.Client) {
	pushDocumentsRequestModel := &ha3engine.PushDocumentsRequest{}
	// 文档推送的表名称，是实例id与表名的拼接，中间用下划线连接
	tableName := "<instance_id>_<table_name>"
	// 文档推送的文档主键字段
	keyField := "<field_pk>"

	// 向量字段
	vector := [4]float32{1.2, 2.2, 3.2, 4.2}
	filed := map[string]interface{}{
		"fields": map[string]interface{}{
			"id":     1,
			"name":   "测试",
			"vector": vector,
		},
		"cmd": tea.String("add"),
	}
	array := []map[string]interface{}{}
	array = append(array, filed)

	pushDocumentsRequestModel.SetBody(array)

    // 推送数据时，默认校验是否存在主键字段。如需关闭校验，请设置请求头 X-Opensearch-Validate-Data: false
	//headers := map[string]*string{}
	//headers["X-Opensearch-Validate-Data"] = tea.String("false")
	//pushDocumentsRequestModel.SetHeaders(headers)

	// 发送请求的方法调用.
	response, _requestErr := client.PushDocuments(tea.String(tableName), tea.String(keyField), pushDocumentsRequestModel)

	// 如果 发送请求 过程中出现异常. 则 返回 _requestErr 且输出 错误信息.
	if _requestErr != nil {
		fmt.Println(_requestErr)
		return
	}

	// 输出正常返回的 response 内容.
	fmt.Println(response)
}
```

主要是在程序中动态将对应的文档数据封装到Map对象中，再将这些Map对象通过add方法添加到缓存中，最后调用pushDocuments方法，批量提交这些Map对象文档数据。

```java
import com.aliyun.ha3engine.async.AsyncClient;
import com.aliyun.ha3engine.async.models.PushDocumentsRequest;
import com.aliyun.ha3engine.async.models.PushDocumentsResponse;
import com.aliyun.sdk.ha3engine.async.core.AsyncConfigInfoProvider;
import com.aliyun.tea.TeaException;
import darabonba.core.client.ClientOverrideConfiguration;
import org.junit.Before;
import org.junit.Test;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

/**
 * @author alibaba
 */
public class AddDoc {

    /**
     * 问天引擎client
     */
    private AsyncClient client;

    @Before
    public void clientInit() {
        // 配置实例的用户名密码, 可在实例详情页>API入口 查看
        AsyncConfigInfoProvider provider = AsyncConfigInfoProvider.create("username", "password");
        // 初始化异步客户端
        client = AsyncClient.builder()
                .credentialsProvider(provider)
                .overrideConfiguration(
                        ClientOverrideConfiguration.create()
                                .setEndpointOverride("ha-cn-i7*****605.public.ha.aliyuncs.com")
                                .setProtocol("http")
                ).build();
    }

    @Test
    public void add() {
        try {
            // 文档推送的表名称
            String tableName = "<table_name>";

            // 文档推送的文档主键字段.
            String pkField = "<field_pk>";

            // 文档推送外层结构, 可添加对文档操作的结构体. 结构内支持一个或多个文档操作内容.
            ArrayList<Map<String, ?>> documents = new ArrayList<>();

            // 添加文档
            Map<String, Object> add2Document = new HashMap<>();
            Map<String, Object> add2DocumentFields = new HashMap<>();

            // 更新文档内容信息, keyValue 成对匹配.
            // field_pk 字段需与 pkField 字段配置一致.
            add2DocumentFields.put("<field_pk>", "<field_pk_value>");
            add2DocumentFields.put("<field_map_key_1>", "<field_map_value_1>");
            add2DocumentFields.put("<field_map_key_2>", "<field_map_value_2>");

            // 问天引擎支持的多值属性类型,索引内配置为"multi_value": true
            ArrayList<Object> addDocumentMultiFields = new ArrayList<>();
            addDocumentMultiFields.add("multi_value_1");
            addDocumentMultiFields.add("multi_value_2");
            add2DocumentFields.put("<multi_value_key>", addDocumentMultiFields);

            // 将文档内容添如 add2Document 结构.
            add2Document.put("fields", add2DocumentFields);
            // 新增对应的文档命令: add
            add2Document.put("cmd", "add");
            documents.add(add2Document);

            // 推送数据
            PushDocumentsRequest request = PushDocumentsRequest.builder().body(documents).build();
            // 推送数据时，默认校验是否存在主键字段。如需关闭校验，请设置请求头 X-Opensearch-Validate-Data: false
//            request.getHeaderParameters().put("X-Opensearch-Validate-Data", "false");
            CompletableFuture<PushDocumentsResponse> responseCompletableFuture = client.pushDocuments(tableName, pkField, request);
            String responseBody = responseCompletableFuture.get().getBody();

            System.out.println("result：" + responseBody);
        } catch (ExecutionException | InterruptedException e) {
            System.out.println(e.getMessage());
        } catch (TeaException e) {
            System.out.println(e.getCode());
            System.out.println(e.getMessage());
            Map<String, Object> exceptionData = e.getData();
            System.out.println(com.aliyun.teautil.Common.toJSONString(exceptionData));
        }
    }
}
```

**说明**

通过add推送数据时，主键相同新数据会覆盖旧数据

### **delete 操作示例**

Java

Python

Go

Java异步

```java
import com.aliyun.ha3engine.vector.Client;
import com.aliyun.ha3engine.vector.models.*;
import com.aliyun.tea.TeaException;
import org.junit.Before;
import org.junit.Test;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;

/**
 * @author alibaba
 */
public class PushDoc {

    /**
     * 问天引擎client
     */
    private Client client;

    @Before
    public void clientInit() throws Exception {
        /*
          初始化问天引擎client
         */
        Config config = new Config();

        // 实例名称，可在实例详情页左上角查看，例:ha-cn-i7*****605
        config.setInstanceId("ha-cn-i7*****605");
        // 用户名，可在实例详情页>网络信息 查看
        config.setAccessUserName("username");
        // 密码，可在实例详情页>网络信息 修改
        config.setAccessPassWord("password");
        // API域名，可在实例详情页>API入口 查看
        config.setEndpoint("ha-cn-i7*****605.public.ha.aliyuncs.com");

        client = new Client(config);
    }

    @Test
    public void delete() throws Exception {
        // 文档推送的表名称，是实例id与表名的拼接，中间用下划线连接
        String tableName = "<instance_id>_<table_name>";

        // 文档推送的文档主键字段.
        String pkField = "<field_pk>";

        try {
            // 文档推送外层结构, 可添加对文档操作的结构体. 结构内支持一个或多个文档操作内容.
            ArrayList<Map<String, ?>> documents = new ArrayList<>();

            // 删除文档
            Map<String, Object> delete2Document = new HashMap<>();
            Map<String, Object> delete2DocumentFields = new HashMap<>();

            // 插入文档内容信息, keyValue 成对匹配.
            // field_pk 字段需与 pkField 字段配置一致.
            delete2DocumentFields.put("<field_pk>", "<field_pk_value>");

            // 将文档内容添如 delete2Document 结构.
            delete2Document.put("fields", delete2DocumentFields);
            // 删除对应的文档命令: delete
            delete2Document.put("cmd", "delete");
            documents.add(delete2Document);

            // 推送数据
            PushDocumentsRequest request = new PushDocumentsRequest();
            request.setBody(documents);
            PushDocumentsResponse response = client.pushDocuments(tableName, pkField, request);
            String responseBody = response.getBody();

            System.out.println("result：" + responseBody);

        } catch (TeaException e) {
            System.out.println(e.getCode());
            System.out.println(e.getMessage());
            Map<String, Object> exceptionData = e.getData();
            System.out.println(com.aliyun.teautil.Common.toJSONString(exceptionData));
        }
    }
}
```

```python
from alibabacloud_ha3engine_vector.client import Client
from alibabacloud_ha3engine_vector.models import Config
from alibabacloud_ha3engine_vector import models
from Tea.exceptions import TeaException, RetryError

config = Config(
    # API域名，可在实例详情页>API入口 查看
    endpoint="http://ha-cn-i7*****605.public.ha.aliyuncs.com",
    # 用户名，可在实例详情页>API入口 查看
    access_user_name="username",
    # 密码，可在实例详情页>API入口 修改
    access_pass_word="password")

# 初始化 引擎客户端
ha3EngineClient = Client(Config)

def pushDoc():
    # 文档推送的表名称，是实例id与表名的拼接，中间用下划线连接
    tableName = "<instance_id>_<table_name>";

    try:
        # 文档推送外层结构, 可添加对文档操作的结构体.结构内支持 一个或多个文档操作内容.
        documentArrayList = []

        # 删除文档
        # 删除一篇文档，删除文档时需要指定文档主键
        # 如果索引构建时采用多级hash方式，需要指定每级hash的主键。
        delete2DocumentFields = {
            "id": 1  # 主键id，INT单值类型
        }
        delete2Document = {
            "fields": delete2DocumentFields,  # 将文档内容添如 delete2Document 结构.
            "cmd": "delete"  # 删除对应的文档命令: delete
        }

        optionsHeaders = {}
        documentArrayList.append(delete2Document)
        pushDocumentsRequest = models.PushDocumentsRequest(
            optionsHeaders, documentArrayList
        )

        # 文档推送的文档主键字段.
        pkField = "id"
        # 使用默认 运行时参数进行请求
        response = ha3EngineClient.push_documents(
            tableName, pkField, pushDocumentsRequest
        )
        print(response)

    except TeaException as e:
        print(f"send request with TeaException : {e}")
    except RetryError as e:
        print(f"send request with Connection Exception  : {e}")

if __name__ == "__main__":
    pushDoc()
```

```go
package main

import (
    "fmt"
    "github.com/alibabacloud-go/tea/tea"
    ha3engine "github.com/aliyun/alibabacloud-ha3-go-sdk/client"
)

func main() {
    // 创建请求客户端实例
    config := &ha3engine.Config{
        // API域名，可在实例详情页>API入口 查看
        Endpoint: tea.String("ha-cn-i7*****605.public.ha.aliyuncs.com"),
        // 用户名，可在实例详情页>API入口 查看
        AccessUserName: tea.String("username"),
        // 密码，可在实例详情页>API入口 修改
        AccessPassWord: tea.String("password"),
    }

    // 初始化一个client, 用以发送请求.
    client, _clientErr := ha3engine.NewClient(config)

    // 如果 NewClient 过程中出现异常. 则 返回 _clientErr 且输出 错误信息.
    if _clientErr != nil {
        fmt.Println(_clientErr)
        return
    }
    deleteDoc(client)
}

func deleteDoc(client *ha3engine.Client) {
    pushDocumentsRequestModel := &ha3engine.PushDocumentsRequest{}
    // 文档推送的表名称，是实例id与表名的拼接，中间用下划线连接
    tableName := "<instance_id>_<table_name>"
    // 文档推送的文档主键字段
    keyField := "<field_pk>"

    var array []map[string]interface{}
    filed := map[string]interface{}{
        "fields": map[string]interface{}{
            "id": 2,
        },
        "cmd": tea.String("delete"),
    }
    array = append(array, filed)

    pushDocumentsRequestModel.SetBody(array)

    // 发送请求的方法调用.
    response, _requestErr := client.PushDocuments(tea.String(tableName), tea.String(keyField), pushDocumentsRequestModel)

    // 如果 发送请求 过程中出现异常. 则 返回 _requestErr 且输出 错误信息.
    if _requestErr != nil {
        fmt.Println(_requestErr)
        return
    }

    // 输出正常返回的 response 内容.
    fmt.Println(response)
}
```

```java
import com.aliyun.ha3engine.async.AsyncClient;
import com.aliyun.ha3engine.async.models.PushDocumentsRequest;
import com.aliyun.ha3engine.async.models.PushDocumentsResponse;
import com.aliyun.sdk.ha3engine.async.core.AsyncConfigInfoProvider;
import com.aliyun.tea.TeaException;
import darabonba.core.client.ClientOverrideConfiguration;
import org.junit.Before;
import org.junit.Test;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

/**
 * @author alibaba
 */
public class DeleteDoc {

    /**
     * 问天引擎client
     */
    private AsyncClient client;

    @Before
    public void clientInit() {
        // 配置实例的用户名密码, 可在实例详情页>API入口 查看
        AsyncConfigInfoProvider provider = AsyncConfigInfoProvider.create("username", "password");
        // 初始化异步客户端
        client = AsyncClient.builder()
                .credentialsProvider(provider)
                .overrideConfiguration(
                        ClientOverrideConfiguration.create()
                                .setEndpointOverride("ha-cn-i7*****605.public.ha.aliyuncs.com")
                                .setProtocol("http")
                ).build();
    }

    @Test
    public void delete() throws Exception {
        try {
            // 文档推送的表名称，是实例id与表名的拼接，中间用下划线连接
            String tableName = "<instance_id>_<table_name>";

            // 文档推送的文档主键字段
            String pkField = "<field_pk>";

            // 文档推送外层结构, 可添加对文档操作的结构体. 结构内支持一个或多个文档操作内容.
            ArrayList<Map<String, ?>> documents = new ArrayList<>();

            // 删除文档
            Map<String, Object> deleteDocument = new HashMap<>();
            Map<String, Object> deleteDocumentFields = new HashMap<>();

            // 更新文档内容信息, keyValue 成对匹配.
            // field_pk 字段需与 pkField 字段配置一致.
            deleteDocumentFields.put("<field_pk>", "<field_pk_value>");

            // 将文档内容添如 deleteDocument 结构.
            deleteDocument.put("fields", deleteDocumentFields);
            // 删除对应的文档命令: delete
            deleteDocument.put("cmd", "delete");
            documents.add(deleteDocument);

            // 推送数据
            PushDocumentsRequest request = PushDocumentsRequest.builder().body(documents).build();
            CompletableFuture<PushDocumentsResponse> responseCompletableFuture = client.pushDocuments(tableName, pkField, request);
            String responseBody = responseCompletableFuture.get().getBody();

            System.out.println("result：" + responseBody);
        } catch (ExecutionException | InterruptedException e) {
            System.out.println(e.getMessage());
        } catch (TeaException e) {
            System.out.println(e.getCode());
            System.out.println(e.getMessage());
            Map<String, Object> exceptionData = e.getData();
            System.out.println(com.aliyun.teautil.Common.toJSONString(exceptionData));
        }
    }
}
```

## **说明**

- 请求的相应结果可参考流量API说明>更新数据中的 [相应结果](https://help.aliyun.com/zh/open-search/vector-search-edition/vector-update-data-api "")

- 不要使用`go get github.com/aliyun/alibabacloud-ha3-go-sdk`命令拉取Git依赖，必须后面指定版本，因为向量检索版和召回引擎版的tag都在同一个github下，拉取依赖的时候需根据实例的版本拉取对应依赖