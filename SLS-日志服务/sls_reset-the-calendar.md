### 关注阿里云

关注阿里云公众号或下载阿里云APP，关注云资讯，随时随地运维管控云服务

![阿里云APP](https://img.alicdn.com/imgextra/i4/O1CN01XLesV31fkf7pYNATb_!!6000000004045-2-tps-400-400.png)![阿里云微信](https://img.alicdn.com/tfs/TB1AOdINW6qK1RjSZFmXXX0PFXa-258-258.jpg)

联系我们：4008013260

[首页](https://help.aliyun.com/) [日志服务](https://help.aliyun.com/zh/sls/)[数据监控](https://help.aliyun.com/zh/sls/data-monitoring/)[告警](https://help.aliyun.com/zh/sls/sls-alerting/)[通知策略](https://help.aliyun.com/zh/sls/notification-management/)[日历与值班](https://help.aliyun.com/zh/sls/calendar-and-duty/)日历重置机制

# 日历重置机制

更新时间：2024-07-22 05:42:27

复制为 MD 格式

[产品详情](https://www.aliyun.com/product/sls)

[我的收藏](https://help.aliyun.com/my_favorites.html)

[上一篇：修改全局默认日历](https://help.aliyun.com/zh/sls/modify-the-global-default-calendar)[下一篇：轮岗与代班场景](https://help.aliyun.com/zh/sls/rotating-shifts-and-substitute-shifts)

该文章对您有帮助吗？

反馈

日志服务全局默认日历支持重置，用于修改日期的默认属性（节假日、工作时间段等）。

例如2024年7月24日~2024年7月26日为公司A的团建日，则公司工作人员可在全局默认日历中将这3天重置为节假日。重置日历后，可基于该日历进行告警通知。

**说明**

- 重置日历后的日期属性的优先级高于默认属性。例如2024年9月16日为节假日，而您重置为工作日，则日志服务告警系统默认该天为工作日。

- 如果某个日期被多次重置，则以最后一次为准。例如您将2024年9月12日~2024年9月14日重置为节假日，又将2024年9月13日重置为工作日。则最终结果是2024年9月12日、2024年9月14日为节假日，2024年9月13日为工作日。


![image](https://help-static-aliyun-doc.aliyuncs.com/assets/img/zh-CN/6431461271/p823981.png)