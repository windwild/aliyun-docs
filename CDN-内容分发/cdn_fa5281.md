### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) 如何在不修改域名解析的情况下将域名指向CDN的源站

# 如何在不修改域名解析的情况下将域名指向CDN的源站

更新时间：2022-01-12 02:36:13

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

> **免责声明：** 本文档可能包含第三方产品信息，该信息仅供参考。阿里云对第三方产品的性能、可靠性以及操作可能带来的潜在影响，不做任何暗示或其他形式的承诺。

## 概述

当您在配置阿里云CDN加速后，在访问加速资源异常时，为了确认问题是否与源站有关，通常需要绕过CDN直接访问源站，对比CDN加速与未加速的访问效果。本文介绍如何在不修改域名解析的情况下，将域名指向源站。

## 详细信息

访问CDN加速资源异常时，通过绑定源站进行测试的方法如下：

### 方法一：通过修改Hosts文件的方式

可以通过修改hosts文件的方式，在不修改域名解析的情况下，将域名指向源站。具体方法如下。

1. 编辑hosts文件。


> **说明**：在浏览器访问域名时，会优先从hosts文件去获取域名对应的IP地址。如果hosts文件内没有对应的条目，才会通过本地DNS服务器去获取域名解析指向的IP地址。

   - 在Windows系统中，该文件保存路径如下所示。
















     ```
     C:\Windows\System32\drivers\etc\hosts
     ```

   - 在Linux系统中，该文件保存路径如下所示。
















     ```
     /etc/hosts
     ```
2. 在hosts文件末尾，添加条目。本文以如下条目为例，`192.168.0.1`为源站IP地址，`example.aliyundoc.com`为待检查的域名。
















```
192.168.0.1 example.aliyundoc.com
```

3. 使用如下命令测试该域名，确认返回的IP地址为`192.168.0.1`。
















```
ping example.aliyundoc.com
```

4. 清理浏览器的缓存，并重新开启浏览器访问该网站。此时会从`192.168.0.1`这个IP地址获取数据，而不使用CDN加速功能。


> **说明**：如果浏览器提示出错，说明源站出现问题。


### 方法二：使用CURL工具HTTP/HTTPS请求源站

使用CURL工具来发起HTTP/HTTPS请求，通过指定参数绑定到源站测试。假设`192.168.0.1`为源站IP地址，`example.aliyundoc.com`为待检查的域名。

> **说明**：
>
> - 如没有CURL工具，请参考相关文档先安装CURL工具。
> - Windows请打开命令行窗口，运行`curl`命令，Mac/Linux直接在命令行工具下运行即可。

1. 源站是80端口，请执行以下命令。
















```
curl -voa "http://example.aliyundoc.com/" -x 192.168.0.1:80
```

2. 源站是443端口，请执行以下命令。
















```
curl -voa "http://example.aliyundoc.com/" --resolve example.aliyundoc.com:443:192.168.0.1
```

3. 源站是自定义端口，请执行以下命令。
















```
curl -voa "http://example.aliyundoc.com/" -x 192.168.0.1:[$Port]
```




> **说明**：\[$Port\]为自定义端口。


## 相关文档

如果源站访问正常，但CDN加速域名打开有问题，请参见 [站点接入到CDN以后参数加载不了](https://help.aliyun.com/zh/cdn/f4c898)，判断是否由URL参数引起的问题。

## 适用于

- CDN

上一篇：无[下一篇：什么是阿里云CDN](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

概述

详细信息

方法一：通过修改Hosts文件的方式

方法二：使用CURL工具HTTP/HTTPS请求源站

相关文档

适用于