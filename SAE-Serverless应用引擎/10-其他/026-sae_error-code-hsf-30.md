## 报错信息

调用HSF服务时，报错信息如下。


```nginx
There is no TOP transformer for Service:[${serviceUniqueName}].
```

## 解决方案

TOP调用方式是为了避免网关应用依赖后端服务的API包，TOP调用在服务端进行转换时，没有找到对应的`transformer`。


### 客户端设置

客户端使用`com.taobao.hsf.app.spring.util.SuperHSFSpringConsumerBeanTop`，该类无需服务端的接口包。通过`com.taobao.hsf.app.spring.util.SuperHSFSpringConsumerBeanTop#invoke`发起调用。


示例代码如下。

```markdown
/**
 * TOP调用该方法来访问远程HSF服务。
 * <p>
 * 这里需要注意的是parameterTypes参数，该参数表示要调用的方法的参数类型。 必须是完整的Java类名，而且如果参数是原子类型，这里的类型就是原子类型的名称。
 * </p>
 *
 * @return 对端业务响应或业务异常
 *
 * @throws HSFException
 *             如果本侧或对端HSF层出现错误，则抛出HSFException
 * @throws Throwable
 *             如果服务端业务出现异常，则抛出Exception
 */
public Object invoke(String methodName, String[] parameterTypes, Object[] args) throws HSFException, Throwable {
    return consumerBeanTop.invoke(methodName, parameterTypes, args);
}

```

代码中的`args`不是真正的服务端业务类型。


### 服务端

服务端初始化时，需要通过`com.taobao.hsf.ServiceInvokeTransform.Helper#register`注册一个`transformer`。


示例代码如下。


```typescript
/**
 * 用于把服务的调用参数转换成服务可以接受的形式。
 *
 * @param methodName
 *            要调用的服务方法名
 * @param args
 *            转换前的调用参数
 * @param parameterTypes
 *            要调用的服务方法的真实参数类型
 */
abstract public Object[] transformRequest(String methodName, Object[] args, String[] parameterTypes)
        throws Exception;

/**
 * 转换请求参数类型
 *
 * @param methodName
 * @param args
 * @param parameterTypes
 * @return
 * @throws Exception
 */
abstract public String[] transformRequestTypes(String methodName, Object[] args, String[] parameterTypes)
        throws Exception;

```

该`transformer`服务在服务端将客户端传递的参数转化为真实的业务类型，HSF使用转化后的参数进行业务调用，然后使用 `transformer`将业务结果进行转化后返回给TOP客户端。


### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 错误编码：HSF-0029

# 错误编码：HSF-0029

更新时间：2022-11-17 01:51:11

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/aliware/sae)

[我的收藏](https://help.aliyun.com/my_favorites.html)

上一篇：无[下一篇：什么是Serverless应用引擎？](https://help.aliyun.com/zh/sae/product-overview/what-is-serverless-app-engine)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

报错信息

解决方案

客户端设置

服务端