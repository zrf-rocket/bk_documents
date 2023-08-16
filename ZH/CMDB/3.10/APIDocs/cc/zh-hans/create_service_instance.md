
### 请求方法

POST


### 请求地址

/api/c/compapi/v2/cc/create_service_instance/


### 通用参数

| 字段 | 类型 | 必选 |  描述 |
|-----------|------------|--------|------------|
| bk_app_code  |  string    | 是 | 应用 ID     |
| bk_app_secret|  string    | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -> 点击应用 ID -> 基本信息 获取 |
| bk_token     |  string    | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username  |  string    | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |


### 功能描述

批量创建服务实例，如果模块绑定了服务模板，则服务实例也会根据模板创建，创建服务实例的进程参数内也必须提供每个进程对应的进程模板 ID

### 请求参数



#### 接口参数

| 字段                 |  类型      | 必选	   |  描述                 |
|----------------------|------------|--------|-----------------------|
| bk_module_id         | int  | 是   | 模块 ID |
| instances            | array  | 是   | 需要创建的服务实例信息|
| bk_biz_id            | int  | 是   | 业务 ID|

#### instances 字段说明

| 字段|类型|必选	   |说明|Description|
|---|---|---|---|---|
|instances.bk_host_id|int|是|主机 ID|服务实例绑定的主机 ID|
|instances.processes|array|是|进程信息|服务实例下新建的进程信息|
|instances.processes.process_template_id|int|是|进程模板 ID|如果模块没有绑定服务模板则填 0|
|instances.processes.process_info|object|是|进程实例信息|如果进程绑定有模板，则仅模板中没有锁定的字段有效|

#### processes 字段说明
| 字段|类型|必选	   |说明|
|---|---|---|---|
|process_template_id|int|是|进程模版 id|
|auto_start|bool|否|是否自动拉起|
|auto_time_gap|int|否|拉起间隔|
|bk_biz_id|int|否|业务 id|
|bk_func_id|string|否|功能 ID|
|bk_func_name|string|否|进程名称|
|bk_process_id|int|否|进程 id|
|bk_process_name|string|否|进程别名|
|bk_supplier_account|string|否|开发商账号|
|face_stop_cmd|string|否|强制停止命令|
|pid_file|string|否|PID 文件路径|
|priority|int|否|启动优先级|
|proc_num|int|否|启动数量|
|reload_cmd|string|否|进程重载命令|
|restart_cmd|string|否|重启命令|
|start_cmd|string|否|启动命令|
|stop_cmd|string|否|停止命令|
|timeout|int|否|操作超时时长|
|user|string|否|启动用户|
|work_path|string|否|工作路径|
|process_info|object|是|进程信息|

#### process_info 字段说明
| 字段|类型|必选	   |说明|
|---|---|---|---|
|bind_info|object|是|绑定信息|
|bk_supplier_account|string|是|开发商账号|

#### bind_info 字段说明
| 字段|类型|必选	   |说明|
|---|---|---|---|
|enable|bool|是|端口是否启用|
|ip|string|是|绑定的 ip|
|port|string|是|绑定的端口|
|protocol|string|是|使用的协议|
|template_row_id|int|是|实例化使用的模板行索引，进程内唯一|

### 请求参数示例

```json
{
  "bk_app_code": "esb_test",
  "bk_app_secret": "xxx",
  "bk_username": "xxx",
  "bk_token": "xxx",
  "bk_biz_id": 1,
  "bk_module_id": 60,
  "instances": [
    {
      "bk_host_id": 2,
      "processes": [
        {
          "process_template_id": 1,
          "process_info": {
            "bk_supplier_account": "0",
            "bind_info": [
              {
                  "enable": false,
                  "ip": "127.0.0.1",
                  "port": "80",
                  "protocol": "1",
                  "template_row_id": 1234
              }
            ],
            "description": "",
            "start_cmd": "",
            "restart_cmd": "",
            "pid_file": "",
            "auto_start": false,
            "timeout": 30,
            "auto_time_gap": 60,
            "reload_cmd": "",
            "bk_func_name": "java",
            "work_path": "/data/bkee",
            "stop_cmd": "",
            "face_stop_cmd": "",
            "port": "8008,8443",
            "bk_process_name": "job_java",
            "user": "",
            "proc_num": 1,
            "priority": 1,
            "bk_biz_id": 2,
            "bk_func_id": "",
            "bk_process_id": 1
          }
        }
      ]
    }
  ]
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
  "data": [53]
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
| data | object | 新建的服务实例 ID 列表 |