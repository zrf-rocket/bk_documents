
### 请求方法

GET


### 请求地址

/api/c/compapi/v2/jobv3/get_public_script_version_detail/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token与bk_username必须一个有效，bk_token可以通过Cookie获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

查询公共脚本版本详情

### 请求参数



#### 接口参数

| 字段       |  类型      | 必选   |  描述      |
|----------------------|------------|--------|------------|
| id             |  long       | 是     | 脚本版本ID，若传入则以此条件为准屏蔽其他条件 |
| script_id      |  string     | 否     | 脚本ID（可与version一起传入定位某个脚本版本）  |
| version        |  string     | 否     | 脚本版本（可与script_id一起传入定位某个脚本版本） |

### 请求参数示例

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "id": 1
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": {
        "id": 1,
        "script_id": "000dbdddc06c453baf1f2decddf00c69",
        "version": "V1.0",
        "content": "#!/bin/bash***",
        "status": 1,
        "version_desc": "版本描述",
        "creator": "admin",
        "create_time": 1600746078520,
        "last_modify_user": "admin",
        "last_modify_time": 1600746078520
    }
}
```

### 返回结果参数说明

#### response
| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| result       | bool   | 请求成功与否。true:请求成功；false请求失败 |
| code         | int    | 错误编码。 0表示success，>0表示失败错误 |
| message      | string | 请求失败返回的错误信息|
| data         | object | 请求返回的数据|
| permission   | object | 权限信息|
| request_id   | string | 请求链id|

#### data

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| id                | long      | 脚本版本ID |
| script_id         | string    | 脚本版本所属的脚本ID |
| version           | string    | 版本号 |
| content           | string    | 脚本版本内容 |
| status            | int       | 脚本版本状态（0：未上线，1：已上线，2：已下线，3：已禁用） |
| version_desc      | string    | 版本描述  |
| creator           | string    | 创建人 |
| create_time       | long      | 创建时间Unix时间戳（ms） |
| last_modify_user  | string    | 最近一次修改人 |
| last_modify_time  | long      | 最近一次修改时间Unix时间戳（ms） |