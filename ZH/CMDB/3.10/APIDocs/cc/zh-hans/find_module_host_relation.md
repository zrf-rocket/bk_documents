
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/cc/find_module_host_relation/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

根据模块 ID 查询主机和模块的关系(v3.8.7)

### 请求参数



#### 接口参数

| 字段          | 类型         | 必选 | 描述                                         |
| ------------- | ------------ | ---- | -------------------------------------------- |
| bk_biz_id     | int          | 是   | 业务 ID                                       |
| bk_module_ids |  array    | 是   | 模块 ID 数组，最多 200 条                        |
| module_fields |  array | 是   | 模块属性列表，控制返回结果的模块里有哪些字段 |
| host_fields   |  array | 是   | 主机属性列表，控制返回结果的主机里有哪些字段 |
| page          | object       | 是   | 分页参数                                     |

#### page

| 字段  | 类型 | 必选 | 描述                  |
| ----- | ---- | ---- | --------------------- |
| start | int  | 否   | 记录开始位置,默认值 0  |
| limit | int  | 是   | 每页限制条数,最大 1000 |

**注: 一个模块下的主机关系可能会拆分多次返回，分页方式是按主机 ID 排序进行分页。**

### 请求参数示例

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_username": "xxx",
    "bk_token": "xxx",
    "bk_biz_id": 1,
    "bk_module_ids": [
        1,
        2,
        3
    ],
    "module_fields": [
        "bk_module_id",
        "bk_module_name"
    ],
    "host_fields": [
        "bk_host_innerip",
        "bk_host_id"
    ],
    "page": {
        "start": 0,
        "limit": 500
    }
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
  "data": {
    "count": 2,
    "relation": [
      {
        "host": {
          "bk_host_id": 1,
          "bk_host_innerip": "127.0.0.1",
        },
        "modules": [
          {
            "bk_module_id": 1,
            "bk_module_name": "m1",
          },
          {
            "bk_module_id": 2,
            "bk_module_name": "m2",
          }
        ]
      },
      {
        "host": {
          "bk_host_id": 2,
          "bk_host_innerip": "127.0.0.2",
        },
        "modules": [
          {
            "bk_module_id": 3,
            "bk_module_name": "m3",
          }
        ]
      }
    ]
  }
}
```

### 返回结果参数说明

| 名称    | 类型   | 说明                                       |
| ------- | ------ | ------------------------------------------ |
| result  | bool   | 请求成功与否。true:请求成功；false 请求失败 |
| code    | int    | 错误编码。 0 表示 success，>0 表示失败错误    |
| message | string | 请求失败返回的错误信息                     |
| permission    | object | 权限信息    |
| request_id    | string | 请求链 id    |
| data    | object | 请求返回的数据                             |

data 字段说明：

| 名称     | 类型         | 说明               |
| -------- | ------------ | ------------------ |
| count    | int          | 记录条数           |
| relation |  array | 主机和模块实际数据 |


relation 字段说明:

| 名称    | 类型         | 说明               |
| ------- | ------------ | ------------------ |
| host    | object       | 主机数据           |
| modules |  array | 主机所属的模块信息 |