
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/cc/find_set_batch/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

根据业务id和集群实例id列表，以及想要获取的属性列表，批量获取指定业务下集群的属性详情 (v3.8.6)

### 请求参数



#### 接口参数

| 字段      |  类型      | 必选   |  描述      |
|-----------|------------|--------|------------|
| bk_biz_id  | int  | 是     | 业务ID |
| bk_ids  | array  | 是     | 集群实例ID列表, 即bk_set_id列表，最多可填500个 |
| fields  |  array   | 是     | 集群属性列表，控制返回结果的集群信息里有哪些字段 |

### 请求参数示例

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_username": "xxx",
    "bk_token": "xxx",
    "bk_biz_id": 3,
    "bk_ids": [
        11,
        12
    ],
    "fields": [
        "bk_set_id",
        "bk_set_name",
        "create_time"
    ]
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "success",
    "permission": null,
    "request_id": "e43da4ef221746868dc4c837d36f3807",
    "data": [
        {
            "bk_set_id": 12,
            "bk_set_name": "ss1",
            "create_time": "2020-05-15T22:15:51.67+08:00",
            "default": 0
        },
        {
            "bk_set_id": 11,
            "bk_set_name": "set1",
            "create_time": "2020-05-12T21:04:36.644+08:00",
            "default": 0
        }
    ]
}
```

### 返回结果参数说明
#### response
| 名称    | 类型   | 说明                                       |
| ------- | ------ | ------------------------------------------ |
| result  | bool   | 请求成功与否。true:请求成功；false请求失败 |
| code    | int    | 错误编码。 0表示success，>0表示失败错误    |
| message | string | 请求失败返回的错误信息                     |
| permission    | object | 权限信息    |
| request_id    | string | 请求链id    |
| data    | object | 请求返回的数据                             |