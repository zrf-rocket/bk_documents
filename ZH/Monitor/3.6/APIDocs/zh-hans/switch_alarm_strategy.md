
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/monitor_v3/switch_alarm_strategy/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

开关告警策略

### 请求参数



#### 接口参数

| 字段       | 类型 | 必选 | 描述       |
| --------- | ---- | ---- | ---------- |
| ids        | list | 是   | 策略 ID 列表 |
| is_enabled | bool | 是   | 是否开启   |

#### 参数示例

```json
{
    "bk_app_code": "xxx",
    "bk_app_secret": "xxxxx",
    "bk_token": "xxxx",
    "ids": [80],
    "is_enabled": true
}
```

### 响应参数

| 字段       | 类型   | 描述         |
| ---------- | ------ | ------------ |
| result     | bool   | 请求是否成功 |
| code       | int    | 返回的状态码 |
| message    | string | 描述信息     |
| data       | dict   | 数据         |
| request_id | string | 请求 ID       |

#### data 参数说明

| 字段       | 类型    | 描述       |
| --------- | ------ | ---------- |
| ids | list | 存在的策略 ID 列表 |

#### 参数示例

```json
{
 	"result": true,
    "code": 200,
    "data": {
    	"ids": [
            80
        ]
    },
    "message": "ok",
    "request_id": "eafafwafw1212241212513wafafafw"
}
```