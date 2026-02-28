### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [对象存储](https://help.aliyun.com/zh/oss/)[常用工具](https://help.aliyun.com/zh/oss/developer-reference/common-tools/)[ossfs 1.0](https://help.aliyun.com/zh/oss/developer-reference/ossfs-overview/)常见问题

# ossfs常见问题

更新时间：2025-12-29 04:27:00

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/oss)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：通过 PrivateLink 私网挂载](https://help.aliyun.com/zh/oss/developer-reference/private-network-mounting-through-privatelink)[下一篇：1.91.9版本](https://help.aliyun.com/zh/oss/developer-reference/version-1-91-9)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

通用说明

权限问题

挂载成功后，touch文件时报错403

通过rm命令删除文件时报错"Operation not permitted"

访问报错"The bucket you are attempting to access must be addressed using the specified endpoint”

挂载问题

ossfs挂载Bucket支持自定义域名吗？

使用1.91.5及之后版本的ossfs，在CentOS 7.x操作系统上通过HTTPS协议的OSS域名挂载Bucket时出现挂载失败

1.91.7之后的版本，通过ECS ram\_role挂载，挂载不上

挂载报错"ossfs: unable to access MOUNTPOINT /tmp/ossfs: Transport endpoint is not connected"

挂载报错"fusermount: failed to open current directory: Permission denied"

挂载报错"ossfs: Mountpoint directory /tmp/ossfs is not empty. if you are sure this is safe, can use the 'nonempty' mount option"

挂载报错"ops-nginx-12-32 s3fs\[163588\]: \[tid-75593\]curl.cpp:CurlProgress(532): timeout now: 1656407871, curl\_times\[curl\]: 1656407810, readwrite\_timeout: 60"

挂载报错"ossfs: credentials file /etc/passwd-ossfs should not have others permissions"

挂载成功后，ls目录时报错"operation not permitted"

挂载时报错"fuse: device not found, try 'modprobe fuse'"

挂载时报错"ossfs: error while loading shared libraries: libcrypto.so.1.1: cannot open shared object file: No such file or directory"

费用问题

在ECS上挂载OSS，如何避免因后台程序扫描文件而产生费用

磁盘内存问题

ossfs偶尔出现断开的情况

ossfs为什么会把磁盘空间写满？

ossfs挂载后，为什么通过df命令显示磁盘空间大小为256 TB？

通过cp命令拷贝数据时报错"input/output error"

使用rsync同步时报错"input/output error"

上传大文件时报错"there is no enough disk space for used as cache(or temporary)"

版本依赖问题

安装ossfs时报错"fuse: warning: library too old, some operations may not work"

安装依赖库fuse报错

使用Is列举文件时报错"Input/Output error"

使用yum/apt-get安装ossfs时报错"conflicts with file from package fuse-devel"

其他问题

在OSS文件数量较多或高并发场景下，使用ossfs挂载后出现卡顿的情况，有什么建议？

使用ossfs上传到OSS的文件的Content-Type全是application/octet-stream

ossfs为什么将文件夹识别成普通文件

ossfs执行mv操作失败

ossfs是否支持在Windows环境中挂载存储空间？

ossfs是否支持将OSS存储空间挂载至多台Linux ECS服务器？

为什么用ossfs看到的文件信息（例如大小）与其他工具看到的不一致

为什么Bucket开启版本控制后出现挂载慢的问题？

如何设置通过HTTPS方式挂载？

目录下有非常多的文件时，为什么ls该目录很慢

卸载时报错"fusermount: failed to unmount /mnt/ossfs-bucket: Device or resource busy"

使用ossfs 1.0时出现大量404日志

本文介绍在使用ossfs时遇到的一些问题案例及解决方案。如果您遇到问题，可以先检查ossfs版本。如果版本较老（如1.80.x）， **建议先升级到最新版本**。新版本增加了新特性，并有稳定性提升。

## 通用说明

ossfs报错信息中均包含message。排查问题时，需要收集这些message，并根据message判断问题。例如socket连接失败、HTTP响应的状态码4xx、5xx等，使用前先开启debug-log。

- 403错误是因权限不足，导致访问被拒绝。

- 400错误是用户的操作方法有误。

- 5xx错误一般和网络抖动以及客户端业务有关系。


ossfs有以下特点：

- ossfs是将远端的OSS挂载到本地磁盘，如果对文件读写性能敏感的业务，不建议使用ossfs 。

- ossfs的操作不是原子性，存在本地操作成功，但OSS远端操作失败的风险。


如果ossfs不满足您的业务需求，建议使用 [ossutil](https://help.aliyun.com/zh/oss/developer-reference/overview-59/#concept-cnr-3d4-vdb "")。

## **权限问题**

### **挂载成功后，touch文件时报错403**![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5324459951/p36506.png)

**问题分析**：403错误通常是访问权限问题导致的。以下情况会导致touch一个文件出现403报错。

- 该文件为归档类型文件，touch时会出现403报错。

- 使用的AccessKey无该存储空间的操作权限。


**解决方案**：

- 归档类型文件问题：将文件解冻后访问或为文件所在Bucket开启归档直读。

- 权限问题：为使用的AccessKey对应的账号配置正确的权限。


### **通过rm命令删除文件时报错"Operation not permitted"**

**问题分析**：通过rm命令删除文件时，会调用DeleteObject API进行删除。如果您是通过RAM用户挂载，请检查挂载的RAM用户是否具备删除文件的权限。

**解决方案**：为该RAM用户设置正确的权限。更多信息，请参见 [RAM Policy](https://help.aliyun.com/zh/oss/ram-policy-overview/#concept-y5r-5rm-2gb "") 和 [RAM Policy常见示例](https://help.aliyun.com/zh/oss/user-guide/common-examples-of-ram-policies#concept-2025445 "")。

### **访问报错"The bucket you are attempting to access must be addressed using the specified endpoint”**

**问题分析**：根据Message判断，错误原因是Endpoint指定错误，有以下两种可能性：

- Bucket和Endpoint不匹配。

- Bucket所属UID和实际的AccessKey对应的UID不一致。


**解决方案**：确认配置信息正确并修改。

## **挂载问题**

### **ossfs挂载Bucket支持自定义域名吗？**

不支持。ossfs目前不支持自定义域名场景。

### **使用1.91.5及之后版本的ossfs，在CentOS 7.x操作系统上通过HTTPS协议的OSS域名挂载Bucket时出现挂载失败**

解决方案：

1. 挂载时增加`-ocurldbg`选项，查看日志中是否存在`NSS error -8023 （SEC_ERROR_PKCS11_DEVICE_ERROR）`相关的日志。

2. 如果有上述相关错误日志，请检查本地安装的NSS版本。

当NSS版本为3.36时，需执行`yum update nss`命令更新NSS版本后再尝试重新挂载。


### **1.91.7之后的版本，通过ECS ram\_role挂载，挂载不上**

**解决方案**：

1. 使用 `curl http://100.100.100.200/latest/meta-data/ram/security-credentials/[your-ecs-ram-role]` 命令检查是否能连通。

2. 如果curl可以正常连通，可以在挂载时加上选项 `-o disable_imdsv2`。


### **挂载报错"ossfs: unable to access MOUNTPOINT /tmp/ossfs: Transport endpoint is not connected"**

**问题分析**：未创建该目录导致的。

**解决方案**：先创建对应的目录，之后再进行挂载操作。

### **挂载报错"fusermount: failed to open current directory: Permission denied"**

**问题分析**：fuse的Bug，要求当前用户对当前目录（非挂载目录）有读权限。

**解决方案**：通过cd命令切换到一个有读权限的目录，再运行ossfs命令。

### **挂载报错"ossfs: Mountpoint directory /tmp/ossfs is not empty. if you are sure this is safe, can use the 'nonempty' mount option"**

**问题分析**：默认情况下，ossfs只能挂载到空目录下。当试图挂载到非空目录下时，会提示上述错误。

**解决方案**：切换到一个空目录下重新挂载。如果还是需要挂载到该目录下，挂载时增加 -ononempty 参数。

### **挂载报错"ops-nginx-12-32 s3fs\[163588\]: \[tid-75593\]curl.cpp:CurlProgress(532): timeout now: 1656407871, curl\_times\[curl\]: 1656407810, readwrite\_timeout: 60"**

**问题分析**：ossfs挂载超时。

**解决方案**：ossfs通过readwrite\_timeout选项指定读或者写请求的超时时间，单位为秒，默认值为60秒。您需要结合实际业务场景，适当增加该选项的取值。

### **挂载报错"ossfs: credentials file /etc/passwd-ossfs should not have others permissions"**

**问题分析**：/etc/passwd-ossfs文件权限不正确。

**解决方案**：/etc/passwd-ossfs保留了访问凭证信息，需要限制others访问该文件。您可以通过`chmod 640 /etc/passwd-ossfs`命令修改文件的访问权限。

### **挂载成功后，ls目录时报错"operation not permitted"**

**问题分析**：请检查您的Bucket中，是否存在名称含有不可见字符的Object。文件系统对文件名和目录名有严格的限制，因此会收到上述错误。

**解决方案**：用其他工具对这些Object重命名后，ls就能正确显示目录内容了。

### **挂载时报错"fuse: device not found, try 'modprobe fuse'"**

**问题分析**：尝试在Docker容器中使用ossfs挂载时遇到的错误"fuse: device not found, try 'modprobe fuse'"通常是因为容器缺乏访问或加载FUSE内核模块所需的权限。

**解决方案**：在Docker容器中运行时，可以通过添加`--privileged=true`参数来赋予容器更高的权限，从而允许容器内的进程执行类似宿主机的操作，包括使用FUSE文件系统。使用`--privileged`标志启动容器的命令示例如下：

```shell
docker run --privileged=true -d your_image
```

### **挂载时报错**"ossfs: error while loading shared libraries: libcrypto.so.1.1: cannot open shared object file: No such file or directory"

**问题分析**：安装包版本与对应的操作系统版本不匹配。

**解决方案**： [下载](https://help.aliyun.com/zh/oss/developer-reference/install-ossfs-1-0#title-sog-1f0-t50 "") 与系统相对应的安装包即可解决。

## **费用问题**

### **在ECS上挂载OSS，如何避免因后台程序扫描文件而产生费用**

**问题分析**：程序扫描ossfs挂载的目录，会转换成向OSS的请求。如果请求次数很多，会产生费用。

**解决方案**：可以通过auditd工具查看是哪些进程扫描了OSS挂载的目录。具体步骤如下：

1. 安装auditd并启动。















```shell
sudo apt-get install auditd
sudo service auditd start
```

2. 将OSS挂载的目录设置为监视目录，例如挂载目录为/mnt/ossfs。















```shell
auditctl -w /mnt/ossfs
```

3. 在auditlog中查看是哪些进程访问了这个目录。















```shell
ausearch -i | grep /mnt/ossfs
```

4. 修改参数，跳过程序扫描。



例如通过auditlog查到是 [updatedb](https://linux.die.net/man/8/updatedb) 扫描了所挂载的目录，可以通过修改/etc/updatedb.conf让它跳过。具体做法是：



1. 在`RUNEFS =`后面加上`fuse.ossfs`。

2. 在`PRUNEPATHS =`后面加上挂载的目录。


## **磁盘内存问题**

### **ossfs偶尔出现断开的情况**![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4324459951/p36507.png)

**问题分析**：

1. 开启ossfs的debug日志，加上-d -odbglevel=dbg参数，ossfs会将日志写入到默认系统文件中。

   - CentOS系统：写入到`/var/log/message`。

   - Ubuntu系统：写入到`/var/log/`syslog。
2. 分析日志，发现ossfs在listbucket、listobject申请内存过多，触发了系统的oom。



**说明**





listobject是发起HTTP请求到OSS获取文件的meta信息，如果客户的文件很多，ls会消耗系统大量内存来获取文件的meta。


**解决方案**：

- 通过-omax\_stat\_cache\_size=xxx参数增大stat cache 的 size，这样第一次ls会较慢，但是后续的ls速度会提高，因为文件的元数据都在本地cache中。这个值默认是1000，约消耗4 MB内存，请根据您机器内存大小调整为合适的值。

- ossfs在读写时会占用磁盘写大量的temp cache ，和Nginx差不多，可能会导致磁盘可用空间不足。当ossfs退出后，会自动清理临时文件。

- 使用ossutil替代ossfs，非线上敏感业务可以使用ossfs ，要求可靠性、稳定性的建议使用ossutil。


### **ossfs为什么会把磁盘空间写满？**

**问题原因**：为提升性能，默认情况下ossfs会尽可能使用磁盘空间来保存上传或下载的临时数据，此时会存在磁盘空间写满的情况。

**解决方案**：您可以通过-oensure\_diskfree选项指定保留磁盘空间大小。例如，指定保留20 GB的磁盘空间大小，命令如下：

```shell
ossfs examplebucket /tmp/ossfs -o url=http://oss-cn-hangzhou.aliyuncs.com -oensure_diskfree=20480
```

### **ossfs挂载后，为什么通过df命令显示磁盘空间大小为256 TB？**

通过df命令显示的磁盘空间大小仅作为展示值，并不代表OSS存储空间实际容量。其中，Size（磁盘空间总大小）和Avail（磁盘空间剩余可用大小）固定为256 TB，Used（已使用磁盘空间大小）固定为0 TB。

OSS存储空间容量无限制，存储空间使用量取决于您的实际使用量。关于存储空间用量查询的更多信息，请参见 [查询Bucket级别的用量情况](https://help.aliyun.com/zh/oss/user-guide/view-the-resource-usage-of-a-bucket#concept-t4l-sxm-vdb "")。

### **通过cp命令拷贝数据时报错"input/output error"**![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5324459951/p36504.png)

**问题分析**：input/output error都是捕获到系统磁盘的错误而产生的报错，可以查看出现报错时，磁盘读写是否存在高负载的情况。

**解决方案**：可以增加分片参数，控制文件读写。使用ossfs -h命令可以查看分片参数。

### **使用rsync同步时报错"input/output error"**![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5324459951/p36509.png)

**问题分析**：ossfs与rsync同步使用本身会出现问题。此案例中，用户对一个141 GB的大文件进行cp操作，使磁盘读写处于非常高的负载状态，从而产生此报错。

**解决方案**：如果想要将OSS文件下载到本地ECS ，或者本地上传到ECS ，可以通过ossutil的分片上传、下载进行操作。

### **上传大文件时报错"there is no enough disk space for used as cache(or temporary)"**![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/5324459951/p36505.png)

- **问题原因**

磁盘空间小于`multipart_size * parallel_count`。

multipart\_size表示分片大小（默认单位为MB），parallel\_count表示并发上传分片数量（默认值为5）。

- **问题分析**

ossfs默认通过分片上传的方式上传大文件。上传时，ossfs会将临时缓存文件写入/tmp目录下，写入前需要先判断/tmp目录所在的磁盘可用空间是否小于`multipart_size * parallel_count`。如果磁盘可用空间大于`multipart_size * parallel_count`，则正常写入文件。如果磁盘可用空间小于`multipart_size * parallel_count`，则出现本地磁盘可用空间不足的报错。

例如，磁盘可用空间为300 GB，待上传的文件为200 GB，但multipart\_size设置为100000（100 GB），并发上传分片数量保持默认值5。此时，ossfs判断上传的文件大小为100 GB\*5=500 GB，超出本地磁盘可用空间。

- **解决方法**

在并发上传分片数量保持默认值5的情况下，设置合理的multipart\_size：

  - 如果磁盘可用空间为300 GB，待上传的文件为200 GB，则multipart\_size设置为20。

  - 如果磁盘可用空间为300 GB，待上传的文件为500 GB，则multipart\_size设置为50。

## **版本依赖问题**

### **安装ossfs时报错"fuse: warning: library too old, some operations may not work"**

**问题分析**：出现错误的原因是ossfs编译时所使用的libfuse版本比运行时链接到的libfuse版本高，这往往是用户自行安装了libfuse导致的。CentOS-5.x和CentOS-6.x系统中，阿里云提供的ossfs安装包里包含了libfuse-2.8.4，如果在运行的时候环境中有libfuse-2.8.3，并且ossfs被链接到了旧版本的fuse上，就会出现上述错误。

您可以通过ldd $(which ossfs) \| grep fuse命令确认ossfs运行时链接的fuse版本，如结果是/lib64/libfuse.so.2，那么通过ls -l /lib64/libfuse\*命令可以看到fuse的版本。

**解决方案**：让ossfs链接到正确的版本。

1. 通过rpm -ql ossfs \| grep fuse命令找到libfuse的目录。

2. 如果结果是/usr/lib/libfuse.so.2，则通过LD\_LIBRARY\_PATH=/usr/lib ossfs …命令运行ossfs。


### **安装依赖库fuse报错**![](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/4324459951/p36502.png)

**问题原因**：fuse的版本不满足ossfs的要求。

**解决方案**：手动下载fuse最新版本安装，不要使用yum安装。详情请参见 [fuse](https://github.com/libfuse/libfuse)。

### **使用Is列举文件时报错"Input/Output error"**

**问题原因**：该问题主要出现在CentOS环境，日志中报错`NSS error -8023`。ossfs在使用libcurl进行HTTPS通信时出现问题，可能是由于libcurl依赖的NSS（Network Security Services）库版本过低导致的。

**解决方案**：使用以下代码，升级NSS库至最新版本。

```shell
yum update nss
```

### **使用yum/apt-get安装ossfs时报错"conflicts with file from package fuse-devel"**

**问题分析**：系统中存在老版本的fuse，与ossfs里的依赖版本冲突。

**解决方案**：请先使用相关的包管理器卸载fuse，再重新安装ossfs。

## **其他问题**

### 在OSS文件数量较多或高并发场景下，使用ossfs挂载后出现卡顿的情况，有什么建议？

ossfs 1.0不建议在高并发场景下使用，若要在该场景下使用，可以参见以下方案：

- 方案一：使用ossfs 2.0挂载 。ossfs 2.0相较于ossfs 1.0在顺序读写和高并发小文件读取方面均实现了显著的性能提升。更多关于ossfs 2.0的性能信息，请参见 [性能提升](https://help.aliyun.com/zh/oss/developer-reference/ossfs-2-0/#dc6019791d3s0 "") 说明。

- 方案二：使用 [通过云存储网关挂载OSS](https://help.aliyun.com/zh/oss/user-guide/use-csg-to-attach-oss-buckets-to-ecs-instances#title-di5-dcv-1nf "")，性能更好。ossfs1.0工具的性能不适合处理高并发和大文件的上传与下载，适合用于日常的小文件操作。


### **使用ossfs上传到OSS的文件的Content-Type全是application/octet-stream**

**问题分析**：上传文件时，ossfs通过查询/etc/mime.types中的内容来设置文件的Content-Type。当该文件不存在时，默认设置为application/octet-stream。

**解决方案**：请检查这个文件是否存在，如果不存在，则需要添加。

- 通过命令自动添加mime.types文件

  - Ubuntu系统

    使用sudo apt-get install mime-support命令添加。

  - CentOS系统

    使用sudo yum install mailcap命令添加。
- 手动添加mime.types文件

1. 创建mime.types文件















     ```shell
     vi /etc/mime.types
     ```

2. 添加需要的格式，每种格式一行，每行格式为`application/javascript js`。

添加完成后，需要重新挂载OSS。

### **ossfs为什么将文件夹识别成普通文件**

- 情形一：


**问题分析**：创建文件夹对象（以`/`结尾的对象）时，content-type指定为text/plain，ossfs会将这个对象识别成普通文件。



**解决方案**：您可以挂载时加上-ocomplement\_stat参数。如果该文件夹对象大小为0或1，ossfs会将其识别成文件夹。

- 情形二：


**问题分析**：可以通过`ossutil stat 文件夹对象（以'/'结尾）`命令（例如：`ossutil stat oss://[bucket]/folder/`）。执行命令后：



1. 查看该对象的Content-Length字段，即对象的大小。如果对象大小非0，则会被识别成文件。

     **解决方案**：如果不再需要该文件夹对象的内容，可以通过`ossutil rm oss://[bucket]/folder/`命令删除该对象（不会影响文件夹下面的文件），或者通过ossutil上传一个大小为0的同名对象将其覆盖。

2. 如果对象大小为0，查看Content-Type字段，即对象属性，如果不是`application/x-directory`，`httpd/unix-directory`，`binary/octet-stream`或`application/octet-stream`，也会被识别成文件。

     **解决方案**：可以通过`ossutil rm oss://[bucket]/folder/`命令删除该对象（不会影响文件夹下面的文件）


### **ossfs执行mv操作失败**

**问题分析**：通过ossfs执行mv操作失败的可能原因是源文件为归档存储、冷归档存储或者深度冷归档存储类型文件。

**解决方案**：对归档存储、冷归档存储或者深度冷归档存储类型的文件执行mv操作前，您需要先解冻文件。具体步骤，请参见 [解冻文件](https://help.aliyun.com/zh/oss/user-guide/restore-objects-for-access#concept-wx5-szt-tdb "")。

### **ossfs是否支持在Windows环境中挂载存储空间？**

不支持。您可以在Windows环境下，通过以下两种方式挂载OSS存储空间。

- 通过云存储网关挂载存储空间。具体步骤，请参见 [通过云存储网关挂载OSS](https://help.aliyun.com/zh/oss/user-guide/use-csg-to-attach-oss-buckets-to-ecs-instances#task-1942033 "")。

- 通过Rclone挂载存储空间。具体步骤，请参见 [Rclone](https://help.aliyun.com/zh/oss/developer-reference/mount-oss-buckets-to-local-file-systems-by-using-amazon-s3-protocols#yI0Ux "")。


### ossfs是否支持将OSS存储空间挂载至多台Linux ECS服务器？

支持。您可以多次将其挂载至Linux ECS服务器中。具体步骤，请参见 [挂载存储空间](https://help.aliyun.com/zh/oss/developer-reference/advanced-configurations "")。

### **为什么用ossfs看到的文件信息（例如大小）与其他工具看到的不一致**

**问题分析**：ossfs默认会缓存文件的元数据（包括大小/权限等），这样就不需要每次ls的时候向OSS发送请求，加快速度。 如果用户通过其他程序（例如SDK/官网控制台/ossutil等）对文件进行了修改，由于缓存的关系，ossfs没有及时更新，导致与其他工具看到的文件信息不一致。

**解决方案**：可以在挂载的时候加上参数-omax\_stat\_cache\_size=0，禁用元数据缓存功能。每次执行 ls时，都会向OSS 发送请求，获取最新的文件信息。

### **为什么Bucket开启版本控制后出现挂载慢的问题？**

**问题原因**：ossfs默认通过调用ListObjects（GetBucket）列举文件。在Bucket开启版本控制，且Bucket中存在一个或者多个历史版本Object以及大量的过期删除标记的情况下，使用ListObjects（GetBucket）接口列举当前版本Object时会出现响应速度下降，从而影响ossfs挂载操作。

**解决方案**：使用-olistobjectsV2选项将ossfs切换至ListObjectsV2（GetBucketV2）接口，提升列举文件的性能。

### **如何设置通过HTTPS方式挂载？**

ossfs支持通过HTTPS方式挂载，以华东1（杭州）地域为例，挂载命令如下：

```shell
ossfs examplebucket /tmp/ossfs -o url=https://oss-cn-hangzhou.aliyuncs.com
```

### **目录下有非常多的文件时，为什么ls该目录很慢**

**问题分析**：假设一个目录下有N个文件，那么ls该目录至少需要N次OSS HTTP requests。在文件非常多的时候，这可能造成严重的性能问题。

**解决方案**： 通过`-omax_stat_cache_size=xxx`参数增大stat cache的size，这样第一次ls会较慢，但是后续的ls就快了，因为文件的元数据都在本地cache中。在1.91.1版本之前，这个值默认是1000；从1.91.1版本开始，这个值默认是100000，内存占用约几十MB，请根据您机器内存大小调整为合适的值。

### **卸载时报错"fusermount: failed to unmount /mnt/ossfs-bucket: Device or resource busy"**

**问题分析**：有进程正在访问挂载目录/mnt/ossfs-bucket下的文件 ，所以无法卸载。

**解决方案**：

1. 使用`lsof /mnt/ossfs-bucket`找出访问该目录的进程。

2. 使用kill命令强制关闭进程。

3. 使用`fusermount -u /mnt/ossfs-bucket`卸载Bucket。


### **使用ossfs 1.0时出现大量404日志**

**背景信息**：在使用 ossfs 1.0 的过程中，日志中出现的 404 Not Found 记录是常见现象。大多数情况下这并非系统错误，而是 ossfs 1.0为模拟本地文件系统语义所采取的正常交互行为。

在操作文件前，操作系统会主动检查目标对象是否存在。该过程可能导致向 OSS 发起大量探测请求，其中“对象不存在”的响应即返回404状态码。

ossfs 1.0检查对象存在性的完整流程如下：

1. 发送 HeadObject 请求查询指定路径（如 `object`）是否作为实际对象存在。

如果对象存在，则系统直接返回文件元信息；如果对象不存在，则系统返回404并继续执行下一步。

2. 收到404后，发送 HeadObject 请求查询`object/`对象是否存在。

如果对象存在，则系统直接返回文件元数据；如果对象不存在，则系统返回404并继续执行下一步。

3. 收到404后，发送 HeadObject 请求查询`object_$folder$`对象是否存在。

如果对象存在，则系统直接返回文件元信息；如果对象不存在，则系统返回404并继续执行下一步。

4. 收到404后，发送 ListObjects 请求判断指定路径是否为“目录”，即查询以` object/`为前缀的对象。

如果返回结果为空，则最终判定路径不存在；如果返回结果非空，则表示目录存在，系统列出目录内容。


**问题分析**：

- 使用 stat 等命令访问不存在的文件时，系统返回 404 并映射为本地文件系统的 No such file or directory 错误。

- 批量创建文件或目录前，操作系统会先检查目标文件是否存在，文件不存在时才发送创建请求。检查过程中产生的404错误属于预期行为，非系统异常。


**解决方案**：虽然 404 属于正常行为，但在高并发或批量操作场景下，频繁的探测请求会影响性能，可通过以下配置进行优化：

**重要**

配置相应选项后，在本地缓存失效前，ossfs 1.0无法感知OSS上文件的变化。

1. 通过调大`-o stat_cache_expire`和`-o max_stat_cache_size`延长元数据缓存时间以及提升缓存条目数量。

在元数据失效前查询文件或目录，可避免重复发起OSS请求。

   - `-o stat_cache_expire`：元数据缓存的过期时间，默认为900s。

   - `-o max_stat_cache_size`：元数据缓存的条目数量，默认为100000。
2. 如果使用的是ossfs 1.91.6之前的版本，请通过配置`-o enable_noobj_cache`启用负缓存（Negative Cache）。1.91.6及之后的版本默认已启用负缓存。

首次查询文件不存在时，将结果缓存在内存中。后续在缓存失效前查询文件时，直接查询本地负缓存而不发送OSS请求。



**说明**





ossfs 1.0的文件负缓存作为元数据缓存的一部分，失效时间可通过参数`-o stat_cache_expire`控制，缓存数量上限可通过参数`-o max_stat_cache_size`控制。