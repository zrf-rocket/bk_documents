# 平台功能相关


## 为什么有的进程无法使用“访问控制台“功能

目前平台只对使用了最新镜像的应用开放了访问控制台的功能，如需要这个功能，需要：

1.在 “应用引擎” → “环境配置” → “修改运行时配置” 中 基础镜像选择： “蓝鲸基础镜像”

**注意**：切换基础镜像后，构建工具也需要重新选择

2.重新部署，保证进程是部署在最新的镜像上的