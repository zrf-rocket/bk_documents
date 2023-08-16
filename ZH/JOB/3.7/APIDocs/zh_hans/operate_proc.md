### 功能描述

操作服务器上的进程

### 请求参数

{{ common_args_desc }}

#### Body参数

| 字段        |  类型      | 必选   |  描述      |
|-------------|------------|--------|------------|
| bk_scope_type | string | 是     | 资源范围类型。可选值: biz - 业务，biz_set - 业务集 |
| bk_scope_id | string | 是 | 资源范围ID, 与bk_scope_type对应, 表示业务ID或者业务集ID |
| op_type       |  int       | 是     | 操作类型，可选值：0:启动进程(start); 1:停止进程(stop); 2:进程状态查询; 3:注册托管进程; 4:取消托管进程; 7:重启进程(restart); 8:重新加载进(reload); 9:杀死进程(kill) |
| process_infos |  array     | 是     | 进程操作参数数组，见下面process_infos结构定义 |

##### process_infos

| 字段        |  类型      | 必选   |  描述      |
|-------------|------------|--------|------------|
| setup_path    |  string    | 是     | 进程路径，例如/usr/local/gse/gseagent/plugins/unifyTlogc/sbin |
| proc_name     |  string    | 是     | 进程名称，例如bk_gse_unifyTlogc |
| pid_path      |  string    | 是     | 进程的pid文件所在路径, 例如/usr/local/gse/gseagent/plugins/unifyTlogc/log/bk_gse_unifyTlogc.pid |
| account       |  string    | 否     | 系统账号，默认不传为root |
| cmd_shell_ext |  string    | 否     | 进程操作控制脚本的扩展名: sh:默认值shell适于Linux或cygwin,bat:windows的dos脚本,ps1:windows的Powershell脚本;注意：这个是针对ip_list参数下所有IP统一配置，所以确保接口传递的ip_list参数下所有IP都能支持指定的脚本。 |
| cpu_lmt       |  int       | 否     | 进程使用cpu限制，超过限制agent会根据配置的cmd_shell_ext调用相应类型的stopCmd停止进程。 |
| mem_lmt       |  int       | 否     | 进程使用mem限制，超过限制agent会根据配置的cmd_shell_ext调用相应类型的stopCmd停止进程。 |
| ip_list       |  array     | 是     | IP对象数组，见下面ip_list结构定义 |

##### ip_list

| 字段        |  类型      | 必选   |  描述      |
|-------------|------------|--------|------------|
| bk_cloud_id |  int    | 是     | 云区域ID |
| ip          |  string | 是     | IP地址 |

### 请求参数示例

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_scope_type": "biz",
    "bk_scope_id": "1",
    "op_type": 1,
    "process_infos": [
        {
            "setup_path": "/usr/local/xxx",
            "proc_name": "gseagent",
            "pid_path": "/usr/local/xxx",
            "account": "root",
            "cmd_shell_ext": "bat",
            "cpu_lmt": 50,
            "mem_lmt": 30,
            "ip_list": [
                {
                    "bk_cloud_id": 0,
                    "ip": "10.0.0.1"
                }
            ]
        }
    ]
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "",
    "data": {
        "bk_gse_taskid": "GSETASK:20180315180551:1000"
    }
}
```

### 返回结果参数说明

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| result       | bool   | 请求成功与否。true:请求成功；false请求失败 |
| code         | int    | 错误编码。 0表示success，>0表示失败错误 |
| message      | string | 请求失败返回的错误信息|
| data         | object | 请求返回的数据|
| permission   | object | 权限信息|

##### data

| 字段      | 类型      | 描述      |
|-----------|-----------|-----------|
| bk_gse_taskid       | string       | GSE任务ID |
