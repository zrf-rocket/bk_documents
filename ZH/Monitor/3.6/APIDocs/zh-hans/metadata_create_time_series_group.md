
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/monitor_v3/metadata_create_time_series_group/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

创建一个自定义时序分组 ID
给定一个数据源和业务，创建一个归属的自定义时序分组 ID

### 请求参数



#### 接口参数

| 字段           | 类型   | 必选 | 描述        |
| -------------- | ------ | ---- | ----------- |
| bk_data_id  | int | 是   | 数据源 ID |
| bk_biz_id | int | 是 | 业务 ID |
| time_series_group_name | string | 是 | 自定义时序分组名 |
| label | string | 是 | 自定义时序分组标签，用于表示监控对象，应该复用【result_table_label】类型下的标签 |
| operator | string | 是 | 操作者 |
| metric_info_list | list | 否 | 自定义时序列表 |

#### metric_info_list 具体内容说明

| 字段                | 类型   | 必选  | 描述     |
| ------------------- | ------ |-----| -------- |
| field_name | string | 是   | 自定义时序名 |
| tag | list | 是   | 维度列表 |

#### 请求示例

```json
{
    "bk_app_code": "xxx",
  	"bk_app_secret": "xxxxx",
 	"bk_token": "xxxx",
	"bk_data_id": 123,
	"bk_biz_id": 123,
	"time_series_group_name": "自定义时序分组名",
	"label": "application",
	"operator": "system",
	"metric_info_list": [{
	  "field_name": "usage for update",
	  "tag_list": ["dimension_name"]
    },{
	  "field_name": "usage for create",
	  "tag_list": ["dimension_name"]
	}]
}
```

### 返回结果

| 字段    | 类型   | 描述         |
| ------- | ------ | ------------ |
| result  | bool   | 请求是否成功 |
| code    | int    | 返回的状态码 |
| message | string | 描述信息     |
| data    | dict   | 数据         |

#### data 字段说明

| 字段                | 类型   | 描述     |
| ------------------- | ------ | -------- |
| time_series_group_id | int | 新建的时序分组 ID  |
| time_series_group_name | string | 时序分组名称 |
| bk_data_id | int | 数据源 id |
| bk_biz_id | int | 业务 id |
| table_id | string | 结果表 ID |
| label | string | 事件标签 |
| is_enable | bool | 是否启用 |
| creator | string | 创建人 |
| create_time | string | 创建时间 |
| last_modify_user | string | 最后更新人 |
| last_modify_time | string | 最后更新时间 |
| metric_info_list | list | \自定义时序列表 |

#### data.metric_info_list 具体内容说明

| 字段        | 类型   | 描述     |
| ----------- | ------ | -------- |
| description | string | 描述     |
| field_name  | string | Field 名 |
| unit        | string | 单位     |
| type        | string | 单位类型 |
| tag_list    | list   | tag 列表  |

#### data.metric_info_list.tag_list 具体说明

| 字段        | 类型   | 描述     |
| ----------- | ------ | -------- |
| field_name  | string | 字段名   |
| description | string | 描述     |
| unit        | string | 单位     |
| type        | string | 单位类型 |

#### 结果示例

```json
{
    "message":"OK",
    "code":200,
    "data": {
    	"bk_data_id": 123,
    	"bk_biz_id": 123,
        "time_series_group_id": 1,
    	"time_series_group_name": "时序自定义时序分组名",
    	"label": "application",
    	"is_enable": true,
    	"creator": "admin",
    	"create_time": "2019-10-10 10:10:10",
    	"last_modify_user": "admin",
    	"last_modify_time": "2020-10-10 10:10:10",
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
    },
    "result":true,
    "request_id":"408233306947415bb1772a86b9536867"
}
```