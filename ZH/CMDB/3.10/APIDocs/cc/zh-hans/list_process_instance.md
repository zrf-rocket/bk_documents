
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/cc/list_process_instance/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

根据服务实例 ID 查询进程实例列表

### 请求参数



#### 接口参数

| 字段                 |  类型      | 必选	   |  描述                 |
|----------------------|------------|--------|-----------------------|
|bk_biz_id|int|是| 业务 ID |
| service_instance_id | int  | 是   | 服务实例 ID |


### 请求参数示例

```python
{
  "bk_app_code": "esb_test",
  "bk_app_secret": "xxx",
  "bk_username": "xxx",
  "bk_token": "xxx",
  "bk_biz_id": 1,
  "service_instance_id": 54
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
  "data": [
    {
      "property": {
        "auto_start": false,
        "auto_time_gap": 60,
        "bk_biz_id": 2,
        "bk_func_id": "",
        "bk_func_name": "java",
        "bk_process_id": 46,
        "bk_process_name": "job_java",
        "bk_start_param_regex": "",
        "bk_supplier_account": "0",
        "create_time": "2019-06-05T14:59:12.065+08:00",
        "description": "",
        "face_stop_cmd": "",
        "last_time": "2019-06-05T14:59:12.065+08:00",
        "pid_file": "",
        "priority": 1,
        "proc_num": 1,
        "reload_cmd": "",
        "restart_cmd": "",
        "start_cmd": "",
        "stop_cmd": "",
        "timeout": 30,
        "user": "",
        "work_path": "/data/bkee",
        "bind_info": [
            {
                "enable": false,  
                "ip": "127.0.0.1",  
                "port": "100",  
                "protocol": "1", 
                "template_row_id": 1  
            }
        ]
      },
      "relation": {
        "bk_biz_id": 1,
        "bk_process_id": 46,
        "service_instance_id": 54,
        "process_template_id": 1,
        "bk_host_id": 1,
        "bk_supplier_account": ""
      }
    }
  ]
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
| data | array | 请求返回的数据 |

#### data 字段说明

| 字段|类型|说明|
|---|---|---|
|property|object|进程属性信息|
|relation|object|进程与服务实例的关联信息|

#### data[x].property 字段说明
| 字段|类型|说明|
|---|---|---|
|auto_start|bool|是否自动拉起|
|auto_time_gap|int|拉起间隔|
|bk_biz_id|int|业务 id|
|bk_func_id|string|功能 ID|
|bk_func_name|string|进程名称|
|bk_process_id|int|进程 id|
|bk_process_name|string|进程别名|
|bk_start_param_regex|string|进程启动参数|
|bk_supplier_account|string|开发商账号|
|create_time|string|创建时间|
|description|string|描述|
|face_stop_cmd|string|强制停止命令|
|last_time|string|更新时间|
|pid_file|string|PID 文件路径|
|priority|int|启动优先级|
|proc_num|int|启动数量|
|reload_cmd|string|进程重载命令|
|restart_cmd|string|重启命令|
|start_cmd|string|启动命令|
|stop_cmd|string|停止命令|
|timeout|int|操作超时时长|
|user|string|启动用户|
|work_path|string|工作路径|
|bind_info|object|绑定信息|

#### data[x].property.bind_info[n] 字段说明
| 字段|类型|说明|
|---|---|---|
|enable|bool|端口是否启用|
|ip|string|绑定的 ip|
|port|string|绑定的端口|
|protocol|string|使用的协议|
|template_row_id|int|实例化使用的模板行索引，进程内唯一|

#### data[x].relation 字段说明
| 字段|类型|说明|
|---|---|---|
|bk_biz_id|int|业务 id|
|bk_process_id|int|进程 id|
|service_instance_id|int|服务实例 id|
|process_template_id|int|进程模版 id|
|bk_host_id|int|主机 id|
|bk_supplier_account|string|开发商账号|