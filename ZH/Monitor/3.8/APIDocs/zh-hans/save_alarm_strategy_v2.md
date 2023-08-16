
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/monitor_v3/save_alarm_strategy_v2/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

保存告警策略

### 请求参数



#### 接口参数
| 字段       | 类型    | 必选 | 描述                 |
| :--------- | ------- | ---- | -------------------- |
| actions    | list    | 是   | 动作列表(Action)     |
| bk_biz_id  | int     | 是   | 业务 ID               |
| detects    | list    | 是   | 检测配置列表(Detect)  |
| id         | int     | 否 | 策略 ID               |
| items      | list    | 是   | 监控项表(Item)       |
| labels     | list    | 是   | 策略标签列表          |
| name       | string  | 是   | 策略名称             |
| scenario   | string  | 是   | 监控对象             |
| source     | string  | 是   | 监控源              |
| is_enabled | bool | 否   | 是否开启，默认开启     |

#### actions

| 字段                              | 类型   | 必选 | 描述             |
| --------------------------------- | ------ | ---- | ---------------- |
| id                                | int    | 是   | 动作 id          |
| type                              | string | 是   | 动作类型(notice) |
| config                            | dict   | 是   | 动作配置         |
| config.alarm_end_time             | string | 是   | 通知时间段       |
| config.alarm_start_time           | string | 是   | 通知时间段       |
| config.send_recovery_alarm        | bool   | 是   | 是否发送恢复     |
| config.alarm_interval             | int    | 是   | 通知间隔         |
| notice_template                   | dict   | 否   | 通知配置         |
| notice_template.anomaly_template  | string | 否   | 异常通知模板     |
| notice_template.recovery_template | string | 否   | 恢复通知模板     |
| notice_group_ids                  | list   | 是   | 通知组 ID 列表     |

#### detects

| 字段                         | 类型   | 必选 | 描述             |
| ---------------------------- | ------ | ---- | ---------------- |
| id                           | int    | 是   | 检测 id         |
| level                        | int    | 是   | 告警级别         |
| expression                   | string | 是   | 计算公式         |
| trigger_config               | dict   | 是   | 触发条件配置     |
| trigger_config.count         | int    | 是   | 触发次数         |
| trigger_config.check_window  | int    | 是   | 触发周期         |
| recovery_config              | dict   | 是   | 恢复条件配置     |
| recovery_config.check_window | int    | 是   | 恢复周期         |
| connector                    | string | 是   | 同级别算法连接符 |

#### items

| 字段                         | 类型   | 必选 | 描述                      |
| ---------------------------- | ------ | ---- | ------------------------- |
| query_configs                | list   | 是   | 指标查询配置(QueryConfig) |
| id                           | string | 是   | 监控项配置 id              |
| name                         | string | 是   | 监控项名称                |
| expression                   | string | 是   | 计算公式                   |
| origin_sql                   | string | 是   | 源 sql                     |
| algorithms                   | list   | 是   | 算法配置列表(Algorithm)   |
| no_data_config               | dict   | 是   | 无数据配置                |
| no_data_config.is_enabled    | bool   | 是   | 是否开启无数据告警        |
| no_data_config.continuous    | int    | 否   | 无数据告警检测周期数      |
| target                       | list   | 是   | 监控目标                  |

#### iterms.target

| 字段                          | 类型   | 必选 | 描述                      |
| ---------------------------- | ------ | ---- | ----------------------- |
| field                        | string | 是   | 监控目标类型               |
| value                        | dict   | 是   | 监控目标数据项             |
| method                       | string | 是   | 监控目标方法               |

field - 根据目标节点类型和目标对象类型组合
host_target_ip
host_ip
host_topo
service_topo
service_service_template
service_set_template
host_service_template
host_set_template

#### items.target.value

| 字段        | 类型   | 必选 | 描述     |
| ----------- | ------ | ---- | -------- |
| ip          | string | 是   | 目标 ip   |
| bk_cloud_id | string | 是   | 云区域 id |

```json
{
  "target": [
    [
      {
        "field": "host_topo_node",
        "method": "eq",
        "value": [
          {
            "bk_inst_id": 7,
            "bk_obj_id": "biz"
          }
        ]
      }
    ]
  ]
}
```

#### queryconfigs

| 字段              | 类型   | 必选 | 描述         |
| ----------------- | ------ | ---- | ------------ |
| alias             | string | 是   | 别名         |
| data_source_label | string | 是   | 数据源标签   |
| data_type_label   | string | 是   | 数据类型标签 |

##### BkMonitorTimeSeries 类型

```json
{
  "data_source_label": "bk_monitor",
  "data_type_label": "time_series"
}
```

