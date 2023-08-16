# Summary

## 标准运维
* [产品简介](产品白皮书/产品简介/README.md)
* [术语解释](产品白皮书/术语解释/glossary.md)
* [产品架构图](产品白皮书/产品架构图/framework.md)
* [快速入门]()
    * [JOB 任务流程](产品白皮书/快速入门/job_flow.md)
* [产品功能]()
    * [本章概述](产品白皮书/产品功能/function.md)
    * [业务首页](产品白皮书/产品功能/page.md)
    * [项目流程](产品白皮书/产品功能/flow.md)
    * [项目流程-新建流程](产品白皮书/产品功能/flow-edit.md)
    * [项目流程-新建任务](产品白皮书/产品功能/flow-new_task.md)
    * [任务管理-任务记录](产品白皮书/产品功能/record.md)
    * [任务管理-周期任务](产品白皮书/产品功能/periodic_task.md)
    * [轻应用](产品白皮书/产品功能/use.md)
    * [公共流程](产品白皮书/产品功能/common_flow.md)
    * [职能化](产品白皮书/产品功能/function_task.md)
    * [审计中心](产品白皮书/产品功能/audit.md)
    * [项目管理](产品白皮书/产品功能/project_management.md)
    * [管理员入口](产品白皮书/产品功能/administrator_portal.md)
* [API 文档]()
    * [简介](APIDocs/sops/README.md)
    * [认领职能化任务](APIDocs/sops/zh-hans/claim_functionalization_task.md)
    * [通过流程模板创建并开始执行任务](APIDocs/sops/zh-hans/create_and_start_task.md)
    * [通过流程模板新建周期任务](APIDocs/sops/zh-hans/create_periodic_task.md)
    * [通过流程模板新建任务](APIDocs/sops/zh-hans/create_task.md)
    * [快速新建一次性任务](APIDocs/sops/zh-hans/fast_create_task.md)
    * [查询单个公共流程模板详情](APIDocs/sops/zh-hans/get_common_template_info.md)
    * [查询公共模板列表](APIDocs/sops/zh-hans/get_common_template_list.md)
    * [获取职能化任务列表](APIDocs/sops/zh-hans/get_functionalization_task_list.md)
    * [查询业务下的某个周期任务详情](APIDocs/sops/zh-hans/get_periodic_task_info.md)
    * [查询业务下的周期任务列表](APIDocs/sops/zh-hans/get_periodic_task_list.md)
    * [查询某个业务下的插件列表](APIDocs/sops/zh-hans/get_plugin_list.md)
    * [根据插件 code 获取某个业务下对应插件信息](APIDocs/sops/zh-hans/get_plugin_detail.md)
    * [批量查询任务状态](APIDocs/sops/zh-hans/get_task_detail.md)
    * [查询任务执行详情](APIDocs/sops/zh-hans/get_task_list.md)
    * [获取业务下的任务列表](APIDocs/sops/zh-hans/get_task_node_data.md)
    * [获取节点执行数据](APIDocs/sops/zh-hans/get_task_node_detail.md)
    * [查询任务节点执行详情](APIDocs/sops/zh-hans/get_task_status.md)
    * [获取一批任务的是否需要人工干预的判断状态](APIDocs/sops/zh-hans/get_tasks_manual_intervention_state.md)
    * [查询任务或任务节点执行状态](APIDocs/sops/zh-hans/get_tasks_status.md)
    * [查询单个模板详情](APIDocs/sops/zh-hans/get_template_info.md)
    * [查询模板列表](APIDocs/sops/zh-hans/get_template_list.md)
    * [获取模板执行方案列表](APIDocs/sops/zh-hans/get_template_schemes.md)
    * [获取项目详情](APIDocs/sops/zh-hans/get_user_project_detail.md)
    * [获取用户有权限的项目列表](APIDocs/sops/zh-hans/get_user_project_list.md)
    * [导入公共流程](APIDocs/sops/zh-hans/import_common_template.md)
    * [导入业务流程模板](APIDocs/sops/zh-hans/import_project_template.md)
    * [修改周期任务的全局参数](APIDocs/sops/zh-hans/modify_constants_for_periodic_task.md)
    * [修改任务的全局参数](APIDocs/sops/zh-hans/modify_constants_for_task.md)
    * [修改周期任务的调度策略](APIDocs/sops/zh-hans/modify_cron_for_periodic_task.md)
    * [回调任务节点](APIDocs/sops/zh-hans/node_callback.md)
    * [操作任务中的节点](APIDocs/sops/zh-hans/operate_node.md)
    * [操作任务](APIDocs/sops/zh-hans/operate_task.md)
    * [获取节点选择后新的任务树](APIDocs/sops/zh-hans/preview_task_tree.md)
    * [获取节点选择后新的任务树（针对公共流程）](APIDocs/sops/zh-hans/preview_common_task_tree.md)
    * [查询任务分类统计总数](APIDocs/sops/zh-hans/query_task_count.md)
    * [设置周期任务是否激活](APIDocs/sops/zh-hans/set_periodic_task_enabled.md)
    * [开始执行任务](APIDocs/sops/zh-hans/start_task.md)
* [常见问题](产品白皮书/常见问题/FAQ.md)
* [附录]()
    * [附录 1：分支表达式]()
        * [定义](产品白皮书/附录/define.md)
        * [语法](产品白皮书/附录/grammar.md)
        * [分支执行逻辑](产品白皮书/附录/logic.md)
    * [附录 2：标准插件开发]()
        * [创建 Django APP 和目录结构](产品白皮书/附录/Django.md)
        * [修改 settings 配置](产品白皮书/附录/settings.md)
        * [接入 ESB API](产品白皮书/附录/ESB.md)
        * [标准插件后台开发](产品白皮书/附录/atomic.md)
        * [标准插件前端开发](产品白皮书/附录/front.md)
        * [标准插件测试](产品白皮书/附录/test.md)
        * [提交代码](产品白皮书/附录/submit.md)
        * [标准插件开发规范](产品白皮书/附录/specification.md)