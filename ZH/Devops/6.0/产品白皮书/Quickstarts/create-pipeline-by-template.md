# 使用模板创建流水线

## 准备事项

- 一个模板，若没有模板，请参考[开发一个流水线模板](../Services/Store/start-new-template.md)

## 入口

流水线服务下，创建流水线->从模板创建
![png](../assets/pipeline-create-by-template.png)

## 从模板创建流水线

![png](../assets/pipeline-create-by-template-1.png)

1. 流水线名称
2. 实例和模板的关系：
    - 自由模式：一旦创建，实例和模板之间再无关联，可以自由修改实例的参数、编排
    - 约束模式：实例始终受模板管控，只能修改流水线参数，不能修改编排、模板参数
3. 查看模板详情

## 创建约束模式流水线

![png](../assets/pipeline_constraint_create.png)

1. 模板版本
2. 约束模式流水线名称，可批量创建
3. 流水线变量，每个实例可以不同
4. 模板常量，不可以修改
5. 可选择是否继承模板设置

## 通过模板一键升级约束模式流水线

当模板升级后，可以一键升级约束模式的实例：
![png](../assets/pipeline_instances_list.png)

1. 选择多个实例后，批量更新
2. 差异对比，可查看升级前后的差异
