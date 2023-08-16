
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/itsm/ticket_approval_result/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

单据详情查询，支持根据单号查询单据的详情（携带基本信息和提单信息）

### 请求参数



#### 接口参数

| 字段        | 类型     | 必选  | 描述                         |
| --------- | ------ | --- | -------------------------- |
| sn        | list | 是   | 单号                       |



### 请求参数示例

```json
{  
    "bk_app_secret": "xxxx", 
    "bk_app_code": "xxxx", 
    "bk_token": "xxxx", 
    "sn": ["NO2019090XXXXXXXX"]
}  
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": [{
        "sn": "REQ20200831000005",
        "title": "测试内置审批",
        "ticket_url": "https://***",
        "current_status": "FINISHED",
        "updated_by": "xx,xxx",
        "update_at": "2020-08-31 20:57:22",
        "approve_result": true
    }]
}
```

### 返回结果参数说明

| 字段      | 类型        | 描述                      |
| ------- | --------- | ----------------------- |
| result  | bool      | 返回结果，true为成功，false为失败   |
| code    | int       | 返回码，0表示成功，其他值表示失败       |
| message | string    | 错误信息                    |
| data    | list    | 返回数据 |

### data

| 字段                     | 类型     | 描述       |
| ---------------------- | ------ | -------- |
| sn                     | string | 单号     |
| title                  | string | 单据标题     |
| current_status         | string | 单据当前状态，RUNNING（处理中）/FINISHED（已结束）/TERMINATED（被终止）   |
| ticket_url             | string | 单据地址   |
| comment_id             | string | 单据评价id   |
| updated_by             | string | 最近更新者    |
| update_at              | string | 最近更新时间   |
| approve_result         | boolean| 审批结果，True为通过,False为拒绝|