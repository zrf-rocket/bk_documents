
### 请求方法

POST


### 请求地址

/api/c/compapi/cmsi/send_voice_msg/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

公共语音通知

### 请求参数

#### 接口参数

| 字段                  |  类型      | 必选   |  描述      |
|-----------------------|------------|--------|------------|
| auto_read_message     |  string    | 是     | 自动语音读字信息 |
| user_list_information |  array     | 否     | 待通知的用户列表，自动语音通知列表，若 user_list_information、receiver__username 同时存在，以 user_list_information 为准 |
| receiver__username    |  string    | 否     | 待通知的用户列表，包含用户名，用户需在蓝鲸平台注册，多个以逗号分隔，若 user_list_information、receiver__username 同时存在，以 user_list_information 为准 |

#### user_list_information

| 字段         |  类型      | 必选   |  描述      |
|--------------|------------|--------|------------|
| username     |  string    | 是     | 被通知人 |
| mobile_phone |  string    | 否     | 被通知人手机号 |

### 请求参数示例

```python
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "auto_read_message": "This is a test",
    "user_list_information": [{
        "username": "admin",
        "mobile_phone": "1234567890",
    }]
}
```

### 返回结果示例

```python
{
    "result": true,
    "code": 0,
    "message": "",
}
```

### 返回结果参数说明

| 字段      | 类型      | 描述      |
|-----------|----------|-----------|
|  result   |    bool    |      返回结果，true 为成功，false 为失败     |
|  code     |    int     |      返回码，0 表示成功，其它值表示失败 |
|  message  |    string  |      错误信息      |