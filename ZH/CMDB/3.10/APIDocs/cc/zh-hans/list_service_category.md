
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/cc/list_service_category/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

查询服务分类列表，根据业务 ID 查询，共用服务分类也会返回

### 请求参数



#### 接口参数

| 字段                 |  类型      | 必选	   |  描述                 |
|----------------------|------------|--------|-----------------------|
| bk_biz_id           | int    | 是   | 业务 ID         |

### 请求参数示例

```python
{
  "bk_app_code": "esb_test",
  "bk_app_secret": "xxx",
  "bk_username": "xxx",
  "bk_token": "xxx",
  "bk_biz_id": 1,
}
```

### 返回结果示例

```python
{
  "result": true,
  "code": 0,
  "message": "success",
  "permission": null,
  "request_id": "e43da4ef221746868dc4c837d36f3807",
  "data": {
    "count": 20,
    "info": [
      {
	"bk_biz_id": 0,
        "id": 16,
        "name": "Apache",
        "bk_root_id": 14,
        "bk_parent_id": 14,
        "bk_supplier_account": "0",
        "is_built_in": true
      },
      {
	"bk_biz_id": 0,
        "id": 19,
        "name": "Ceph",
        "bk_root_id": 18,
        "bk_parent_id": 18,
        "bk_supplier_account": "0",
        "is_built_in": true
      },
      {
	"bk_biz_id": 1,
        "id": 1,
        "name": "Default",
        "bk_root_id": 1,
        "bk_supplier_account": "0",
        "is_built_in": true
      }
    ]
  }
}
```

### 返回结果参数说明

#### response

| 名称  | 类型  | 描述 |
|---|---|---|
| result | bool | 请求成功与否。true:请求成功；false 请求失败 |
| code | int | 错误编码。 0 表示 success，>0 表示失败错误 |
| message | string | 请求失败返回的错误信息 |
| permission    | object | 权限信息    |
| request_id    | string | 请求链 id    |
| data | object | 请求返回的数据 |

#### data 字段说明

| 字段|类型|描述|
|---|---|---|
|count|int|总数|
|info|array|返回结果|

#### info 字段说明

| 字段|类型|说明|
|---|---|---|
|id|int|服务分类 ID|
|name|string|服务分类名称|
|bk_root_id|int|根服务分类 ID|
|bk_parent_id|int|父服务分类 ID|
|is_built_in|bool|是否内置|
|bk_supplier_account | string |开发商帐户名称|