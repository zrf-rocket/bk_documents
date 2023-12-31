# 通过业务集实现跨业务的主机管控诉求

“业务集”是由一个或多个业务组合的资源空间，它与业务有直接的上下层关系；常见的管理使用场景多为公共平台职能团队，如数据库运维团队、中间件运维团队、基础运维团队等等；这些职能团队是跳脱在业务层之上的管理场景，通过“业务集”对符合属性条件的业务里的主机进行跨业务维度的消费。

### 创建业务集

![image-20220406113640869](media/image-20220406113640869.png)

在配置平台的 `资源` - `业务集` 页面中点击 `新建` 按钮，填写必要的信息（如业务集名、描述等），设定该业务集的业务范围条件，点保存。

### 查看业务集拓扑

![image-20220406113849744](media/image-20220406113849744.png)

前往一级导航 `业务` 下，通过业务选择器选择刚才创建的业务集，查看该业务集所包含的所有业务的拓扑集合。

### 在业务集下执行脚本

![image-20220406114117676](media/image-20220406114117676.png)

