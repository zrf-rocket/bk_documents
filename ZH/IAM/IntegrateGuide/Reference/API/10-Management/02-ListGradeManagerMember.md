# 接入系统管理类 API
### 查询分级管理员成员列表

-------

#### URL

ESB API

> GET /api/c/compapi/v2/iam/management/grade_managers/{grade_manager_id}/members/

APIGateway2.0 API

> GET /api/v1/open/management/grade_managers/{grade_manager_id}/members/

> `特别说明`: [ESB API 与 APIGateway2.0 API 说明](../01-Overview/01-BackendAPIvsESBAPI.md)


#### Parameters

* 通用参数

| 字段 |  类型 |是否必须  | 描述  |
|--------|--------|--------|--------|
|bk_app_code|string|是|应用 ID|
|bk_app_secret|string|是|安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取|
|bk_token|string|否|当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取|
|bk_username|string|否|当前用户用户名，仅仅在 ESB 里配置免登录态验证白名单中的应用，才可以用此字段指定当前用户|

* 接口参数

| 字段 |  类型 |是否必须  | 位置 |描述  |
|--------|--------|--------|--------|--------|
| grade_manager_id | int | 是 | path | 分级管理员 ID |

#### Request
```bash
Get /api/c/compapi/v2/iam/management/grade_managers/1/members/
```

#### Response

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| data   | array[string]     | 用户名列表 |


> Status: 200 OK

```json
{
  "code": 0,
  "message": "ok",
  "data": [
    "admin",
    "test"
  ]
}
```
