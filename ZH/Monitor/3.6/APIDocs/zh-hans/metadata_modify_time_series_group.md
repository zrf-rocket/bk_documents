
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/monitor_v3/metadata_modify_time_series_group/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

修改一个自定义时序分组 ID
给定一个自定义时序分组 ID，修改某些具体的信息

### 请求参数



#### 接口参数

| 字段           | 类型   | 必选 | 描述        |
| -------------- | ------ | ---- | ----------- |
| time_series_group_id  | int | 是   | 自定义时序组 ID |
| time_series_group_name | string | 是 | 自定义时序分组名 |
| label | string | 否 | 事件分组标签，用于表示自定义时序监控对象，应该复用【result_table_label】类型下的标签 |
| operator | string | 否 | 操作者 |
| metric_info_list | bool | 否 | 自定义时序列表 |
| is_enable | bool | 否 | 是否停用自定义时序组 |
| field_list | list | 否 | 字段列表 |

##### field_list 的具体参数说明

| 键值              | 类型   | 是否必选 | 默认值 | 描述                                                |
| ----------------- | ------ | -------- | ------ | --------------------------------------------------- |
| field_name        | string | 是       | -      | 字段名                                              |
| field_type        | string | 是       | -      | 字段类型，可以为 float, string, boolean 和 timestamp   |
| description       | string | 否       | ""     | 字段描述信息                                        |
| tag               | string | 是       | -      | 字段标签，可以为 metric, dimemsion, timestamp, group |
| alias_name        | string | 否       | None   | 入库别名                                            |
| option            | string | 否       | {}     | 字段选项配置，键为选项名，值为选项配置              |
| is_config_by_user | bool   | 是       | true   | 用户是否启用该字段配置                              |

#### 请求示例

```json
{
    "bk_app_code": "xxx",
  	"bk_app_secret": "xxxxx",
  	"bk_token": "xxxx",
	"time_series_group_id": 123,
	"time_series_group_name": "自定义时序开发",
	"operator": "system",
	"description": "what the group use for.",
	"is_enable": true,
	"field_list": [{
		"filed_name": "usage",
		"field_type": "double",
		"description": "field description",
		"tag": "metric",
        "alias_name": "usage_alias",
		"option": [],
		"is_config_by_user": true
	}]
}
```

### 返回结果

| 字段       | 类型   | 描述         |
| ---------- | ------ | ------------ |
| result     | bool   | 请求是否成功 |
| code       | int    | 返回的状态码 |
| message    | string | 描述信息     |
| data       | dict   | 数据         |
| request_id | string | 请求 ID       |

#### data 字段说明

| 字段                   | 类型   | 描述             |
| ---------------------- | ------ | ---------------- |
| time_series_group_id   | int    | 新建的时序分组 ID |
| time_series_group_name | string | 时序分组名称     |
| bk_data_id             | int    | 数据源 id         |
| bk_biz_id              | int    | 业务 id           |
| table_id               | string | 结果表 ID         |
| label                  | string | 事件标签         |
| is_enable              | bool   | 是否启用         |
| creator                | string | 创建人           |
| create_time            | string | 创建时间         |
| last_modify_user       | string | 最后更新人       |
| last_modify_time       | string | 最后更新时间     |
| metric_info_list       | list   | 自定义时序列表   |

#### metric_info_list 具体内容说明

| 字段        | 类型   | 描述     |
| ----------- | ------ | -------- |
| field_name  | string | 字段名   |
| description | string | 字段描述 |
| unit        | string | 单位     |
| type        | string | 字段类型 |
| tag_list    | list   | 维度列表 |

#### metric_info_list.tag_list 具体内容说明

| 字段        | 类型   | 描述     |
| ----------- | ------ | -------- |
| field_name  | string | 字段名   |
| description | string | 字段描述 |
| unit        | string | 单位     |
| type        | string | 字段类型 |

#### 结果示例

```json
{
    "message":"OK",
    "code":200,
    "data": [{
        'time_series_group_id': 1,
        'time_series_group_name': 'bkunifylogbeat common metrics',
        'bk_data_id': 1100006,
        'bk_biz_id': 0,
        'table_id': 'bkunifylogbeat_common.base',
        'label': 'service_process',
        'is_enable': True,
        'creator': 'system',
        'create_time': '2021-12-07 03:29:51',
        'last_modify_user': 'system',
        'last_modify_time': '2021-12-07 03:29:51',
        "metric_info_list": [{
            "field_name": "mem_usage",
            "description": "mem_usage_2",
            "unit": "M",
            "type": "double",
            "tag_list": [
                {
                    "field_name": "test_name",
                    "description": "test_name_2",
                    "unit": "M",
                    "type": "double",
                }
            ]
        },{
            "field_name": "cpu_usage",
            "description": "mem_usage_2",
            "unit": "M",
            "type": "double",
            "tag_list": [
                {
                    "field_name": "test_name",
                    "description": "test_name_2",
                    "unit": "M",
                    "type": "double",
                }
            ]
        }]
    }],
    "result":true,
    "request_id":"408233306947415bb1772a86b9536867"
}
```