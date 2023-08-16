
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/monitor_v3/search_event/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

查询事件

### 请求参数



#### 接口参数

| 字段       | 类型   | 必选 | 描述                                                         |
| ---------- | ------ | ---- | ------------------------------------------------------------ |
| bk_biz_ids | list   | 是   | 业务 ID 列表                                                   |
| time_range | string | 否   | 事件结束的时间范围，格式为：2020-02-26 00:00:00 -- 2020-02-28 23:59:59 |
| days       | int    | 否   | 查询最近几天内的时间，这个参数存在，time_range 则失效         |
| conditions | list   | 否   | 查询条件                                                     |
| page       | int | 否 | 第几页，不传则不分页 |
| page_size | int | 否 | 每页数量，默认 100 |

> 需要注意的是，当前未恢复的事件不受时间条件的约束，也就是无论选择什么时间范围，当前的未恢复的事件都会被查出来，除非使用 conditions 进行事件状态过滤。

#### conditions

conditions 用于按事件相关的其他字段过滤事件，由 key,value 组成，意味着过滤出 key 字段在 value 列表中事件。

如下列匹配条件，表示筛选出事件状态为“已恢复”的事件。

```json
[
  {
    "key":"event_status",
    "value":["RECOVERED"]
  }
]
```

可用的字段有：

1. strategy_id - 事件关联的策略 ID

2. id - 事件 ID

3. level - 告警级别

   1. 1 - 致命
   2. 2 - 预警
   3. 3 - 提醒

4. event_status - 事件状态

   1. ABNORMAL - 未恢复
   2. CLOSED - 已关闭
   3. RECOVERED - 已恢复

5. data_source - 数据来源及类型

   是由 `|`分隔的字符串，左边为数据来源，右边为数据类型，比如`bk_monitor|time_series`

   数据来源有：

   1. bk_monitor - 监控采集
   2. bk_data - 数据平台
   3. bk_log_search - 日志检索
   4. custom - 用户自定义

   数据类型有:

   1. time_series - 时序数据
   2. event - 事件
   3. log - 日志关键字

#### 示例数据

```json
{
    "bk_app_code": "xxx",
    "bk_app_secret": "xxxxx",
    "bk_token": "xxxx",
    "bk_biz_ids":[2],
    "time_range":"2020-02-26 00:00:00 -- 2020-02-28 23:59:59",
    "conditions":[
        {
            "key":"event_status",
            "value":[
                "RECOVERED"
            ]
        },
        {
            "key":"data_source",
            "value":[
                "bk_monitor|time_series"
            ]
        }
    ],
    "page": 1,
    "page_size": 100
}
```

### 响应参数

| 字段    | 类型   | 描述         |
| ------- | ------ | ------------ |
| result  | bool   | 请求是否成功 |
| code    | int    | 返回的状态码 |
| message | string | 描述信息     |
| data    | list   | 数据         |

#### data 字段说明

| 字段          | 类型   | 描述                                                         |
| ------------- | ------ | ------------------------------------------------------------ |
| bk_biz_id     | int    | 业务 ID                                                       |
| is_ack        | bool   | 是否确认                                                     |
| level         | int    | 告警级别，1(执行) 2(预警) 3(提醒)                            |
| origin_alarm  | dict   | 事件产生时的异常点数据                                       |
| origin_config | dict   | 事件产生时的告警策略配置，数据请参考告警策略 api 相关文档      |
| strategy_id   | int    | 告警策略 ID                                                   |
| id            | int    | 事件表自增 ID                                                 |
| is_shielded   | bool   | 是否在屏蔽中                                                 |
| event_id      | string | 异常事件 ID                                                   |
| status        | int    | 事件状态，ABNORMAL(未恢复) CLOSED(已关闭) RECOVERED(已恢复)  |
| create_time   | string | 产生事件的时间，格式为 yyyy-mm-dd hh:mm:ss                    |
| begin_time    | string | 该事件关联的第一个异常点的创建时间，格式为 yyyy-mm-dd hh:mm:ss |
| end_time      | string | 事件结束时间，格式为 yyyy-mm-dd hh:mm:ss                      |
| target_key    | string | 事件目标，不存在则为空字符串                                 |
| p_event_id    | string | 父事件 ID，默认为空                                           |