| 字段            | 类型   | 必选 | 描述     |
| --------------- | ------ | ---- | -------- |
| metric_field    | string | 是   | 指标     |
| unit            | string | 是   | 单位     |
| agg_condition   | list   | 是   | 查询条件 |
| agg_dimension   | list   | 是   | 聚合维度 |
| agg_method      | string | 是   | 聚合方法 |
| agg_interval    | int    | 是   | 聚合周期 |
| result_table_id | string | 是   | 结果表 ID |

##### BkMonitorLog 类型

```json
{
  "data_source_label": "bk_monitor",
  "data_type_label": "log"
}
```

| 字段            | 类型   | 必选 | 描述     |
| --------------- | ------ | ---- | -------- |
| agg_method      | string | 是   | 聚合方法 |
| agg_condition   | list   | 是   | 查询条件 |
| result_table_id | string | 是   | 结果表   |
| agg_interval    | int    | 是   | 聚合周期 |

##### BkMonitorEvent 类型

```json
{
  "data_source_label": "bk_monitor",
  "data_type_label": "event"
}
```

| 字段            | 类型   | 必选 | 描述     |
| --------------- | ------ | ---- | -------- |
| metric_field    | string | 是   | 指标     |
| agg_condition   | list   | 是   | 查询条件 |
| result_table_id | string | 是   | 结果表   |

##### BkLogSearchTimeSeries 类型

```json
{
  "data_source_label": "bk_log_search",
  "data_type_label": "time_series"
}
```

| 字段            | 类型   | 必选 | 描述     |
| --------------- | ------ | ---- | -------- |
| metric_field    | string | 是   | 指标     |
| index_set_id    | int    | 是   | 索引集 ID |
| agg_condition   | list   | 是   | 查询条件 |
| agg_dimension   | list   | 是   | 聚合维度 |
| agg_method      | string | 是   | 聚合方法 |
| result_table_id | string | 是   | 索引     |
| agg_interval    | int    | 是   | 聚合周期 |
| time_field      | string | 是   | 时间字段 |
| unit            | string | 是   | 单位     |

##### BkLogSearchLog 类型

```json
{
  "data_source_label": "bk_log_search",
  "data_type_label": "log"
}
```

| 字段            | 类型   | 必选 | 描述     |
| --------------- | ------ | ---- | -------- |
| index_set_id    | int    | 是   | 索引集 ID |
| agg_condition   | list   | 是   | 查询条件 |
| query_string    | int    | 是   | 查询语句 |
| agg_dimension   | list   | 是   | 聚合维度 |
| result_table_id | string | 是   | 索引     |
| agg_interval    | int    | 是   | 聚合周期 |
| time_field      | string | 是   | 时间字段 |

##### CustomEvent 类型

```json
{
  "data_source_label": "custom",
  "data_type_label": "event"
}
```

| 字段              | 类型   | 必选 | 描述           |
| ----------------- | ------ | ---- | -------------- |
| custom_event_name | string | 是   | 自定义事件名称 |
| agg_condition     | list   | 是   | 查询条件       |
| agg_interval      | int    | 是   | 聚合周期       |
| agg_dimension     | list   | 是   | 查询维度       |
| agg_method        | string | 是   | 聚合方法       |
| result_table_id   | string | 是   | 结果表 ID       |

##### CustomTimeSeries 类型

```json
{
  "data_source_label": "custom",
  "data_type_label": "time_series"
}
```
 | 字段            | 类型   | 必选 | 描述     |
| --------------- | ------ | ---- | -------- |
| metric_field    | string | 是   | 指标     |
| unit            | string | 是   | 单位     |
| agg_condition   | list   | 是   | 查询条件 |
| agg_dimension   | list   | 是   | 聚合维度 |
| agg_method      | string | 是   | 聚合方法 |
| agg_interval    | int    | 是   | 聚合周期 |
| result_table_id | string | 是   | 结果表 ID |

##### BkDataTimeSeries 类型

```json
{
  "data_source_label": "bk_data",
  "data_type_label": "time_series"
}
```

| 字段            | 类型   | 必选 | 描述     |
| --------------- | ------ | ---- | -------- |
| metric_field    | string | 是   | 指标     |
| unit            | string | 是   | 单位     |
| agg_condition   | list   | 是   | 查询条件 |
| agg_dimension   | list   | 是   | 聚合维度 |
| agg_method      | string | 是   | 聚合方法 |
| agg_interval    | int    | 是   | 聚合周期 |
| result_table_id | string | 是   | 结果表   |
| time_field      | string | 是   | 时间字段 |

#### algorithms

