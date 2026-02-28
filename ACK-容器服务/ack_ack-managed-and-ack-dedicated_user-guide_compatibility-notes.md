### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/)[ACK托管与专有集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/)[操作指南](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/)[安全沙箱](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/overview-10/)安全沙箱兼容性说明

# 安全沙箱在Pod层面的兼容字段

更新时间：2025-03-14 02:52:16

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：在安全沙箱容器中直接挂载NAS](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/mount-a-nas-file-system-to-a-sandboxed-container)[下一篇：Linux图形应用最佳实践](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/user-guide/best-practice-for-linux-graphics-applications)

该文章对您有帮助吗？

反馈

- 本页导读 （1）

Pod兼容字段列表

安全沙箱（runV）容器在创建时除了不支持Pod层面的个别字段之外，其他与runC容器一致，如Pod（Container） 网络、Service网络（ClusterIP、NodePort）、镜像等等。您在使用安全沙箱容器运行时，无需改变任何开发模式、镜像打包等。本文为您介绍安全沙箱运行时在Pod层面的字段兼容性。

## Pod兼容字段列表

| **字段** | **是否兼容** |
| --- | --- |

|     |     |
| --- | --- |
| **字段** | **是否兼容** |
| activeDeadlineSeconds | 兼容 |
| affinity | 兼容 |
| automountServiceAccountToken | 兼容 |
| containers | - 兼容字段<br>  <br>  args、command、env、envFrom、image、imagePullPolicy、lifecycle、livenessProbe、name、ports、readinessProbe、resources、startupProbe、stdin、stdinOnce、terminationMessagePath、terminationMessagePolicy、tty、volumeDevices、volumeMounts、workingDir、以及securityContext字段下的allowPrivilegeEscalation、capabilities、procMount、readOnlyRootFilesystem、runAsGroup、runAsNonRoot、runAsUser、seLinuxOptions<br>  <br>- 不兼容字段<br>  <br>  privileged、windowsOptions |
| dnsConfig | 兼容 |
| dnsPolicy | 兼容 |
| enableServiceLinks | 兼容 |
| hostAliases | 兼容 |
| hostIPC | 不兼容 |
| hostNetwork | 不兼容 |
| hostPID | 不兼容 |
| hostname | 兼容 |
| imagePullSecrets | 兼容 |
| initContainers | 兼容 |
| nodeName | 兼容 |
| nodeSelector | 兼容 |
| priority | 兼容 |
| priorityClassName | 兼容 |
| readinessGates | 兼容 |
| restartPolicy | 兼容 |
| runtimeClassName | 兼容 |
| schedulerName | 兼容 |
| securityContext | 兼容<br>该字段下的fsGroup、runAsGroup、runAsNonRoot、runAsUser、seLinuxOptions、supplementalGroups、sysctls字段也兼容。 |
| serviceAccount | 兼容 |
| serviceAccountName | 兼容 |
| shareProcessNamespace | 不兼容 |
| subdomain | 兼容 |
| terminationGracePeriodSeconds | 兼容 |
| tolerations | 兼容 |
| volumes | 兼容 |