#### target key

表示当前事件对应的监控目标，数据格式如下：

- 主机: host|ip|bk_cloud_id
    eg: host|10.0.0.1|0
- 服务实例: service|bk_target_service_instance_id
    eg: service|13
- 拓扑节点: topo|bk_obj_id|$bk_inst_id
    eg: topo|biz|2
- 无: ""

#### origin_alarm

表示事件发生时的异常点数据

| 字段                    | 类型   | 描述           |
| ----------------------- | ------ | -------------- |
| data                    | dict   | 数据           |
| data.dimensions         | dict   | 数据维度       |
| data.values             | dict   | 异常点的值     |
| data.time               | int    | 异常点的时间戳 |
| dimension_translation   | dict   | 维度展示信息   |
| anomaly                 | dict   | 异常信息       |
| anomaly.key             | string | 告警级别       |
| anomaly.anomaly_message | string | 异常描述       |
| anomaly.anomaly_time    | string | 异常时间       |
| anomaly.anomaly_id      | string | 异常地点 ID     |

#### origin_alarm.dimension_translation - 维度展示信息

将维度翻译成给用户展示的内容，与 data.dimensions 的信息对应

1. display_name - 维度名称
2. display_value - 维度的值
3. value - 维度的原始值

```json
{
  "bk_topo_node":{
    "display_name":"bk_topo_node",
    "display_value":[
      {
        "bk_obj_name":"集群",
        "bk_inst_name":"空闲机池"
      },
      {
        "bk_obj_name":"业务",
        "bk_inst_name":"蓝鲸"
      },
      {
        "bk_obj_name":"模块",
        "bk_inst_name":"空闲机"
      }
    ],
    "value":[
      "set|2",
      "biz|2",
      "module|3"
    ]
  },
  "bk_target_cloud_id":{
    "display_name":"bk_target_cloud_id",
    "display_value":0,
    "value":0
  },
  "bk_target_ip":{
    "display_name":"bk_target_ip",
    "display_value":"10.0.0.1",
    "value":"10.0.0.1"
  }
}
```

#### 示例数据

```json
{
    "code": 200,
    "result": true,
    "message": "ok",
    "data": [
        {
            "status": "ABNORMAL",
            "bk_biz_id": 2,
            "is_ack": false,
            "level": 1,
            "origin_alarm": {
                "data": {
                    "record_id": "d751713988987e9331980363e24189ce.1574439900",
                    "values": {
                        "count": 10,
                        "dtEventTimeStamp": 1574439900
                    },
                    "dimensions": {},
                    "value": 10,
                    "time": 1574439900
                },
                "trigger": {
                    "level": "1",
                    "anomaly_ids": [
                        "d751713988987e9331980363e24189ce.1574439660.88.118.1",
                        "d751713988987e9331980363e24189ce.1574439720.88.118.1",
                        "d751713988987e9331980363e24189ce.1574439780.88.118.1",
                        "d751713988987e9331980363e24189ce.1574439840.88.118.1",
                        "d751713988987e9331980363e24189ce.1574439900.88.118.1",
                        "d751713988987e9331980363e24189ce.1574439960.88.118.1",
                        "d751713988987e9331980363e24189ce.1574440020.88.118.1",
                        "d751713988987e9331980363e24189ce.1574440080.88.118.1",
                        "d751713988987e9331980363e24189ce.1574440140.88.118.1"
                    ]
                },
                "anomaly": {
                    "1": {
                        "anomaly_message": "count >= 1.0, 当前值10.0",
                        "anomaly_time": "2019-11-22 16:31:06",
                        "anomaly_id": "d751713988987e9331980363e24189ce.1574439900.88.118.1"
                    }
                },
                "dimension_translation": {},
                "strategy_snapshot_key": "bk_bkmonitor.ee.cache.strategy.snapshot.88.1574411061"
            },
            "target_key": "",
            "strategy_id": 88,
            "id": 1364253,
            "is_shielded": false,
            "event_id": "d751713988987e9331980363e24189ce.1574439660.88.118.1",
            "create_time": "2019-11-22 16:31:07",
            "end_time": null,
            "begin_time": "2019-11-22 16:25:00",
            "origin_config": {},
            "p_event_id": ""
        }
    ]
}
```