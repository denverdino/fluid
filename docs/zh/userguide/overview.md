# Fluid概览

## Fluid的功能目标与应用场景

Fluid是一款开源的云原生基础架构。在计算和存储分离的大背景驱动下，Fluid的目标是为AI与大数据云原生应用提供一层高效便捷的数据抽象，将数据从存储抽象出来，以便实现：
1. 通过数据亲和性调度和分布式缓存引擎加速，实现数据和计算之间的融合，从而加速计算对数据的访问。
2. 将数据独立于存储进行管理，并且通过Kubernetes的命名空间进行资源隔离，实现数据的安全隔离。
3. 将来自不同存储的数据联合起来进行运算，从而有机会打破不同存储的差异性带来的数据孤岛效应。

通过Kubernetes服务提供的该数据层抽象，就可以让数据像流体一样在诸如HDFS、OSS、Ceph这样的存储源和Kubernetes上层的云原生应用计算之间灵活高效地移动、复制、驱逐、转换和管理。而具体的数据操作对用户透明，用户不必再担心访问远端数据的效率，或是管理数据源的便捷性，以及如何帮助Kuberntes做出恰当的调度决策等运维问题。用户只需以Kubernetes原生数据卷的方式直接访问抽象出来的数据，剩余任务交给Fluid完成。

Fluid项目当前主要关注数据集编排和应用编排这两个重要场景。数据集编排可以将指定数据集的数据缓存到指定特性的Kubernetes节点；而应用编排将指定该应用调度到可以或已经存储了指定数据集的节点上。这两者还可以组合形成协同编排场景，即协同考虑数据集和应用需求进行节点资源调度。

## 为什么云原生需要Fluid
云原生环境与更早的大数据处理框架在设计理念和机制上存在天然分歧。深受Google三篇论文GFS、MapReduce、BigTable影响的Hadoop大数据生态，从诞生之初即信奉和实践“移动计算而不是数据”的理念。因此以Spark，Hive，MapReduce为代表的数据密集型计算框架及其应用为减少数据传输，其设计更多地考虑数据本地化架构。但随着时代的变迁，为兼顾资源扩展的灵活性与使用成本，计算和存储分离的架构在更新兴的云原生环境中大行其道。因此云原生环境里需要类似Fluid这样的一款组件来补充大数据框架拥抱云原生以后的数据本地性的缺失。

此外，在云原生环境中，应用通常以无状态（Stateless）微服务化方式部署并不以数据处理为中心；而数据密集型框架和应用通常以数据抽象为中心，开展相关计算作业和任务的分配执行。当数据密集型框架融入云原生环境后，也需要像Fluid这样以数据抽象为中心的调度和分配框架来协同。

针对当前Kubernetes缺乏对应用数据的感知和优化，以及像Alluxio这样的数据编排引擎难以直接驱动云原生应用等架构层的局限，Fluid提出将数据应用协同编排、智能感知、联合优化等一系列创新方法，并且基于Alluxio形成一套云原生场景下数据密集型应用的高效支撑平台。


具体的架构参见下图：
<div align="center">
  <img src="http://kubeflow.oss-cn-beijing.aliyuncs.com/Static/architecture.png" title="architecture" height="60%" width="60%" alt="">
</div>

## 演示
我们提供了视频的Demo，为您展示如何通过Fluid提升数据访问速度。

### 演示 1: 加速文件访问

[![](http://kubeflow.oss-cn-beijing.aliyuncs.com/Static/remote_file_accessing.png)](http://cloud.video.taobao.com/play/u/2987821887/p/1/e/6/t/1/277753111709.mp4)


### 演示 2: 加速机器学习

[![](http://kubeflow.oss-cn-beijing.aliyuncs.com/Static/machine_learning.png)](http://cloud.video.taobao.com/play/u/2987821887/p/1/e/6/t/1/277528130570.mp4)

## 快速体验Fluid
Fluid需要运行在 Kubernetes v1.14 及以上版本，并且需要支持CSI存储。Fluid Operator的部署和管理是通过 Kubernetes 平台上的包管理工具 Helm v3实现的。运行 Fluid前请确保 Helm 已经正确安装在 Kubernetes 集群里。

你可以参照参考文档 [docs](https://github.com/fluid-cloudnative/docs-fluid)，安装和使用Fluid。
- [English](docs/en/TOC.md)
- [简体中文](docs/zh/TOC.md)