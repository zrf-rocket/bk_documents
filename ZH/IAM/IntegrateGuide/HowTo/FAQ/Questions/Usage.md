# 使用场景相关

## 1. 怎么实现批量鉴权, 一个用户是否有查看 1000 台主机的权限 

- 调用策略查询`/api/v1/policy/query`接口
    - 传了 resource, 相当于权限中心会基于表达式做第一遍计算, 缩小策略数量
    - 不传 resource, 会把所有策略返回去
- 不传 resource, 获取得到所有策略
- 将 1000 台主机 for 循环逐一带入求值
- 此时, 相当于做一次策略查询, 执行 1000 次计算(内存表达式求值性能很高)

## 2. 配置权限的时候, 怎么控制只能选择实例, 不需要配置属性

action 操作注册时, `related_resource_types[i].selection_mode=instance`即可, 具体见文档  [操作(Action) API](../../../Reference/API/02-Model/13-Action.md)

如果只需要属性,  `selection_mode=attribute`; 如果两者都要`selection_mode=all`

## 3. 能否放开单个用户配置超过 10000 个实例的权限

10000 个限制**不会放开**

具体见 [大规模实例级权限限制具体说明和对应处理方案](../../../Explanation/06-LargeScaleInstances.md)

## 4. 授权接口的机制是怎样的? 重复调用会不会有问题?

增量更新, 会同已有权限进行合并

重复调用不会有问题

## 5. 用户组管理时, 组名是唯一的吗?

用户组名是分级管理员下唯一

## 6. 如果调用权限中心接口报错, 应该怎么提示给用户?

假设接入系统调用接口报错, 需要显式提示并且打日志: **记录详细错误信息, 并把错误信息/原因暴露给用户**

相关信息:
- 请求时间
- method
- url
- response status
- response body
- requestID
- 报错堆栈

有很多因素, 例如网络错误/超时/请求数据错误/接口 500 /接口 502等等.

一定不能: 吞掉异常或者没有打日志, 直接弹窗提示请联系权限中心(这是无法排查的, 调用失败日志都在接入系统, 请求可能根本没到权限中心)

## 7. 参数校验失败: 单次授权自定义系统数最多 5 个

这是产品层面的限制

- 临时解决方案：分多次进行权限添加
- 最终解决方案：产品考虑是否开放给每个企业单独配置单次授权最大系统数量