## 1. 接口描述

云数据库SQL Server是腾讯云基于微软公司推出的SQL Server专业打造的云数据库。具体介绍请参考<a href="/doc/product/238/产品概述" title="产品概述">云数据库SQL Server</a>页面。
查询云数据库SQL Server产品监控数据，入参取值如下：

namespace: qce/sqlserver
维度名称取值：resourceId 
dimensions.0.name=resourceId 
dimensions.0.value为实例的资源 Id

## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href="/doc/api/405/公共请求参数" title="公共请求参数">公共请求参数</a>页面。其中，此接口的Action字段为GetMonitorData。


<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> namespace
<td> 是
<td> String
<td> 命名空间，参见第一小节
<tr>
<td> metricName
<td> 是
<td> String
<td> 指标名称，具体名称见第5小节
<tr>
<td> dimensions.n.name
<td> 是
<td> String
<td> 维度的名称，具体维度名称见第5小节各产品监控指标列表，与dimensions.n.value配合使用。
<tr>
<td> dimensions.n.value
<td> 是
<td> String
<td> 对应的维度的值，具体维度名称见第5小节各产品监控指标列表，与dimensions.n.name配合使用。
<tr>
<td> period
<td> 否
<td> Int
<td> 监控统计周期。默认为取值为300，单位为s。目前CVM支持60s、300s粒度，其他产品支持仅300s。后续将逐步支持更多产品。
<tr>
<td> startTime
<td> 否
<td> Datetime
<td> 起始时间，如”2016-01-01 10:25:00”。 默认时间为当天的”00:00:00”
<tr>
<td> endTime
<td> 否
<td> Datetime
<td> 结束时间，默认为当前时间。 endTime不能小于startTime
</tbody></table>



## 3. 输出参数

<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> code
<td> Int
<td> 错误码, 0: 成功, 其他值表示失败
<tr>
<td> message
<td> String
<td> 返回信息
<tr>
<td> startTime
<td> Datetime
<td> 起始时间
<tr>
<td> endTime
<td> Datetime
<td> 结束时间
<tr>
<td> metricName
<td> String
<td> 指标名称
<tr>
<td> period
<td> Int
<td> 监控统计周期，单位为s
<tr>
<td> dataPoints
<td> Array
<td> 监控数据列表
</tbody></table>


## 4. 错误码表

| 错误代码 | 错误描述    | 英文描述                                 |
| ---- | ------- | ------------------------------------ |
| -502 | 资源不存在   | OperationDenied.SourceNotExists      |
| -503 | 请求参数有误  | InvalidParameter                     |
| -505 | 参数缺失    | InvalidParameter.MissingParameter    |
| -507 | 超出限制    | OperationDenied.ExceedLimit          |
| -509 | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513 | DB操作失败  | InternalError.DBoperationFail        |


## 5. 指标列表

**metricName可选取值范围**

| 指标名称                   | 含义                    | 单位   | 维度         |
| ---------------------- | --------------------- | ---- | ---------- |
| cpu                    | 实例CPU消耗的百分比           | %    | resourceId |
| transactions           | 平均每秒的事务数              | 次/秒  | resourceId |
| connections            | 平均每秒用户连接数据库的个数        | 个    | resourceId |
| requests               | 每秒请求次数                | 次/秒  | resourceId |
| logins                 | 每秒登录次数                | 次/秒  | resourceId |
| logouts                | 每秒登出次数                | 次/秒  | resourceId |
| storage                | 实例数据库文件和日志文件占用的空间总和   | GB   | resourceId |
| in_flow                | 所有连接输入包大小总和           | MB/s | resourceId |
| out_flow               | 所有连接输出包大小总和           | MB/s | resourceId |
| iops                   | 磁盘读写次数                | 次/秒  | resourceId |
| disk_reads             | 每秒读取磁盘次数              | 次/秒  | resourceId |
| disk_writes            | 每秒写入磁盘次数              | 次/秒  | resourceId |
| slow_queries           | 运行时间超过1秒的查询数量         | 个    | resourceId |
| blocks_processes       | 当前阻塞数量                | 个    | resourceId |
| lock_requests          | 平均每秒锁请求的次数            | 次/秒  | resourceId |
| user_errors            | 平均每秒错误数               | 次/秒  | resourceId |
| sql_compilations       | 平均每秒SQL编译次数           | 次/秒  | resourceId |
| sql_recompilations     | 平均每秒SQL重编译次数          | 次/秒  | resourceId |
| full_scans             | 每秒不受限制的完全扫描数          | 次/秒  | resourceId |
| buffer_cache_hit_ratio | 数据缓存（内存）命中率           | %    | resourceId |
| latch_waits            | 每秒闩锁等待数量              | 次/秒  | resourceId |
| lock_waits             | 每个导致等待的锁请求的平均等待时间     | ms   | resourceId |
| network_io_waits       | 平局网络IO延迟时间            | ms   | resourceId |
| plan_cache_hit_ratio   | 每个SQL有一个执行计划，执行计划的命中率 | %    | resourceId |

## 6. 示例

**读取云数据库SQL Server监控指标示例**

输入

<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&<<a href="https://www.qcloud.com/doc/api/229/6976">公共请求参数</a>>
&namespace=qce/sqlserver
&metricName=cpu
&dimensions.0.name=resourceId
&dimensions.0.value=mssql-dh01nvsb
&startTime=2016-06-28 14:10:00
&endTime=2016-06-28 14:20:00
</pre>

输出

```
{
	"code": 0,
	"message": "",
	"metricName": "cpu",
	"startTime": "2016-06-28 14:10:00",
	"endTime": "2016-06-28 14:20:00",
	"period": 300,
	"dataPoints": [
		50,
		44
	]
}
```