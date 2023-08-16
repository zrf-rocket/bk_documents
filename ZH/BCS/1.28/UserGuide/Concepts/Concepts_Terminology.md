# 术语解释

了解 BCS，会涉及到以下基本概念：

- **容器编排引擎**：用于容器化应用的自动化部署、扩展和管理的工具或平台，目前行业主流的引擎 K8S。
- **集群**：容器运行所需要的物理机或虚拟机资源的集合。
- **节点**：一台已经注册到集群中的服务器，为集群提供计算资源。
- **应用**：由一组容器及服务构成集合，这个集合可以代表一个业务，或者业务的某个大区，在 K8S 中应用通常由工作负载（Workload）、服务（Service、Ingress）、配置（ConfigMap、Secret）构成。
- **Helm Release**：Release 是运行在 Kubernetes 集群中的 chart 的实例。一个 chart 通常可以在同一个集群中安装多次。每一次安装都会创建一个新的 release。以 MySQL chart为例，如果你想在你的集群中运行两个数据库，你可以安装该chart两次。每一个数据库都会拥有它自己的 release 和 release name
- **网络**：主要包含 **服务** 和 **负载均衡器** 的定义和管理，服务是由多个相同配置的容器和访问这些容器的规则组成的微服务，负载均衡器定义了访问规则的具体实现。
- **仓库**：用户存放 Docker 镜像、Helm Charts。