| 字段        | 类型   | 必选 | 描述         |
| ----------- | ------ | ---- | ------------ |
| config      | list   | 是   | 算法配置列表 |
| level       | int    | 是   | 告警级别     |
| type        | string | 是   | 算法类型     |
| unit_prefix | string | 否   | 算法单位前缀 |

#### 算法配置 config

##### 静态阈值 Threshold

```json
[
  {
    "method": "gt", // gt,gte,lt,lte,eq,neq
    "threshold": "1"
  }
]
```

##### 简单环比 SimpleRingRatio

```json
{
  "floor": "1",
  "ceil": "1"
}
```

##### 简单同比 SimpleYearRound

```json
{
  "floor": "1",
  "ceil": "1"
}
```

##### 高级环比 AdvancedRingRatio

```json
{
  "floor": "1",
  "ceil": "1",
  "floor_interval": 1,
  "ceil_interval": 1
}
```

##### 高级同比 AdvancedYearRound

与高级环比检测算法配置格式一致

##### 智能异常检测 IntelligentDetect

```json
{
  "sensitivity_value": 1 // 0-100
  "anomaly_detect_direct": "ceil" // "ceil", "floor", "all"(default)
}
```

##### 同比振幅 YearRoundAmplitude

```json
{
  "ratio": 1,
  "shock": 1,
  "days": 1,
  "method": "gte" // gt,gte,lt,lte,eq,neq
}
```

##### 同比区间 YearRoundRange

与同比振幅配置格式一致

##### 环比振幅 RingRatioAmplitude

```json
{
  "ratio": 1,
  "shock": 1,
  "days": 1,
  "threshold": 1
}
```

#### 示例数据

```json
{
    "bk_app_code": "xxx",
    "bk_app_secret": "xxxxx",
    "bk_token": "xxxx",
    "bk_biz_id": 7,
    "scenario": "os",
    "name": "进程端口",
    "labels": [],
    "is_enabled": true,
    "items": [
        {
            "name": "AVG(CPU使用率)",
            "no_data_config": {
                "continuous": 10,
                "is_enabled": false,
                "agg_dimension": [
                    "bk_target_ip",
                    "bk_target_cloud_id"
                ],
                "level": 2
            },
            "target": [],
            "expression": "a",
            "origin_sql": "",
            "query_configs": [
                {
                    "data_source_label": "bk_monitor",
                    "data_type_label": "time_series",
                    "alias": "a",
                    "result_table_id": "system.cpu_summary",
                    "agg_method": "AVG",
                    "agg_interval": 60,
                    "agg_dimension": [
                        "bk_target_ip",
                        "bk_target_cloud_id"
                    ],
                    "agg_condition": [],
                    "metric_field": "usage",
                    "unit": "percent",
                    "metric_id": "bk_monitor.system.cpu_summary.usage",
                    "index_set_id": "",
                    "query_string": "*",
                    "custom_event_name": "usage",
                    "functions": [],
                    "time_field": "time",
                    "bkmonitor_strategy_id": "usage",
                    "alert_name": "usage"
                }
            ],
            "algorithms": [
                {
                    "level": 1,
                    "type": "Threshold",
                    "config": [
                        [
                            {
                                "method": "gte",
                                "threshold": "80"
                            }
                        ]
                    ],
                    "unit_prefix": "%"
                }
            ]
        }
    ],
    "detects": [
        {
            "level": 1,
            "expression": "",
            "trigger_config": {
                "count": 1,
                "check_window": 5
            },
            "recovery_config": {
                "check_window": 5
            },
            "connector": "and"
        }
    ],
    "actions": [
        {
            "type": "notice",
            "config": {
                "alarm_start_time": "00:00:00",
                "alarm_end_time": "23:59:59",
                "alarm_interval": 1440,
                "send_recovery_alarm": false
            },
            "notice_group_ids": [
                11
            ],
            "notice_template": {
                "anomaly_template": "{{content.level}}\n{{content.begin_time}}\n{{content.time}}\n{{content.duration}}\n{{content.target_type}}\n{{content.data_source}}\n{{content.content}}\n{{content.current_value}}\n{{content.biz}}\n{{content.target}}\n{{content.dimension}}\n{{content.detail}}\n{{content.related_info}}",
                "recovery_template": ""
            }
        }
    ]
}
```

### 响应参数

| 字段    | 类型   | 描述         |
| ------- | ------ | ------------ |
| result  | bool   | 请求是否成功 |
| code    | int    | 返回的状态码 |
| message | string | 描述信息     |
| data    | dict   | 数据         |

#### 示例数据

```json
{
  "result": true,
  "code": 200,
  "message": "OK",
  "data": {data返回保存的策略结构，与请求参数一致（示例数据中省略）}
}
```