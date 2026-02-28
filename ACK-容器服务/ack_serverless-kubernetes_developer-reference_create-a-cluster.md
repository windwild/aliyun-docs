### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [容器服务 Kubernetes 版 ACK](https://help.aliyun.com/zh/ack/) [ACK Serverless集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/) [开发参考](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/) [CLI参考](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/cli-reference/) 创建集群

# 创建集群

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：查看集群](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/view-cluster)[下一篇：删除集群实例](https://help.aliyun.com/zh/ack/serverless-kubernetes/developer-reference/deleting-a-cluster-1)

该文章对您有帮助吗？

反馈

创建一个新的集群实例，并新建指定数量的节点。

关于该命令的详细参数说明，请参见API文档 [CreateCluster - 创建集群](https://help.aliyun.com/zh/ack/ack-managed-and-ack-dedicated/developer-reference/api-cs-2015-12-15-createcluster "")。

## API请求响应

请求格式

```plaintext
aliyun cs  POST /clusters --region=${regionId} --header "Content-Type=application/json" --body "$(cat create.json)"
```

参数说明：

- `--header`：需要指定Content-Type为application/json。

- `--region`：集群所在的地域。

- `--body`：是要发送给服务端的body内容，可以从本地文件读取，需要是有效的JSON格式。`create.json`的内容如下所示。


请求示例：

- **Kubernetes集群**



```plaintext
{
      "cluster_type":"Kubernetes",
      "name":"webService",
      "region_id":"cn-beijing",
      "disable_rollback":true,
      "timeout_mins":60,
      "kubernetes_version":"1.14.8-aliyun.1",
      "snat_entry":true,
      "endpoint_public_access":true,
      "ssh_flags":true,
      "cloud_monitor_flags":true,
      "deletion_protection":false,
      "node_cidr_mask":"26",
      "proxy_mode":"ipvs",
      "tags":[],
      "addons":[{"name":"flannel"},{"name":"arms-prometheus"},{"name":"flexvolume"},{"name":"alicloud-disk-controller"},{"name":"logtail-ds","config":"{"IngressDashboardEnabled":"false"}"},{"name":"ack-node-problem-detector","config":"{"sls_project_name":""}"},{"name":"nginx-ingress-controller","config":"{"IngressSlbNetworkType":"internet"}"}],
      "os_type":"Linux",
      "platform":"CentOS",
      "node_port_range":"30000-32767",
      "key_pair":"sian-sshkey",
      "cpu_policy":"none",
      "master_count":3,
      "master_vswitch_ids":["vsw-2zete8s4qocqg0mf6****","vsw-2zete8s4qocqg0mf6****","vsw-2zete8s4qocqg0mf6****"],
      "master_instance_types":["ecs.n4.large","ecs.n4.large","ecs.n4.large"],
      "master_system_disk_category":"cloud_ssd",
      "master_system_disk_size":120,
      "runtime":{"name":"docker","version":"18.09.2"},
      "worker_instance_types":["ecs.i1.xlarge"],
      "num_of_nodes":1,
      "worker_system_disk_category":"cloud_efficiency",
      "worker_system_disk_size":120,
      "vpcid":"vpc-2zecuu62b9zw7a7q****",
      "worker_vswitch_ids":["vsw-2zete8s4qocqg0mf6****"],
      "container_cidr":"172.20.0.0/16",
      "service_cidr":"172.21.0.0/20"
}
```





请求示例补充说明



```plaintext
如果是terway网络类型的集群，"pod_vswitch_ids"为必填参数，请求入参示例如下。
{
      "cluster_type":"Kubernetes",
      "name":"webService-terway",
      "region_id":"cn-beijing",
      "disable_rollback":true,
      "timeout_mins":60,
      "kubernetes_version":"1.14.8-aliyun.1",
      "snat_entry":true,
      "endpoint_public_access":true,
      "ssh_flags":true,"cloud_monitor_flags":true,
      "deletion_protection":false,
      "proxy_mode":"ipvs",
      "tags":[],
      "addons":[{"name":"terway-eni"},{"name":"flexvolume"},{"name":"alicloud-disk-controller"},{"name":"logtail-ds","config":"{\"IngressDashboardEnabled\":\"false\"}"},{"name":"ack-node-problem-detector","config":"{\"sls_project_name\":\"\"}"},{"name":"nginx-ingress-controller","config":"{\"IngressSlbNetworkType\":\"internet\"}"}],
      "os_type":"Linux",
      "platform":"CentOS",
      "node_port_range":"30000-32767",
      "pod_vswitch_ids":["vsw-2zete8s4qocqg0mf6****"],
      "key_pair":"sian-sshkey",
      "cpu_policy":"none",
      "master_count":3,
      "master_vswitch_ids":["vsw-2zed90q9inwtuyfzd****","vsw-2zed90q9inwtuyfzd****","vsw-2zed90q9inwtuyfzd****"],
      "master_instance_types":["ecs.i1.4xlarge","ecs.i1.4xlarge","ecs.i1.4xlarge"],
      "master_system_disk_category":"cloud_ssd",
      "master_system_disk_size":120,
      "runtime":{"name":"docker","version":"18.09.2"},
      "worker_instance_types":["ecs.i1.4xlarge"],
      "num_of_nodes":1,
      "worker_system_disk_category":"cloud_efficiency",
      "worker_system_disk_size":120,
      "vpcid":"vpc-2zecuu62b9zw7a7q****",
      "worker_vswitch_ids":["vsw-2zed90q9inwtuyfzd****"],
      "is_enterprise_security_group":true,
      "service_cidr":"172.21.0.0/20"
}
```

- **托管Kubernetes集群**



```plaintext
{
      "name":"amk-cluster",
      "cluster_type":"ManagedKubernetes",
      "disable_rollback":true,
      "timeout_mins":60,
      "kubernetes_version":"1.16.9-aliyun.1",
      "region_id":"cn-beijing",
      "snat_entry":true,
      "cloud_monitor_flags":true,
      "endpoint_public_access":true,
      "deletion_protection":true,
      "node_cidr_mask":"26",
      "proxy_mode":"ipvs",
      "tags":[\
          {\
              "key":"tier",\
              "value":"backend"\
          }\
      ],
      "addons":[{"name":"flannel"},{"name":"csi-plugin"},{"name":"csi-provisioner"},{"name":"logtail-ds","config":"{\"IngressDashboardEnabled\":\"true\"}"},{"name":"ack-node-problem-detector","config":"{\"sls_project_name\":\"\"}"},{"name":"nginx-ingress-controller","config":"{\"IngressSlbNetworkType\":\"internet\"}"},{"name":"arms-prometheus"}],
      "os_type":"Linux",
      "platform":"CentOS",
      "runtime":{
          "name":"docker",
          "version":"19.03.5"
      },
      "worker_instance_types":[\
          "ecs.i2.2xlarge"\
      ],
      "num_of_nodes":3,
      "worker_system_disk_category":"cloud_efficiency",
      "worker_system_disk_size":120,
      "worker_data_disks":[\
          {\
              "category":"cloud_efficiency",\
              "size":"40",\
              "encrypted":"true",\
              "auto_snapshot_policy_id":""\
          }\
      ],
      "worker_instance_charge_type":"PrePaid",
      "worker_period_unit":"Month",
      "worker_period":1,
      "worker_auto_renew":true,
      "worker_auto_renew_period":1,
      "vpcid":"vpc-2zemm8mo5rmdppgqm****",
      "container_cidr":"172.20.0.0/16",
      "service_cidr":"172.21.0.0/20",
      "vswitch_ids":[\
          "vsw-2zej67xyhh61oqn7i****"\
      ],
      "login_password":"Hello1234",
      "logging_type":"SLS",
      "cpu_policy":"none",
      "taints":[\
          {\
              "key":"key1",\
              "value":"value1",\
              "effect":"NoSchedule"\
          }\
      ],
      "security_group_id":"sg-2zeg3u73kkhtixda****"
}
```

- **ACK Serverless集群**



```plaintext
{
      "cluster_type":"Ask",
      "name":"ask-cluster",
      "kubernetes_version":"1.16.9-aliyun.1",
      "region_id":"cn-shenzhen",
      "endpoint_public_access":true,
      "private_zone":true,
      "tags":[\
          {\
              "key":"tier",\
              "value":"frontend"\
          }\
      ],
      "deletion_protection":true,
      "addons":[\
          {\
              "name":"logtail-ds"\
          }\
      ],
      "zone_id":"cn-shenzhen-a",
      "vpc_id":"vpc-wz984yvbd6lck22z3****",
      "vswitch_ids":[\
          "vsw-wz9uwxhawmtzg7u9h****"\
      ],
      "logging_type":"SLS",
      "security_group_id":"sg-wz9b86l4s7nthi1k****"
}
```


响应结果

```plaintext
{
    "cluster_id": "c61cf530524474386a7ab5a1c192****",
    "request_id": "348D4C9C-9105-4A1B-A86E-B58F0F875575",
    "task_id": "T-5ad724ab94a2b109e8000004"
}
```