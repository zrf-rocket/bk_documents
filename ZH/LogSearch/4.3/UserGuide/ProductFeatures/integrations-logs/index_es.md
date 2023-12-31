# 索引集管理

索引集管理为管理员提供索引集的增、删、查、改功能。

存储在 ES 中的日志要先通过建立索引集，才能进行查询。查询的对象为索引集。

![-w2020](media/2019-12-12-11-03-07.jpg)

**索引集列表字段解读**

索引集：用户自定义索引集合的名称，支持中英文。

索引：保存在 ES 中的 index。

数据分类：日志类型标签。

数据源：数据平台、采集接入、第三方 ES。

> 数据平台：指日志来自数据平台 ES；
>  采集接入：指日志来自日志检索内部采集；
>  第三方 ES：指接入用户独立的第三方 ES 集群。

集群名：用户独立的第三方 ES 集群的名字

## 新建索引集

在日志检索内采集接入的日志，会自动创建对应的索引集。

其他情况需要管理员手动创建索引集。

![-w2020](media/2019-12-13-10-29-12.jpg)

![-w2020](media/2019-12-13-10-29-37.jpg)

![-w2020](media/2019-12-13-10-14-41.jpg)

![-w2020](media/2019-12-13-10-16-53.jpg)

## 编辑索引集

编辑索引集可修改索引集名称、数据分类、增删索引、修改授权，不能修改数据源类型。

![-w2020](media/2019-12-13-10-31-15.jpg)


