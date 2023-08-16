
### 请求方法

GET


### 请求地址

/api/c/compapi/v2/monitor_v3/metadata_list_transfer_cluster/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

获取所有 transfer 集群信息

### 请求参数



#### 接口参数

无请求参数

#### 请求示例

```json
{
    "bk_app_code": "xxx",
  	"bk_app_secret": "xxxxx",
  	"bk_token": "xxxx",
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

| 字段       | 类型   | 描述           |
| ---------- | ------ | -------------- |
| cluster_id | string | transfer 集群 ID |

#### 结果示例

```json
{
    "message": "OK",
    "code": 200,
    "data": [
        {
            "cluster_id": "default"
        },
        {
            "cluster_id": "bkmonitorv3-na"
        }
    ],
    "result": true,
    "request_id": "408233306947415bb1772a86b9536867"
}
```