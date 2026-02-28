### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[操作指南](https://help.aliyun.com/zh/cdn/user-guide/)[缓存配置](https://help.aliyun.com/zh/cdn/user-guide/cache-settings/)缓存相关常见问题

# 缓存相关常见问题

更新时间：2026-01-18 21:41:42

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：配置跨域资源共享](https://help.aliyun.com/zh/cdn/user-guide/configure-cors)[下一篇：回源概述](https://help.aliyun.com/zh/cdn/user-guide/back-to-origin-routing-overview)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

CDN缓存清理机制是什么？

CDN默认的缓存规则是什么？

如何判断CDN缓存是否成功？

如何解决URL的传递参数为变量导致CDN缓存命中率低的问题？

如何设置文件不缓存直接回源？

在CDN控制台缓存过期时间设置为0，为何访问到的资源仍然不是最新内容？

源站变更文件后，CDN节点上的缓存会主动、实时更新吗？

影响CDN缓存命中率下降的因素有哪些？

如何排查CDN缓存命中率较低的问题？

如何设置缓存全局生效？

缓存配置为什么没有生效？

通过HTTP响应头配置CDN跨域资源共享（CORS）及注意事项

为什么已经配置了响应头Access-Control-Allow-Origin，但是访问资源仍提示跨域问题，response header中没有配置的响应头？

异常状态码缓存规则是什么？

出站响应头和入站响应头有什么区别？

如何配置整个域名不缓存？

CDN是否支持多副本缓存？如何实现CDN的多副本缓存？

CDN如何配置子目录访问首页？

确认源站

配置子目录重写

本文为您介绍CDN缓存相关的常见问题。

- [CDN缓存清理机制是什么？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#a3c36fa3b3xbr "")

- [CDN默认的缓存规则是什么？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#a780fc19d9kqw "")

- [如何判断CDN缓存是否成功？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#6d3abcbd7715l "")

- [如何解决URL的传递参数为变量导致CDN缓存命中率低的问题？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#45b29f333amia "")

- [如何设置文件不缓存直接回源？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#2af4a644cf7cs "")

- [在CDN控制台缓存过期时间设置为0，为何访问到的资源仍然不是最新内容？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#fe7cc249d9cy8 "")

- [源站变更文件后，CDN节点上的缓存会主动、实时更新吗？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#8674697ff4s48 "")

- [影响CDN缓存命中率下降的因素有哪些？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#3ddd3cbc28cwc "")

- [如何排查CDN缓存命中率较低的问题？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#ac299fc256fo3 "")

- [如何提高CDN缓存命中率？](https://help.aliyun.com/zh/cdn/use-cases/increase-the-cache-hit-ratios-of-alibaba-cloud-cdn "")

- [如何设置缓存全局生效？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#68352508cbyec "")

- [设置Nginx HTTP缓存策略](https://help.aliyun.com/zh/cdn/user-guide/set-the-nginx-cache-policy "")

- [设置Apache缓存策略](https://help.aliyun.com/zh/cdn/user-guide/set-apache-caching-policy "")

- [设置IIS缓存策略](https://help.aliyun.com/zh/cdn/user-guide/set-the-iis-cache-policy "")

- [CDN加速静态资源时如何设置服务器端的缓存过期时间？](https://help.aliyun.com/zh/cdn/user-guide/specify-a-ttl-value-for-pops-when-using-alibaba-cloud-cdn-to-accelerate-the-delivery-of-static-content "")

- [通过CDN访问与直接访问源站得到的结果不一样](https://help.aliyun.com/zh/cdn/user-guide/the-results-obtained-by-accessing-the-source-site-through-alibaba "")

- [缓存配置为什么没有生效？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#2e4c7dc2deei7 "")

- [通过HTTP响应头配置CDN跨域资源共享（CORS）及注意事项](https://help.aliyun.com/zh/cdn/user-guide/configure-cors "")

- [为什么已经配置了响应头Access-Control-Allow-Origin，但是访问资源仍提示跨域问题，response header中没有配置的响应头？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#baec2b5193okp "")

- [异常状态码缓存规则是什么？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#3233d6eb29tvn "")

- [出站响应头和入站响应头有什么区别？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#389228aa9b042 "")

- [如何配置整个域名不缓存？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#fc4fbd1001jpw "")

- [CDN是否支持多副本缓存？如何实现CDN的多副本缓存？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#2ed61269e13op "")

- [CDN如何配置子目录访问首页？](https://help.aliyun.com/zh/cdn/user-guide/cache-related-faq#319be90699tcy "")


## CDN **缓存清理机制是什么？**

缓存在CDN节点上的资源，如果该资源的访问热度较低（同一个CDN节点上的同一个资源被客户端访问的频次较低），那么很可能会在缓存过期之前被CDN节点上其他访问热度较高的资源覆盖。

## CDN **默认的缓存规则是什么？**

CDN节点在收到源站响应的文件资源的时候，会按照以下的缓存规则来执行（数值越小，优先级越高）：

![缓存优先级](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9740041961/p384328.png)

1. 源站响应`pragma:no-cache`、`cache-control:no-cache`（或者`no-store`，或者`max-age=0`）时，CDN遵循源站的策略，完全不缓存资源。

2. CDN控制台设置的缓存过期时间或者状态码过期时间。



**说明**







若CDN请求同时命中多条规则，有且仅有一条规则会生效，优先级为：权重>规则创建时间。



   - 有多条缓存规则的情况下，建议每条缓存规则都设置不同的权重（权重越大优先级越高），通过权重来控制规则执行优先级。

   - 权重相同的规则生效优先级：先创建的＞后创建的，与规则类型无关。


3. 源站配置其他缓存规则，优先级由高至低为：`cache-control`>`expires`>`last-modified`>`ETag`。

1. 如果源站响应中携带了`cache-control`，参数值包含`max-age`或`s-maxage`，并且`max-age`或`s-maxage`的值大于0，则使用`cache-control`设置缓存过期时间，例如：cache-control:max-age=3600。如果同时存在`max-age`和`s-maxage`，则以`s-maxage`的值为准。

2. 如果源站响应中没有携带`cache-control`，但是携带了`Expires`，则使用`Expires`设置缓存过期时间，例如：expires:Tue, 25 Nov 2031 17:25:43 GMT。

3. 如果源站响应中没有携带`cache-control`和`Expires`，但是携带了`last-modified`，则使用以下规则来计算缓存时间：使用公式（当前时间-`last-modified`）\\* 0.1，计算结果在10秒~3600秒及之间的，取计算结果时间；小于10秒的，按照10秒处理；大于3600秒的，按照3600秒处理。

4. 如果源站响应中没有携带`cache-control`、`Expires`和`last-modified`，但是携带了`ETag`，缓存10秒。
4. 如果源站返回的数据中，`cache-control`、`expires`、`last-modified`和`ETag`这些缓存策略相关的响应头都没有携带，则默认不缓存。


## **如何判断** CDN **缓存是否成功？**

阿里云CDN对于文件是否支持缓存，您可以通过检查HTTP响应头中的相关字段来判断。

1. `X-Cache`: 表示请求是否命中CDN缓存。值为 **HIT** 表示命中， **MISS** 或者字段不存在表示未命中。

2. `Age`: 表示文件在CDN节点上缓存的时间（秒）。文件被刷新或首次访问无此字段。`Age`为0表示缓存过期，需回源校验。

3. `X-Swift-CacheTime`: 表示文件在CDN节点上的允许缓存时间。计算剩余缓存时间：`X-Swift-CacheTime`– `Age`。

4. `X-Swift-SaveTime`：表示资源首次被缓存到CDN节点上的时间（GMT）。转换为中国北京时间需加上8小时。


为了查看这些HTTP响应头，您可以通过以下两种方式查看您的内容是否缓存到CDN：

#### **方式1：使用浏览器的开发者工具（如Chrome的开发者工具）**

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/2280724071/p753872.png)

#### **方式2：使用curl命令查看资源缓存情况**

```javascript
curl "http://example.com/path/to/response.html" -v
```

![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/0957228471/p960215.png)

## **如何解决URL的传递参数为变量导致** CDN **缓存命中率低的问题？**

可能是因为没有开启CDN的忽略参数功能，详情请参见 [URL的传递参数为变量导致CDN缓存命中率低](https://help.aliyun.com/zh/cdn/user-guide/variable-parameters-in-urls-result-in-low-cdn-cache-hit-ratio "")。

## **如何设置文件不缓存直接回源？**

根据您的需求，针对不希望缓存的资源，按照目录、文件路径、文件类型设置对应的缓存时间，设置如下：

- **类型**：选择 **目录** 或 **文件后缀名**。

- **地址**：填写您不想缓存的具体资源路径或文件名后缀，例如`php,jsp,asp`类型的动态文件和`admin`目录下的所有文件。

- **过期时间**：设置为“0”，表示不缓存该类型的资源。

- **权重**：可按照需要调整权重值，权重越高，优先级越强。


详情请参见 [配置CDN缓存过期时间](https://help.aliyun.com/zh/cdn/user-guide/configure-the-cdn-cache-expiration-time "")。

![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/1586824071/p754131.png)

## **在** CDN **控制台缓存过期时间设置为0，为何访问到的资源仍然不是最新内容？**

在CDN控制台将缓存过期时间设置为0，目的是每次请求都直接回源站获取最新内容。然而，如果您发现访问到的资源仍然不是最新的内容，可能有几个原因：

1. **浏览器本地缓存**：浏览器可能缓存了旧内容。建议清除浏览器缓存或使用无痕模式测试。

2. **配置生效延迟**：设置缓存时间为0后，可能需要时间让所有CDN节点生效。另外，如果CDN节点未检测到更改，可能仍返回旧缓存。

3. **源站缓存未刷新**：源站服务器可能有缓存机制，未及时更新时，CDN节点回源可能获取旧缓存。

4. **节点缓存清除延迟**：修改配置前已缓存的资源可能需要时间清除。您可以手动刷新缓存，确保立即获取最新内容，详情请参见 [操作指南](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources#section-wdh-o0c-cwb "")。


## **源站变更文件后，** CDN **节点上的缓存会主动、实时更新吗？**

源站变更文件后，CDN节点上的缓存不会主动、实时更新。缓存更新取决于配置的缓存策略。

- CDN节点根据配置的缓存过期时间更新缓存。如果缓存未过期，源站变更文件不会立即反映在CDN缓存中，详情请参见 [配置CDN缓存过期时间](https://help.aliyun.com/zh/cdn/user-guide/configure-the-cdn-cache-expiration-time "")。

- 您可以通过CDN提供的刷新缓存手动清除缓存，使下一次请求回源获取最新的内容。

  - 通过控制台操作： [操作指南](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources#section-wdh-o0c-cwb "")

  - 调用API接口： [刷新缓存](https://help.aliyun.com/zh/cdn/developer-reference/api-cdn-2018-05-10-refreshobjectcaches "")

## **影响** CDN **缓存命中率下降的因素有哪些？**

影响阿里云CDN缓存命中率下降的因素如下：

1. **刷新缓存**：手动或自动刷新缓存操作可能导致短时间内命中率下降。

2. **带宽突增**：当带宽在短时间内大幅度增加时，会导致CDN节点回源请求增多，从而降低缓存命中率。

3. **CDN节点访问新内容**：如果CDN节点频繁访问首次请求的新内容，也会导致回源较多，进而表现出缓存命中率的下降趋势。

4. **缓存规则调整**：对CDN缓存策略进行修改或调整可能会影响缓存命中率，例如未配置合适的缓存过期时间或者缓存策略设置不当。

5. **URL中带有可变参数**：URL中问号（?）后的参数变化会导致不同的URL请求被视为不同的资源，即使实际指向的是同一份内容，这也会造成CDN缓存命中率降低。

6. **未合理配置缓存过期时间**：对于不同更新频率的静态文件，如未根据实际情况设置合理的缓存过期时间，可能会导致缓存资源过早失效，从而影响缓存命中率。


更多场景关于影响缓存命中率的因素介绍请参见 [提高CDN缓存命中率](https://help.aliyun.com/zh/cdn/use-cases/increase-the-cache-hit-ratios-of-alibaba-cloud-cdn "")。具体可参见 [刷新和预热资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources "")、 [忽略参数](https://help.aliyun.com/zh/cdn/user-guide/ignore-parameters "") 和 [配置CDN缓存过期时间](https://help.aliyun.com/zh/cdn/user-guide/configure-the-cdn-cache-expiration-time "")。

## **如何排查CDN缓存命中率较低的问题？**

缓存命中率低会导致加载速度变慢和源站负载增加。请参见 [CDN缓存命中率较低排查方法](https://help.aliyun.com/zh/cdn/user-guide/cdn-cache-hit-rate-low-troubleshooting-method "")。

## **如何设置缓存全局生效？**

您可以通过设置缓存过期时间来实现缓存全局生效。设置时， **类型** 选择 **目录** 后，在地址栏用正斜线（/）匹配所有目录。具体操作请参见 [配置CDN缓存过期时间](https://help.aliyun.com/zh/cdn/user-guide/configure-the-cdn-cache-expiration-time#task-261642 "")。

## **缓存配置为什么没有生效？**

如果您配置了缓存规则，在使用过程中发现此缓存规则未生效，可能是以下原因：

1. **生效延迟**：缓存规则的修改或新增通常需要一段时间才能生效，请您在规则生效后再验证。

2. **缓存更新机制：** 新规则不会立即应用到已缓存的内容，需要等到原缓存过期后才会生效。

3. **缓存刷新操作未执行：** 更改缓存设置后，如果没有手动刷新缓存，旧的缓存内容将继续被提供给用户，直到自然过期。详情请参见 [刷新和预热资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources#section-wdh-o0c-cwb "")。

4. **缓存响应头设置不当**：检查源站发送的HTTP响应头里的`Cache-Control`和`Expires`标头是否正确设置。

5. **缓存规则有优先级**：若CDN请求同时命中多条规则，优先级为：权重>规则创建时间。


   - 有多条缓存规则的情况下，建议每条缓存规则都设置不同的权重（权重越大优先级越高），通过权重来控制规则执行优先级。

   - 权重相同的规则生效优先级：先创建的＞后创建的，与规则类型无关。


**配置示例**：为加速域名`demo.aliyun.com`配置以下缓存策略，CDN节点回源下载资源`http://demo.aliyun.com/image/example.png`，虽然以下两条规则都匹配到了，但是因为这两条规则的权重相同，因此要判断规则创建的时间，先创建的规则优先级高于后创建的，因为目录/image这条规则创建的时间更早，所以系统最终生效的是目录类型这条规则。![image.png](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/3001931571/p703246.png)

## **通过HTTP响应头配置CDN跨域资源共享（CORS）及注意事项**

设置适当的HTTP响应头，允许来自不同源的请求访问资源，详情请参见 [配置跨域资源共享](https://help.aliyun.com/zh/cdn/user-guide/configure-cors "")。

## **为什么已经配置了响应头Access-Control-Allow-Origin，但是访问资源仍提示跨域问题，response header中没有配置的响应头？**

如果您在阿里云CDN中配置了`Access-Control-Allow-Origin`等回源响应头，但客户端仍遇到跨域问题且响应头中没有这些配置，可能原因如下：

#### **可能的原因**

1. **配置未生效或错误**：配置未正确设置或尚未生效 **。**

2. **CDN缓存**：CDN节点缓存了旧的响应头。

3. **源站问题**：源站的跨域响应头与CDN配置冲突。

4. **浏览器缓存**：浏览器缓存了旧的响应。


#### **解决方案**

1. **验证配置**：确认CDN配置已正确设置并生效。

2. **清除CDN缓存**：使用CDN的刷新功能清空缓存，然后再次访问资源。具体请参见 [刷新和预热资源](https://help.aliyun.com/zh/cdn/user-guide/refresh-and-prefetch-resources "")。

3. **检查源站设置**：确认源站不会返回与CDN配置冲突的跨域响应头。建议统一源站和CDN的跨域头设置。

4. **清除浏览器缓存**：清空浏览器缓存，或使用无痕模式测试。

5. **联系技术支持**：如果问题仍然存在，请联系阿里云CDN技术支持。


## 异常状态码缓存规则是什么？

- 对于204、305、404、405、414、424、429、500、501、502、503和504状态码，缓存规则如下：
![image](<Base64-Image-Removed>)
1. 如果源站返回`set-cookie`响应头，CDN不缓存。

2. 如果源站没有返回Set-Cookie响应头，则遵循CDN控制台配置的状态码过期时间来缓存，配置多条规则时生效方式请参考多条规则生效优先级说明。

3. 如果源站没有返回Set-Cookie响应头，CDN控制台也没有配置状态码过期时间，则按照源站设置的Pragma、Cache-Control或者Expires响应头来缓存。

4. 如果源站没有返回Set-Cookie、Pragma、Cache-Control或者Expires响应头，CDN控制台也没有配置状态码过期时间，则默认缓存1秒。
- 对于302、307和403状态码，缓存规则如下：
![image](<Base64-Image-Removed>)
1. 如果源站返回`set-cookie`响应头，CDN不缓存。

2. 如果源站没有返回Set-Cookie响应头，则遵循CDN控制台配置的状态码过期时间来缓存，配置多条规则时生效方式请参考多条规则生效优先级说明。

3. 如果源站没有返回Set-Cookie响应头，CDN控制台也没有配置状态码过期时间，则按照源站设置的Pragma、Cache-Control或者Expires响应头来缓存。

4. 如果源站没有返回Set-Cookie、Pragma、Cache-Control或者Expires响应头，CDN控制台也没有配置状态码过期时间，不缓存。
- 针对304状态码，CDN将不进行缓存，且无法通过任何方式设置缓存时间。


## 出站响应头和入站响应头 **有什么区别？**

![image](<Base64-Image-Removed>)

出站响应头和入站响应头在缓存架构中代表不同环节的HTTP头部信息。

- **出站响应头**：由CDN节点发送给客户端（如浏览器）的HTTP响应头。当CDN节点有缓存内容时，会直接返回给客户端，无需向源站请求。

- **入站响应头**：由源站发送给CDN节点的HTTP响应头。当CDN节点的缓存过期或未命中时，CDN点会向源站请求最新内容，源站返回的内容及相关HTTP头部信息就是入站响应头。


因此，出站响应头和入站响应头的区别在于它们的应用场景和控制对象不同。出站响应头用于控制客户端和CDN节点的缓存行为，而入站响应头用于控制源站与CDN节点之间的缓存行为。它们通常共同使用，以实现高效、精确的缓存控制。关于入站响应头的更多信息，请参见 [修改入站响应头](https://help.aliyun.com/zh/cdn/user-guide/rewrite-http-response-headers "")。

## **如何配置整个域名不缓存？**

为了配置阿里云CDN整个域名不缓存，您可以通过设置 **全路径缓存过期时间为0** 来实现。以下是具体步骤：

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **缓存配置**。

5. 在 **缓存过期时间** 页签下，单击 **添加**。

   - **类型**：选择 **目录**。

   - **地址**：填写`/`，表示全部路径。

   - **过期时间**：填写`0秒`。

   - 其他参数保持默认选项。
6. 单击 **确定**，完成配置。


**说明**

若阿里云CDN请求同时命中多条规则，有且仅有一条规则会生效，优先级为：权重>规则创建时间。

如果 **缓存过期时间** 中有多条规则，请保证全域名不缓存规则的 **权重** 最高（此时优先级最高）。

![image](<Base64-Image-Removed>)

## **CDN是否支持多副本缓存？如何实现CDN的多副本缓存？**

CDN支持默认多副本缓存。此时源站需要携带`Vary`头来告知CDN节点需要用哪个请求头的值来做多副本。

以压缩为例，当客户端发送 `Accept-Encoding: gzip` 时，源站会返回经过 gzip 压缩的内容；而如果客户端发送的是 `Accept-Encoding: br`，源站则返回使用 Brotli 压缩的内容。为了缓存这些不同版本的响应，就需要源站在响应中添加 `Vary` 头，明确告知缓存系统根据哪个请求头来区分不同的副本。在本例中，源站应设置 `Vary: Accept-Encoding`，表明需要根据 `Accept-Encoding` 的值来存储和提供不同的缓存副本。

## **CDN如何配置子目录访问首页？**

通过访问子目录名来返回默认的子目录首页是站点常见的操作之一，在CDN上也可以实现这个能力，减少源站改动。

例如，首页文件是https://www.example.com/cdn/index.html，该方案可以实现访问`https://www.example.com/cdn`、`https://www.example.com/cdn/`子目录也可以返回首页文件。

### **确认源站**

先确认源站的子目录首页具体文件可以访问，例如`https://www.example.com/cdn/index.html`可以正常访问到。

### **配置子目录重写**

1. 登录[CDN控制台](https://cdn.console.aliyun.com/)。

2. 在左侧导航栏，单击 **域名管理**。

3. 在 **域名管理** 页面，找到目标域名，单击 **操作** 列的 **管理**。

4. 在指定域名的左侧导航栏，单击 **缓存配置**。

5. 单击 **重写访问URL** 页签。

6. 单击 **添加**，根据您的实际需求，配置访问URL重写参数。

配置两条规则，分别针对结尾是`/`和结尾不是`/`的进行匹配：


   - 规则1：待重写的Path：`^/(.+)/$`；目标Path：`/$1/index.html`；执行规则：`Break`。

   - 规则2：待重写的Path：`^/([^.?#]+)$`；目标Path：`/$1/index.html`；执行规则：`Break`。


![image](<Base64-Image-Removed>)