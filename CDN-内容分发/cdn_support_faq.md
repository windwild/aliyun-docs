### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [CDN](https://help.aliyun.com/zh/cdn/)[服务支持](https://help.aliyun.com/zh/cdn/support/)常见问题

# 常见问题

更新时间：2025-12-11 02:47:22

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/cdn)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：HTTP状态码说明](https://help.aliyun.com/zh/cdn/developer-reference/http-status-code-description)[下一篇：CDN访问出现400错误码](https://help.aliyun.com/zh/cdn/support/cdn-access-error-reporting-400)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

基础功能/使用咨询

购买和计费

无法访问/访问异常

添加域名/域名解析

缓存相关

回源/源站

HTTPS相关

刷新/预热

安全相关

OSS相关

边缘程序

日志相关

Terraform和API相关

您在使用CDN时如果收到CDN返回的错误信息，可查阅CDN错误代码汇总匹配解决方案。如果您没有收到具体的错误信息，可根据如下问题分类匹配问题场景和解决方案。

**说明**

有关CDN常见错误的更多信息，请参见[CDN错误代码汇总](https://error-center.aliyun.com/status/product/Cdn?spm=5176.10421674.home.25.88c1ebedALghTT)。

## 基础功能/使用咨询

- [什么是阿里云CDN？](https://help.aliyun.com/zh/cdn/product-overview/what-is-alibaba-cloud-cdn#concept-aml-tlg-tdb "")

- [什么是域名解析？](https://help.aliyun.com/zh/cdn/support/what-is-dns-resolution#trouble-2323389 "")

- [什么是静态内容和动态内容？](https://help.aliyun.com/zh/cdn/support/what-are-static-content-and-dynamic-content#trouble-2321166 "")

- [CDN节点与镜像站点的区别是什么？](https://help.aliyun.com/zh/cdn/support/differences-between-a-cdn-pop-and-a-mirror#trouble-2323389 "")

- [如何关闭CDN服务或停止计费？](https://help.aliyun.com/zh/cdn/support/how-do-i-shut-down-the-cdn-service-or-stop "")


## 购买和计费

- [为什么监控查询流量、用量查询流量与日志统计流量有差异？](https://help.aliyun.com/zh/cdn/product-overview/traffic-amount-in-the-monitoring-and-usage-analytics-or-in-the-usage-statistics-feature-different-from-the-logged-traffic-amount#trouble-2320953 "")

- [为什么CDN停止服务后仍会产生费用？](https://help.aliyun.com/zh/cdn/product-overview/why-are-fees-still-charged-after-i-disable-alibaba-cloud-cdn-for-my-domain-name#trouble-2320953 "")

- [源站不在中国内地，使用中国内地CDN节点加速如何收费？](https://help.aliyun.com/zh/cdn/product-overview/billing-for-using-alibaba-cloud-cdn-pops-in-the-chinese-mainland-if-my-origin-server-is-located-outside-the-chinese-mainland#trouble-1925557 "")

- [CDN加速OSS计费说明](https://help.aliyun.com/zh/cdn/product-overview/billing-of-oss-content-acceleration#trouble-1925540 "")

- [阿里云CDN与阿里云其他产品配合使用时流量如何计费？](https://help.aliyun.com/zh/cdn/product-overview/billing-of-data-transfer-when-alibaba-cloud-cdn-is-used-with-other-alibaba-cloud-services#trouble-2320764 "")

- [如何查看新购买的CDN资源包？](https://help.aliyun.com/zh/cdn/product-overview/where-can-i-view-details-about-resource-plans-that-i-have-purchased#trouble-2320953 "")

- [购买了资源包为什么仍会扣费或欠费？](https://help.aliyun.com/zh/cdn/product-overview/why-am-i-still-charged-for-resources-after-i-purchase-resource-plans-of-alibaba-cloud-cdn#trouble-2323903 "")

- [关于请求数计费的常见问题](https://help.aliyun.com/zh/cdn/product-overview/faq-about-the-billing-of-requests#concept-1986432 "")

- [如何查看单个域名的分账明细？](https://help.aliyun.com/zh/cdn/product-overview/how-do-i-view-the-billing-details-or-split-bills#concept-1986432 "")

- [变更计费方式后，为什么还是按照原来的计费模式扣费？](https://help.aliyun.com/zh/cdn/product-overview/after-i-change-the-metering-method-of-alibaba-cloud-cdn-why-is-alibaba-cloud-cdn-still-billed-based-on-the-previous-metering-method#concept-2101373 "")

- [如何变更计费方式](https://help.aliyun.com/zh/cdn/product-overview/how-do-i-change-the-billing-method#task-2101383 "")

- [全站加速和CDN资源包可以共享吗，抵扣顺序是什么？](https://help.aliyun.com/zh/cdn/product-overview/can-resource-plans-be-shared-by-alibaba-cloud-cdn-and-dcdn-and-what-is-the-offset-order#concept-2101377 "")

- [RAM用户支持变更CDN的计费方式吗？](https://help.aliyun.com/zh/cdn/product-overview/can-ram-users-change-the-billing-method-of-alibaba-cloud-cdn#concept-2099559 "")

- [被攻击或恶意盗刷产生的流量和请求是否收费？](https://help.aliyun.com/zh/cdn/product-overview/am-i-charged-for-data-transfer-and-requests-that-are-generated-by-attacks-or-other-malicious-behaviors-such-as-click-farming#concept-2102888 "")

- [CDN节点在响应4xx状态码的情况下是否会产生费用？](https://help.aliyun.com/zh/cdn/product-overview/am-i-charged-if-the-requested-cdn-pop-returns-a-4xx-status-code#concept-2247324 "")


## 无法访问/访问异常

- [CDN回源时网站出现5xx报错的排查方法](https://help.aliyun.com/zh/oss/how-to-troubleshoot-5xx-errors-reported-on-websites-when-cdn-initiates-a-back-to-origin-request "")

- [使用CDN加速后网站无法访问](https://help.aliyun.com/zh/cdn/troubleshoot-unreachable-websites-after-using-alibaba-cloud-content-delivery-network-acceleration)

- [地域节点获取CDN节点文件异常或访问域名失败](https://help.aliyun.com/zh/cdn/access-exceptions-to-a-cdn-pop)

- [使用CDN加速后访问URL时出现空白页面](https://help.aliyun.com/zh/cdn/the-access-page-after-using-alibaba-cloud-content-delivery-network-acceleration-appears-blank)

- [定位访问异常是CDN节点问题还是源站问题](https://help.aliyun.com/zh/cdn/troubleshoot-whether-a-cdn-access-exception-is-caused-by-a-cdn-pop-or-network-problem)

- [开通海外节点后没有提高海外用户的访问速度](https://help.aliyun.com/zh/cdn/after-opening-overseas-nodes-in-alibaba-cloud-content-delivery-network-the-access-speed-of-overseas-users-has-not-been-improved)

- [使用域名访问HTML文件变为强制下载该文件](https://help.aliyun.com/zh/cdn/requests-sent-to-cdn-accelerated-domain-names-to-access-html-files-trigger-automatic-downloads-of-the-files)

- [站点接入到CDN后URL中参数加载失败](https://help.aliyun.com/zh/cdn/f4c898)

- [使用CDN后对网站的SEO的影响](https://help.aliyun.com/zh/cdn/whether-the-use-of-cdn-will-affect-the-seo-of-the-website)

- [使用CDN加速后Websocket对象无法访问](https://help.aliyun.com/zh/cdn/the-websocket-object-cannot-be-accessed-after-cdn-is-used)

- [访问CDN加速的资源返回304 状态码](https://help.aliyun.com/zh/cdn/http-304-status-code-is-returned-for-resource-access-after-a-cdn-domain-name-is-used)

- [访问CDN资源返回403状态码](https://help.aliyun.com/zh/cdn/troubleshoot-a-403-forbidden-error-when-accessing-resources-through-cdn)

- [使用CDN后访问HTML页面返回“Content-Type: application/octet-stream”导致变为下载页面](https://help.aliyun.com/document_detail/252067.html)

- [通过CDN请求大文件自动断开](https://help.aliyun.com/document_detail/254231.html)

- [访问HTTPS网站速度慢但本地网络速度正常排查思路](https://help.aliyun.com/document_detail/163177.html)

- [重定向次数过多的解决方案](https://help.aliyun.com/zh/cdn/support/too-many-redirects-occur-after-my-domain-name-is-accelerated-by-alibaba-cloud-cdn#trouble-2248995 "")

- [CDN节点运维下线说明](https://help.aliyun.com/zh/cdn/support/cdn-node-o-m-offline-description "")


## 添加域名/域名解析

- [CDN支持泛域名加速吗？](https://help.aliyun.com/zh/cdn/does-alibaba-cloud-cdn-support-wildcard-domain-names#concept-2438181 "")

- [切换加速区域后的影响是什么？](https://help.aliyun.com/zh/cdn/impacts-when-i-change-the-accelerated-region-of-alibaba-cloud-cdn#trouble-2323389 "")

- [如何测试CNAME解析是否正常？](https://help.aliyun.com/zh/cdn/check-whether-a-cname-record-takes-effect#trouble-1780507 "")

- [阿里云子账号获取ListRoles权限](https://help.aliyun.com/zh/cdn/grant-the-listroles-permission-to-a-ram-user#trouble-2449811 "")

- [如何验证CDN节点是否生效](https://help.aliyun.com/zh/cdn/ee86e4)

- [新添加的域名审核失败](https://help.aliyun.com/zh/cdn/alibaba-cloud-content-delivery-network-dynamic-route-for-content-delivery-network-add-accelerated-domain-name-audit-failed)

- [如何处理未备案或备案失效的域名](https://help.aliyun.com/zh/cdn/icp-number-of-my-domain-name-expires)

- [上传泛域名证书后访问三级域名异常](https://help.aliyun.com/zh/cdn/an-error-occurred-when-an-alibaba-cloud-cdn-wildcard-domain-certificate-was-used-to-match-a-target-website-address)

- [设置CDN时出现“检测到没有启用状态的AccessKey，暂不提供CNAME绑定服务”报错](https://help.aliyun.com/zh/cdn/the-cname-binding-service-is-unavailable-because-no-enabled-accesskey-pair-is-detected)

- [如何验证指定的IP是否为阿里云CDN节点的IP地址](https://help.aliyun.com/zh/cdn/verify-that-the-specified-ip-address-is-the-ip-address-of-the-alibaba-cloud-cdn-pop)

- [如何解决DNS解析记录冲突](https://help.aliyun.com/zh/cdn/dns-records-conflict-with-each-other#concept-2093797 "")

- [CNAME解析未生效怎么办？](https://help.aliyun.com/zh/cdn/cname-record-does-not-take-effect#concept-2093802 "")

- [添加CDN加速域名时，源站可以使用其他账号下的OSS域名吗？](https://help.aliyun.com/zh/cdn/use-an-oss-bucket-that-belongs-to-another-alibaba-cloud-account-as-the-origin-server#concept-2102900 "")

- [域名出现备案阻断是什么原因以及该如何处理？](https://help.aliyun.com/zh/cdn/why-is-the-icp-filing-of-a-domain-name-suspended-and-how-do-i-handle-the-issue#concept-2187023 "")


## 缓存相关

- [CDN缓存命中率低](https://help.aliyun.com/zh/cdn/alibaba-cloud-content-delivery-network-cache-hit-rate-is-low)

- [URL的传递参数为变量导致缓存命中率低](https://help.aliyun.com/zh/cdn/the-passing-parameter-of-the-url-is-a-variable-resulting-in-a-low-alibaba-cloud-content-delivery-network-cache-hit-rate)

- [设置Nginx缓存策略](https://help.aliyun.com/zh/cdn/c57f83)

- [设置Apache缓存策略](https://help.aliyun.com/zh/cdn/0dac46)

- [设置IIS缓存策略](https://help.aliyun.com/zh/cdn/setting-method-of-iis-cache-policy)

- [如何关闭指定域名的目录或者文件的缓存策略](https://help.aliyun.com/zh/cdn/how-can-i-disable-directory-and-file-cache-policy-through-cdn)

- [加速静态资源时如何设置服务器端的缓存过期时间](https://help.aliyun.com/zh/cdn/user-guide/specify-a-ttl-value-for-pops-when-using-alibaba-cloud-cdn-to-accelerate-the-delivery-of-static-content)

- [通过阿里云CDN系列产品访问与直接访问源站得到的结果不一样](https://help.aliyun.com/document_detail/213792.html)

- [如何划分CDN缓存节点？](https://help.aliyun.com/zh/cdn/user-guide/classification-of-cdn-cache-pops#trouble-2342201 "")

- [如何处理预热URL提示预加载队列已满问题？](https://help.aliyun.com/zh/cdn/user-guide/preload-queue-is-full#trouble-2367798 "")

- [如何设置缓存全局生效](https://help.aliyun.com/zh/cdn/user-guide/how-do-i-apply-cache-settings-to-a-specified-path#concept-2101066 "")

- [使用阿里云CDN加速后网站访问速度较慢](https://help.aliyun.com/document_detail/161222.html)

- [CDN的多语言缓存机制](https://help.aliyun.com/zh/cdn/user-guide/cdn-multi-language-cache-mechanism "")


## 回源/源站

- [CDN回源节点IP地址有哪些？](https://help.aliyun.com/zh/cdn/support/query-ip-addresses-of-pops-for-a-cdn-domain#trouble-1779964 "")

- [回源流量较大](https://help.aliyun.com/zh/cdn/alibaba-cloud-content-delivery-network-back-to-source-traffic-is-large)

- [回源流量大于访问流量](https://help.aliyun.com/zh/cdn/the-back-to-origin-traffic-of-the-alibaba-cloud-content-delivery-network-service-is-greater-than-the-access-traffic)

- [实际访问的域名与控制台设置的源站域名不同](https://help.aliyun.com/zh/cdn/handle-alibaba-cloud-cdn-origin-domain-name-errors)

- [新建CDN如何配置多个源站](https://help.aliyun.com/zh/cdn/configure-multiple-origin-servers-for-a-new-alibaba-cloud-cdn)

- [CDN的配置回源HOST与源站的区别](https://help.aliyun.com/zh/cdn/differences-between-alibaba-cloud-content-delivery-network-configuration-back-to-origin-host-and-origin)

- [请求CDN加速域名出现跨域问题并提示“The 'Access-Control-Allow-Origin' header has a value 'xxx' that is not equal to the supplied origin”](https://help.aliyun.com/document_detail/213793.html)

- [请求通过CDN回源后未正常启用Gzip压缩](https://help.aliyun.com/document_detail/205123.html)

- [如何处理源站的302跳转？](https://help.aliyun.com/zh/cdn/support/alibaba-cloud-cdn-process-302-redirects-from-an-origin-server#trouble-2320051 "")

- [排查CDN故障时如何将域名指向源站](https://help.aliyun.com/zh/cdn/fa5281)

- [阿里云CDN对源站的健康检查机制是什么？](https://help.aliyun.com/zh/cdn/support/health-check-mechanism-for-origin-servers#trouble-2323389 "")


## HTTPS相关

- [如何查看HTTPS请求数的使用情况](https://help.aliyun.com/zh/cdn/how-to-view-the-usage-of-the-number-of-https-requests)

- [如何给CDN加速域名配置HTTPS中级证书](https://help.aliyun.com/zh/cdn/how-to-configure-https-intermediate-certificate-for-alibaba-cloud-content-delivery-network-accelerated-domain-name)

- [微信小程序访问CDN证书校验失败](https://help.aliyun.com/zh/cdn/wechat-mini-program-access-cdn-certificate-verification-failed)

- [在CDN的HTTPS设置中申请免费证书失败](https://help.aliyun.com/document_detail/151172.html)

- [网站提示证书风险如何处理？](https://help.aliyun.com/zh/cdn/support/website-prompts-certificate-related-risks#concept-2097304 "")

- [源站服务器和CDN上的HTTPS证书冲突了怎么办？](https://help.aliyun.com/zh/cdn/support/the-ssl-certificate-on-the-origin-server-conflicts-with-the-one-in-alibaba-cloud-cdn#concept-2101135 "")

- [泛域名如何配置HTTPS证书？](https://help.aliyun.com/zh/cdn/support/configure-an-ssl-certificate-for-a-wildcard-domain-name#concept-2101136 "")

- [个人测试证书（免费版）到期后如何处理？](https://help.aliyun.com/zh/cdn/support/manage-free-ssl-certificates-after-they-expire#concept-2101147 "")

- [使用CDN加速后无法通过HTTPS访问资源](https://help.aliyun.com/document_detail/293537.html)


## 刷新/预热

- [配置CDN后如何对文件进行同名更新](https://help.aliyun.com/zh/cdn/how-to-update-files-after-configuration-alibaba-cloud-content-delivery-network)

- [如何查看预热任务的执行状态](https://help.aliyun.com/zh/cdn/how-to-check-whether-the-preheating-task-of-the-alibaba-cloud-content-delivery-network-is-completed)

- [访问域名出现“504 Gateway Time-out”报错](https://help.aliyun.com/zh/cdn/error-message-is-displayed-after-you-use-the-cdn-domain-name)

- [CDN和视频点播中使用脚本刷新预热M3U8资源](https://help.aliyun.com/document_detail/189851.html)


## 安全相关

- [如何屏蔽恶意IP访问](https://help.aliyun.com/zh/cdn/block-specified-ip-using-cdn)

- [源站存在安全防护等原因导致访问域名返回503状态码](https://help.aliyun.com/zh/cdn/a-503-error-is-reported-when-accessing-the-cdn-domain-name-due-to-origin-site-security-protection-or-other-reasons)

- [由于防盗链异常导致访问资源返回403状态码](https://help.aliyun.com/zh/cdn/solution-to-403-error-return-of-access-alibaba-cloud-content-delivery-network-due-to-anti-leech-anomaly)

- [为什么IP黑名单中的IP仍可访问资源？](https://help.aliyun.com/zh/cdn/why-can-an-ip-address-in-the-ip-blacklist-still-be-used-to-request-resources#trouble-2321152 "")

- [如何处理加速域名遭受DDoS或CC攻击问题？](https://help.aliyun.com/zh/cdn/protect-domain-names-accelerated-by-alibaba-cloud-cdn-from-ddos-or-http-flood-attacks#trouble-1893492 "")

- [CDN空Referer盗刷防护实践](https://help.aliyun.com/zh/cdn/prevent-traffic-abuse-with-empty-referer "")


## OSS相关

- [使用CDN加速的OSS跨域访问失败](https://help.aliyun.com/zh/oss/to-configure-alibaba-cloud-content-delivery-network-accelerated-oss-cross-domain-access)

- [CDN加速OSS资源](https://help.aliyun.com/zh/cdn/use-cases/use-alibaba-cloud-cdn-to-accelerate-the-delivery-of-resources-from-oss-buckets/ "")

- [使用CDN加速导致OSS配置的CORS失效](https://help.aliyun.com/zh/oss/alibaba-cloud-content-delivery-network-acceleration-causes-the-cors-configuration-of-oss-to-become-invalid)

- [网站中如何设置CORS访问](https://help.aliyun.com/zh/cdn/configure-cors-for-a-website-accelerated-by-alibaba-cloud-cdn)

- [配置跨域资源共享](https://help.aliyun.com/zh/cdn/user-guide/configure-cors "")

- [开启私有OSS Bucket回源后，访问域名提示“You are forbidden to list buckets”错误](https://help.aliyun.com/zh/cdn/you-are-forbidden-to-list-buckets-after-access-to-private-oss-buckets-is-enabled#concept-2120076 "")

- [CDN回源OSS私有Bucket功能与OSS静态网站托管功能的默认首页配置冲突](https://help.aliyun.com/zh/cdn/errors-arise-after-i-enable-access-to-private-oss-buckets-and-static-website-hosting#concept-2121413 "")


## 边缘程序

- [Fetch类FAQ](https://help.aliyun.com/zh/cdn/faq-about-the-fetch-api#concept-1957486 "")

- [waitUntil类FAQ](https://help.aliyun.com/zh/cdn/faq-about-waituntil#concept-1957495 "")

- [编码类FAQ](https://help.aliyun.com/zh/cdn/faq-about-encoding#concept-1957551 "")


## 日志相关

- [CDN访问日志的分析方法](https://help.aliyun.com/zh/cdn/analysis-method-of-alibaba-cloud-content-delivery-network-access-log)


## **Terraform和API相关**

- [使用Terraform添加CDN域名出现HTTPS配置报错](https://help.aliyun.com/zh/cdn/developer-reference/using-terraform-to-add-cdn-domain-name-results-in-https-configuration-error "")