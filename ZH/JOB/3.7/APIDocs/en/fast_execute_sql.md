### Function Description

Quick execution of SQL scripts

### Request Parameters

{{ common_args_desc }}

#### Interface parameters

| Fields    |  Type  | Required | Description |
|---------------|------------|--------|------------|
| bk_scope_type | string | yes  | Resource scope type. Optional values: biz - Business，biz_set - Business Set |
| bk_scope_id | string | yes | Resource scope ID. Corresponds to bk_scope_type, which means business ID or business set ID |
| script_version_id |  long       |  no   | SQL script version ID|
| script_id | string | no |Script id. When script_id is passed in and script_version_id is empty, the online version of the current script is used|
| script_content |  string    |  no   | Script content Base64. If script_version_id and script_id do not exist, script_content is used. Priority: script_version_id>script_id>script_content|
| timeout |  int       |  no   | Script timeout in seconds. Default 7200, value range 1 86400|
| db_account_id  |  long       |  yes  |Db account ID for SQL execution|
| target_server    |   object   |  no   | Target server, see server definition|
| callback_url |  string   |  no   | Callback URL, when the task execution is completed, the JOB will call this URL to inform the task execution result. Callback protocol refer to the callback_protocol component documentation|

#### server

| Fields             | Type  | Required | Description                         |
| ------------------ | ----- | -------- | ----------------------------------- |
| ip_list            |  array | no       | Static IP list, as defined in ip              |
| dynamic_group_list | array | no       | Dynamic grouping list, see dynamic_group for definition   |
| topo_node_list     |  array | no       | Dynamic topo node list. See topo_node for definition|

#### ip

| Fields      | Type   | Required | Description   |
| ----------- | ------ | -------- | ------------- |
| bk_cloud_id | long   | yes      | Cloud area ID |
| ip          | string | yes      | IP Address    |

#### dynamic_group

| Fields | Type   | Required | Description    |
| ------ | ------ | -------- | -------------- |
| id     |  string | yes      | CMDB dynamic grouping ID|

#### topo_node_list

| Fields    | Type   | Required | Description                                                  |
| --------- | ------ | -------- | ------------------------------------------------------------ |
| id        |  long   |  yes      | Dynamic topo node ID, corresponding to bk_inst_id in CMDB API                 |
| node_type | string | yes      | Dynamic topo node type, corresponding to bk_obj_id in CMDB API, such as "module,""set"|

### Example of request

```json
{
    "bk_app_code": "esb_test",
    "bk_app_secret": "xxx",
    "bk_token": "xxx",
    "bk_scope_type": "biz",
    "bk_scope_id": "1",
    "script_version_id": 1,
    "timeout": 1000,
    "db_account_id": 32,
    "target_server": {
        "dynamic_group_list": [
            {
                "id": "blo8gojho0skft7pr5q0"
            }
        ],
        "ip_list": [
            {
                "bk_cloud_id": 0,
                "ip": "10.0.0.1"
            },
            {
                "bk_cloud_id": 0,
                "ip": "10.0.0.2"
            }
        ],
        "topo_node_list": [
            {
                "id": 1000,
                "node_type": "module"
            }
        ]
    }
}
```

### Example of responses

```json
{
    "result": true,
    "code": 0,
    "message": "success",
    "data": {
        "job_instance_name": "API Quick SQL Execution1524454292038",
        "job_instance_id": 10000,
        "step_instance_id": 10001
    }
}
```

### Response Description

#### response
| Fields | Type  | Description |
|-----------|-----------|-----------|
| result       |  bool   | Whether the request was successful or not. True: request succeeded;False: request failed|
| code         |  int    | Error code. 0 indicates success, >0 indicates failure|
| message      |  string |Error message|
| data         |  object |Data returned by request|
| permission   |  object |Permission information|
| request_id   |  string |Request chain id|

#### data

| Fields | Type  | Description |
|-----------|-----------|-----------|
| job_instance_id     |  long      | Job instance ID|
| job_instance_name   |  long      | Job instance name|
| step_instance_id    |  long      | Step instance ID|
