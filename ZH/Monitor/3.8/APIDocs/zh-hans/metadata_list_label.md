
### 请求方法

GET


### 请求地址

/api/c/compapi/v2/monitor_v3/metadata_list_label/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

获取数据标签 
根据请求的参数，返回各个请求数据标签，包含了数据源标签及结果表各级标签

### 请求参数



#### 接口参数

| 字段           | 类型   | 必选 | 描述        |
| -------------- | ------ | ---- | ----------- |
| label_type | string | 是 | 标签分类，`source_label`, `type_label` or `result_table_label` |
| level | int | 是 | 标签层级, 层级从 1 开始计算, 该配置只在`label_type`为`result_table`时生效 |
| include_admin_only | bool | 是 | 是否展示管理员可见标签 |


#### 请求示例

```json
{
    "bk_app_code": "xxx",
  	"bk_app_secret": "xxxxx",
  	"bk_token": "xxxx",
    "include_admin_only": True,
	"level": 1,
	"label_type": "source_label"
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

| 字段                | 类型   | 描述     |
| ------------------- | ------ | -------- |
| label_id | string | 标签 ID（英文名）
| label_name | string | 标签名（中文名）| 
| label_type | string | 标签分类 |
| level | int | 标签层级 | 
| parent_label | string | 父级标签 ID |
| index | int | 标签在同 level 下的排序顺序 | 


#### 结果示例

```json
{
    "message":"OK",
    "code":200,
    "data": {
        "source_label": [{
            "label_id": "bk_monitor_collector",
            "label_name": "蓝鲸监控采集器",
            "label_type": "source_label",
            "level": null,
            "parent_label": null,
            "index": 0
        }],
        "type_label": [{
            "label_id": "time_series",
            "label_name": "时序数据",
            "label_type": "type_label",
            "level": null,
            "parent_label": null,
            "index": 0
        }],
        "result_table_label": [{
            "label_id": "OS",
            "label_name": "操作系统",
            "label_type": "result_table_label",
            "level": 2,
            "parent_label": "host",
            "index": 0
        }, {
            "label_id": "host",
            "label_name": "主机",
            "label_type": "result_table_label",
            "level": 1,
            "parent_label": null,
            "index": 1
        }]
    },
    "result":true,
    "request_id":"408233306947415bb1772a86b9536867"
}
```