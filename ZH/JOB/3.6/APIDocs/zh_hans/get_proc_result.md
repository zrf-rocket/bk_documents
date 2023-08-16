### 功能描述

操作服务器上的进程结果查询

### 请求参数

{{ common_args_desc }}

#### Body参数

| 字段        |  类型      | 必选   |  描述      |
|-------------|------------|--------|------------|
| bk_scope_type | string | 是     | 资源范围类型。可选值: biz - 业务，biz_set - 业务集 |
| bk_scope_id | string | 是 | 资源范围ID, 与bk_scope_type对应, 表示业务ID或者业务集ID |
| bk_gse_taskid |  string    | 是     | GSE任务ID |

### 请求参数示例

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_scope_type": "biz",
    "bk_scope_id": "1",
    "bk_gse_taskid": "GSETASK:20180315180551:1000"
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": {
        "status": 115,
        "result": {
            "/usr/local/gse/gseagent/plugins/unifyTlogc/sbin/bk_gse_unifyTlogc:0:10.0.0.1": {
                "content": {
                    "process": [
                        {
                            "instance": [
                                {
                                    "cpuUsageAve": 0,
                                    "stat": "",
                                    "phyMemUsage": 0,
                                    "cmdline": "",
                                    "freeVMem": "0",
                                    "pid": -1,
                                    "threadCount": 0,
                                    "cpuUsage": 0,
                                    "elapsedTime": 0,
                                    "processName": "bk_gse_unifyTlogc",
                                    "diskSize": -1,
                                    "stime": "0",
                                    "startTime": "",
                                    "usePhyMem": 0,
                                    "utime": "0"
                                }
                            ],
                            "procname": "bk_gse_unifyTlogc"
                        }
                    ],
                    "ip": "10.0.0.1",
                    "utctime": "2018-04-04 09:56:20",
                    "utctime2": "2018-04-04 01:56:20",
                    "timezone": 8
                },
                "error_code": 0,
                "error_msg": "success"
            }
        }
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
| status       | int       | 预留字段。GSE任务状态码 |
| result       | object      | 真正的数据，依赖于GSE数据结构 |
