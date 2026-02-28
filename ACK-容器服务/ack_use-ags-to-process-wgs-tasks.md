### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/)

# 通过AGS处理全基因组测序WGS

更新时间：

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/kubernetes)

[我的收藏](https://help.aliyun.com/my_favorites.html)

该文章对您有帮助吗？

反馈

通过AGS可以快速处理全基因组测序WGS（Whole Genome Sequencing）的全流程任务，包括基因比对、排序、去重和变异检测。本文介绍如何通过AGS命令行管理WGS工作流。

## 前提条件

[开通服务](https://common-buy.aliyun.com/?commodityCode=csk_gspayasgo_public_cn#/buy)。

## 准备工作

完成权限的配置和数据的准备。

1. 配置AGS。

关于AGS的下载和安装，请参见 [AGS命令行帮助](https://help.aliyun.com/zh/ack/introduction-to-ags-cli#concept-525487 "")。


```plaintext
ags config init
```

2. 准备Bucket，并授权AGS服务读写权限和GetBucketInfo权限。







**说明**

   - 请确保指定Bucket的Owner是您当前的账号，否则建议您新建一个Bucket后再进行GetBucketInfo的授权。

   - 如果您使用的是RAM用户（子账号），需要为RAM用户（子账号）授予AliyunOSSFullAccess权限，请参见 [为RAM用户授权](https://help.aliyun.com/zh/ram/user-guide/grant-permissions-to-the-ram-user#task-187800 "")。

   - 如果您使用的是RAM用户（子账号），建议您重新创建OSS Bucket，以确保该账号是所使用Bucket的Owner。执行以下命令确认Bucket的Owner。


     ```plaintext
     ossutil stat oss://<your new bucket name>
     ```


```plaintext
Usage:
ags config oss <your bucket name>

e.g.
ags config oss my-test-shenzhen
```

3. 通过ossutil上传FASTQ数据到OSS Bucket。



关于ossutil的下载和安装，请参见 [安装ossutil](https://help.aliyun.com/zh/oss/developer-reference/install-ossutil#concept-303829 "")。









**说明**

目前只支持人类基因数据 WGS、WES等，暂不支持甲基化数据，以及动植物数据的比对。







   - 普通上传。


     ```plaintext
     Usage:

     ossutil cp -r <local dir of fastq> <path of  oss bucket >

     e. g.
     ossutil cp -r ./MGISEQ oss://my-test-shenzhen/MGISEQ
     ```

   - 大规模数据上传。

     按照如下示例成对整理样本，存放至不同的目录。


     ```plaintext
     ./samples
     ├── sample1
     │ ├── fastq_L1.tgz
     │ └── fastq_L2.tgz
     └── sample2
            ├── fastq_L1.tgz
            └── fastq_L2.tgz
     ```


     使用以下命令进行批量上传，`ossutil`命令支持断点续传。


     ```plaintext
     Usage:

     ossutil--recursivecp-r-u--parallel<numberofconcurrenttasks><localdiroffastqornfspath><pathofossbucket>

     e. g.
     ossutil --recursive cp -r -u  --parallel 16  ./samples  oss://mybucket/samples
     ```

## 启动WGS流程

关于参考基因组--reference，推荐和默认使用`hg19`基因组（hs37d5版本）。

**说明**

`hg19`基因组（hs37d5版本）主要有以下特点：

- 不包含ALT contigs

- Hard mask了chrY上的PARs区域

- 包含decoy contig


虽然AGS是ALT-Aware，可以识别并处理ALT contigs，而`UCSC hg19`基因组包含了ALT contigs，但是由于`UCSC hg19`基因组不具备后面两个特点，仍会造成变异检测的质量下降。详情参见 [Which human reference genome to use?](http://lh3.github.io/2017/11/13/which-human-reference-genome-to-use)。

```plaintext
Usage:

ags remote run wgs \
--region cn-shenzhen # region of oss, e.g. cn-shenzhen, cn-beijing and etc\
--fastq1 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_1.fq.gz # filename of fastq pair 2, fastq-path\filename \
--fastq2 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_2.fq.gz  # filename of fastq pair 1\
--bucket my-test-shenzhen # Bucket name\
--output-bam bam/MGISEQ_NA12878_hs37d5.bam, # Output BAM to bucket,  By default empty, non output of BAM \
--output-vcf vcf/MGISEQ_NA12878_hs37d5_5.vcf # Output filename \
--service "g" #SLA: [n:normal|s:silver|g:gold|p:platinum]\
--reference [hg19|hg38|<reference path on OSS>] # hg19: it is hs37d5 version, GRCh37/hg19 include decoy contig, no support for UCSC hg19. hg38: GRCh38/hg38 include decoy
--reference-group "\"@RG\\tID:TEST\\tSM:12878\\tPL:MGISEQ2000\"" # allow to specify reference groups for PL/SM/ID and etc
e.g.
ags remote run wgs \
--region cn-shenzhen \
--fastq1 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_1.fq.gz  \
--fastq2 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_2.fq.gz  \
--bucket my-test-shenzhen \
--output-vcf vcf/MGISEQ_NA12878_hs37d5_5.vcf \
--output-bam bam/MGISEQ_NA12878_hs37d5_5.bam \
--service "s" \
--reference hg19

### 批量多Lane多样本的下机样本的处理
MGISAMPLE001是一组WGS多Lane测序样本，可以通过指定样本目录--fastq1 MGISAMPLE001，--fastq2 MGISAMPLE001 实现对多Lane测序结果的合并和计算。
oss://my-test-shenzhen/MGISAMPLE001/L1/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_1.fq.gz
oss://my-test-shenzhen/MGISAMPLE001/L2/MGISEQ2000_PCR-free_NA12878_1_V100003043_L02_1.fq.gz
oss://my-test-shenzhen/MGISAMPLE001/L1/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_2.fq.gz
oss://my-test-shenzhen/MGISAMPLE001/L2/MGISEQ2000_PCR-free_NA12878_1_V100003043_L02_2.fq.gz

ags remote run wgs \
--region cn-shenzhen \
--fastq1 MGISAMPLE001 \
--fastq2 MGISAMPLE001 \
--bucket my-test-shenzhen \
--output-vcf vcf/MGISEQ_NA12878_hs37d5_6.vcf \
--output-bam bam/MGISEQ_NA12878_hs37d5_6.bam \
--service "g" \
--reference hg19

ags remote run wgs \
--region cn-shenzhen \
--fastq1 MGISAMPLE002 \
--fastq2 MGISAMPLE002 \
--bucket my-test-shenzhen \
--output-vcf vcf/MGISEQ_NA12878_hs37d5_7.vcf \
--output-bam bam/MGISEQ_NA12878_hs37d5_7.bam \
--service "g" \
--reference hg19
```

以下将为您演示如何通过命令调用AGS WGS。

![wgs.svg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9486769271/p862648.svg)

## 启动Mapping流程

通过--fastq1和--fastq2指定fastq，通过--output指定bam的输出路径。

```plaintext
Usage:

ags remote run mapping \
--region cn-shenzhen # region of oss, e.g. cn-shenzhen, cn-beijing and etc\
--fastq1 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_1.fq.gz # filename of fastq pair 2, fastq-path\filename \
--fastq2 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_2.fq.gz  # filename of fastq pair 1\
--bucket my-test-shenzhen # Bucket name\
--output-bam bam/MGISEQ_NA12878_hs37d5.bam # Output filename of BAM \
--service "g" #SLA: [n:normal|s:silver|g:gold|p:platinum]\
--markdup [true|false|default true] #Mark Duplicated, by default true
--reference [hg19|hg38|<reference path on OSS>]

e.g.

ags remote run mapping \
--region cn-shenzhen \
--fastq1 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_1.fq.gz  \
--fastq2 MGISEQ/MGISEQ2000_PCR-free_NA12878_1_V100003043_L01_2.fq.gz  \
--bucket my-test-shenzhen \
--output-bam bam/MGISEQ_NA12878_hs37d5.bam # Output filename of BAM \
--service "g" \
--markdup "true" \
--reference hg19

```

以下将为您演示如何通过命令调用AGS Mapping。

![mapping.svg](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/9486769271/p862652.svg)

## 列出远程流程

```plaintext
Usage:
ags remote list

e.g.
ags remtoe list
+---------------+-------------------------------+
|   JOB NAME    |          CREATE TIME          |
+---------------+-------------------------------+
| wgs-gpu-ckw96 | 2020-01-07 19:08:32 +0000 UTC |
| wgs-gpu-djzws | 2020-01-07 18:31:22 +0000 UTC |
| wgs-gpu-pd659 | 2020-01-03 20:34:09 +0000 UTC |
+---------------+-------------------------------+
```

## 获取流程的详细信息

```plaintext
Usage:
ags remote get <workflow id> --show
--show show detail of input parameters of workflow

e.g.
ags remote get wgs-gpu-sjtlw
+---------------+------------------+-----------+-------------------------------+----------+-------------------------------+
|   JOB NAME    |  JOB NAMESPACE   |  STATUS   |          CREATE TIME          | DURATION |          FINISH TIME          |
+---------------+------------------+-----------+-------------------------------+----------+-------------------------------+
| wgs-gpu-sjtlw | XXXXXXXXXXXXXXXX | Succeeded | 2020-01-07 21:38:05 +0800 CST | 12m25s   | 2020-01-07 21:50:30 +0800 CST |
+---------------+------------------+-----------+-------------------------------+----------+-------------------------------+

ags remote get wgs-gpu-97xfn --show

+---------------+------------------+-----------+-------------------------------+----------+-------------------------------+
|   JOB NAME    |  JOB NAMESPACE   |  STATUS   |          CREATE TIME          | DURATION |          FINISH TIME          |
+---------------+------------------+-----------+-------------------------------+----------+-------------------------------+
| wgs-gpu-sjtlw | XXXXXXXXXXXXXXXX | Succeeded | 2020-01-07 21:38:05 +0800 CST | 12m25s   | 2020-01-07 21:50:30 +0800 CST |
+---------------+------------------+-----------+-------------------------------+----------+-------------------------------+

+-----------------------+---------------------------------+
|      JOB DETAIL       |                                 |
+-----------------------+---------------------------------+
| wgs_reference_file    | hg19                          |
| wgs_service           | g                               |
| wgs_oss_region        | cn-shenzhen                     |
| wgs_fastq_first_name  | MGISAMPLE001                    |
| wgs_fastq_second_name | MGISAMPLE001                    |
| wgs_bucket_name       | my-test-shenzhen                |
| wgs_vcf_file_name     | vcf/MGISEQ_NA12878_hs37d5_6.vcf |
| wgs_bam_file_name     | bam/MGISEQ_NA12878_hs37d5_6.bam |
+-----------------------+---------------------------------+


```

## 取消运行中的工作流

```plaintext
Usage:

ags remote cancel  <workflow id>

e.g.

ags remote cancel wgs-gpu-zls6r
INFO[0000] Successed to cancel wgs-gpu-zls6r
```

## 删除结束的工作流

您可以删除成功和失败的工作流，但不能删除运行中的工作流。

```plaintext
Usage:

ags remote remove <workflow id>

e.g.

ags remote remove wgs-gpu-zls6r
INFO[0000] Successed to remove wgs-gpu-zls6r
```