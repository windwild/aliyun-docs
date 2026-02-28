### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[刷新和预热](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch/)刷新和预热相关常见问题

# 刷新和预热相关常见问题

更新时间：2024-09-12 02:55:50

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：使用自动化脚本刷新和预热](https://help.aliyun.com/zh/cdn/user-guide/run-scripts-to-refresh-and-prefetch-content)[下一篇：检测IP地址是否属于阿里云CDN节点](https://help.aliyun.com/zh/cdn/user-guide/does-the-ip-belong-to-cdn-pops)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

刷新和预热有什么区别？

刷新和预热有先后顺序吗？

刷新预热时，输入源站URL还是加速域名URL？

如何刷新泛域名的缓存？

刷新和预热任务需要多久生效？

预热时能携带自定义请求头预热吗？

如何提高刷新和预热的每日配额上限？

是否支持自动化刷新或预热？

如何查看CDN的预热任务是否执行完成？

配置CDN后如何对文件进行同名更新？

预热失败了怎么办？

为什么使用CDN刷新预热功能后访问的资源没有更新？

是否需要分别对HTTP和HTTPS刷新和预热？

是否支持预热M3U8文件？

已经进行了缓存预热，为什么下载速度先快后慢？

本文为您介绍CDN刷新和预热相关的常见问题。

- [刷新和预热有什么区别？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#812aa31b828jf "")

- [刷新和预热有先后顺序吗？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#61c5407fabg7w "")

- [刷新预热时，输入源站URL还是加速域名URL？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#1bd5cff5df4z6 "")

- [如何刷新泛域名的缓存？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#e6306304a0sw8 "")

- [刷新和预热任务需要多久生效？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#043dcacfa0cld "")

- [预热时能携带自定义请求头预热吗？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#264b8787a2hsc "")

- [如何提高刷新和预热的每日配额上限？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#9cec05669dcp1 "")

- [是否支持自动化刷新或预热？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#6bf2f69e6533b "")

- [如何查看CDN的预热任务是否执行完成？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#6237a4ce5ei5l "")

- [配置CDN后如何对文件进行同名更新？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#e1c2548dbejfv "")

- [预热失败了怎么办？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#4c57c3db57g4h "")

- [为什么使用CDN刷新预热功能后访问的资源没有更新？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#4566e64996ci4 "")

- [是否需要分别对HTTP和HTTPS刷新和预热？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#1b04609d80qj1 "")

- [是否支持预热M3U8文件？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#366677200b1ab "")

- [已经进行了缓存预热，为什么下载速度先快后慢？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#7f83d64b4frsq "")


## **刷新和预热有什么区别？**

- 刷新：把CDN所有节点上对应的缓存资源标记为失效，当用户再次请求时，CDN会直接回源站获取对应的资源并返回给用户，同时将资源重新缓存到CDN节点。刷新功能会降低缓存命中率。

- 预热：源站主动将对应的资源缓存到CDN节点，当您首次请求资源时，即可直接从CDN节点获取到最新的资源，无需再回源站获取。预热功能会提高缓存命中率。


## **刷新和预热有先后顺序吗？**

刷新和预热通常是两种不同的操作，并不一定有严格的先后顺序。但在实际应用中，根据场景可能会有一个自然的逻辑顺序。当您的源站资源更新，需要更新CDN节点缓存时：

1. 先刷新：删除CDN缓存中的旧文件，让后续的访问都能获取到源站上最新的内容。

2. 后预热：待刷新任务生效后再进行预热操作，将最新的内容缓存到CDN节点，保证用户第一时间获取到速度最快的服务。

3. 如果您首次接入CDN，节点无缓存，可以直接执行预热操作，将资源缓存到CDN节点。


## **刷新预热时，输入源站URL还是加速域名URL？**

刷新预热是对加速域名对应的URL内容进行操作，所以，您需要输入的是基于加速域名下的URL，而不是源站的原始URL。这样做的原因是CDN系统通过加速域名来识别和管理缓存资源，对加速域名下指定路径的请求进行刷新或预热，可以确保CDN节点上的缓存内容得到及时更新或提前加载。

## **如何刷新泛域名的缓存？**

阿里云CDN不支持直接刷新整个泛域名下的所有缓存内容，需要对具体的子域名对应的目录或特定URL路径分别提交刷新请求，不能直接输入https://\*.example.com/file01.html或https://\*.example.com/file02/。刷新多个URL时，请按照一行一个URL进行输入。

## **刷新和预热任务需要多久生效？**

- 刷新任务从提交到生效，大约需要5~6分钟，如果文件或者目录配置的缓存过期时间少于5分钟，您无需执行刷新操作，等待文件或者目录缓存超时更新即可。

- 预热任务从提交到预热完成，实际执行时间视预热文件大小而定，大约需要5~30分钟，文件平均大小越小，预热速度越快。


## **预热时能携带自定义请求头预热吗？**

预热请求默认携带的header是`Accept-Encoding:gzip`，如果您需要预热请求携带其他header，或者实现多副本预热，那么可以使用OpenAPI接口 [PushObjectCache-预热URL](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-pushobjectcache "")，并通过设定请求参数`WithHeader`来实现自定义预热header。

## **如何提高刷新和预热的每日配额上限？**

- URL刷新和目录刷新

默认情况下，一个账号每日最多可以提交10,000条URL刷新和100条目录刷新，目录刷新包含子目录。如果您的阿里云账号的日带宽峰值大于200Mbps，您可以通过 [配额管理](https://help.aliyun.com/zh/cdn/user-guide/quota-management#concept-2086246 "") 申请提升每日配额，阿里云将根据您业务的实际需求进行评估和配置。

- 正则刷新

默认情况下，一个账号每日最多可以提交20条正则刷新，如果您的阿里云账号的日带宽峰值大于10Gbps，您可以通过[填写信息](https://page.aliyun.com/form/act2017566026/index.htm)来申请提升每日配额。

- 预热

默认情况下，一个账号每日最多可以提交1000条URL预热任务，如果您账号的日带宽峰值大于200Mbps，可通过 [配额管理](https://help.aliyun.com/zh/cdn/user-guide/quota-management#concept-2086246 "") 申请提升每日配额，阿里云将根据您业务的实际需求进行评估和配置。

每个账号的预热队列最大为100,000条URL，CDN根据URL提交的先后顺序进行预热；当预热队列中待预热的URL达到了100,000条时，CDN将会拒绝接收新的预热任务。


## **是否支持自动化刷新或预热？**

如果您需要自动化刷新或预热，请参见 [使用自动化脚本刷新和预热](https://help.aliyun.com/zh/cdn/user-guide/run-scripts-to-refresh-and-prefetch-content#topic-2404622 "")。

## **如何查看CDN的预热任务是否执行完成？**

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **刷新预热**。

3. **操作类型** 选择 **预热**，在URL框内输入URL地址，单击 **提交**。提交预热任务后，您可以在 **操作记录** 页签中查看资源预热的详细记录和进度。预热进度为100%，表示预热任务执行完成。预热数量多会影响预热进度，请您耐心等待。



**说明**





预热任务的状态为成功，表示预热任务提交成功，并不代表文件已经预热结束。

4. 执行如下命令，查看预热任务的执行状态。















```javascript
curl -I 'http://example.aliyundoc.com/test.json'
```



系统显示类似如下。
![TB1oFf2JFXXXXa9XXXXXXXXXXXX.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4121656861/p631592.png)



**说明**





   - Via的前半部分代表L2节点状态，其中的“H”表示命中，说明文件已经预热到L2节点，不需要再回源站。

   - Via的后半部分代表L1节点的状态，“M”表示L1节点上没有缓存，需要向L2节点回源。


#### **相关文档**

调用DescribeRefreshTaskById，查询刷新状态和预热状态是否在全网生效，详情请参见 [DescribeRefreshTaskById - 查询刷新预热任务-按ID](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-describerefreshtaskbyid "")。

## **配置CDN后如何对文件进行同名更新？**

使用CDN加速资源时，请参见以下方法进行文件更新：

- 建议您源站的内容不使用同名更新，而是采用版本号的方式同步。

为了能准确找到更新前和更新后的源站内容，建议您源站的内容以版本号的方式同步，即更新源站内容时采用不同的名称。例如，采用img-v1.0.jpg、img-v2.1.jpg的方式命名。

- 对于必须进行同名更新的文件，可以从控制台或是OpenAPI提交刷新请求。控制台操作请参见 [刷新和预热资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources "")，OpenAPI操作请参见 [刷新预热](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-dir-refresh-and-prefetch/ "")。使用CDN刷新预热功能后，访问的资源如没有更新，请参见 [为什么使用CDN刷新预热功能后访问的资源没有更新？](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-warm-up-related-faq#4566e64996ci4 "")


## **预热失败了怎么办？**

预热失败的可能原因是：

1. **确认URL正确性**：验证预热的URL是否正确，包括是否有拼写错误、路径错误或者文件实际不存在等问题，确认URL是否可以直接在浏览器中访问。

2. **检查源站状态**：确认源站服务器是否正常工作，没有出现过载或宕机情况，如不能正常访问也将造成预热失败。

3. **控制预热任务的数量**：如果同时提交了大量的预热任务，可能会因为系统繁忙导致一部分任务失败。预热时请尽量分批次执行，避免对源站带宽造成过大压力。

4. **检查资源可缓存性**：


   - 确认预热的资源是否允许被缓存。如果资源设置了`Cache-Control`头部为`no-cache`、`no-store`或`private`，并且CDN配置遵循源站头信息，则会导致资源无法被缓存。

   - 检查资源对应的缓存过期时间（如`Expires`或`max-age`），确保其不是0，非零值表示资源可以被缓存。


CDN缓存规则请参见 [阿里云CDN默认缓存规则及优先级](https://help.aliyun.com/zh/cdn/user-guide/configure-the-cdn-cache-expiration-time#section-qsg-cem-k22 "")。

5. 目前不支持预热目录。


## **为什么使用CDN刷新预热功能后访问的资源没有更新？**

#### **问题原因**

导致资源没有更新的常见原因有以下3种：

- 使用CDN刷新预热虽然清除了CDN缓存，但是受到浏览器缓存的影响，导致访问到旧的资源。

- 源站的资源没有更新，本身就是旧的资源。

- 刷新预热任务没有执行完毕。


#### **解决方案**

根据问题原因选择其对应的解决方法：

- 尝试清理浏览器缓存，然后刷新页面，查看资源是否更新。

- 将站点域名直接绑定源站（通过修改本地host的方式），直接访问源站，检查源站的资源是否更新。如果资源没有更新，请更新源站的资源，再使用CDN加速。

- 登录[CDN控制台](https://cdn.console.aliyun.com/)，检查刷新预热任务是否执行完毕，如果没有执行完毕，建议重新执行任务，如何执行请参见 [刷新和预热资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources "")。
![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4268814071/p631651.png)


## **是否需要分别对HTTP和HTTPS刷新和预热？**

不需要，只需要刷新或预热HTTP或HTTPS其中一种即可。例如您需要预热aaa.mp4文件，您只需预热`https://example.com/aaa.mp4`即可，不必再预热`http://example.com/aaa.mp4`。

## **是否支持预热** M3U8 **文件？**

M3U8文件是一种基于HTTP Live Streaming (HLS) 的视频流媒体播放列表格式，它由苹果公司开发。M3U8是M3U播放列表文件的扩展，其中“8”代表文件使用UTF-8字符编码。该文件格式通常用于在线流媒体服务，以提供连续播放的多媒体内容。M3U8文件是一个纯文本文件，包含了分段（通常是TS或MP4文件）视频文件的路径信息，这些分段视频文件被称为“切片”。

预热只作用于M3U8文件本身，不会自动预热列表中引用的各个TS切片文件。您可以使用脚本来预热M3U8文件，详情请参见[CDN和视频点播中使用脚本刷新预热M3U8资源](https://help.aliyun.com/document_detail/189851.html)。

## 已经进行了缓存预热，为什么下载速度先快后慢？

CDN预热是多个节点同时进行下载，开始某个节点的下载速度较快，随着更多节点的加入，下载速度受到源站服务器带宽的影响，呈现先快后慢的情况。对于带宽较小的源站服务器所需预热时间会长一点，因此，可以通过升级带宽来解决或者使用OSS来存储大文件。使用CDN对OSS资源进行加速，以获得更好的加速效果。