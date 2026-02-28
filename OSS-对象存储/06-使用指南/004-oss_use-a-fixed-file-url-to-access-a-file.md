### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[对象/文件（Object）](https://help.aliyun.com/zh/oss/data-upload-and-download/)[上传文件](https://help.aliyun.com/zh/oss/upload-file-faq/)是否支持使用固定的地址访问已上传的文件？

# 是否支持使用固定的地址访问已上传的文件？

更新时间：2025-10-31 02:34:34

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：上传音视频文件时，音视频时长是否存在限制？](https://help.aliyun.com/zh/oss/duration-limit-for-audio-and-video-files-uploaded-to-oss)[下一篇：断点续传上传时报错Too many parts, Please increase part size.怎么办？](https://help.aliyun.com/zh/oss/what-should-i-do-if-encountering-the-error-too-many-parts-please-increase-part-size-during-during-resumable-upload)

该文章对您有帮助吗？

反馈

公共读以及公共读写权限的文件 **支持** 使用固定的地址访问已上传的文件，私有权限的文件 **不支持**。

- 文件读写权限为公共读或者公共读写

在存储路径未修改的情况下，公共读或者公共读写的文件的访问地址不变。您可以通过拼接文件URL的方式长期访问文件，文件URL的格式为`<http或者https>://<Bucket>.<Endpoint>/<Object>`，例如`https://examplebucket.oss-cn-hangzhou.aliyuncs.com/example.txt`。



**重要**





出于数据安全考虑，不建议您将文件读写权限设置为公共读或者公共读写。这可能会造成数据外泄以及费用激增的情况。更多信息，请参见 [Object ACL](https://help.aliyun.com/zh/oss/user-guide/object-acl "")。

- 文件读写权限为私有

对于读写权限为私有的文件，其文件URL格式为`<http或者https>://<Bucket>.<Endpoint>/<Object>?签名信息`，签名信息是动态变化的。因此，OSS不支持通过固定文件URL访问读写权限为私有的文件。更多信息，请参见 [签名版本4（推荐）](https://help.aliyun.com/zh/oss/developer-reference/add-signatures-to-urls "")。



**重要**





出于数据安全考虑，推荐将文件读写权限设置为私有。这样只有文件的拥有者可以对文件进行读写操作，其他人在未授权的情况下无法访问该文件。