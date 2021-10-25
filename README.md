# 整理k8s（Kubernetes）的工程师资料，代码，项目，pdf，论文，视频，开源组件，各大厂内部分享资料

<br>  

<div align=center>
  
<img width="70%" height="70%" src="https://user-images.githubusercontent.com/87457873/138632184-e1f090e6-b95b-4b19-ab78-195bc9e46af4.png"/>
  
## ————【Docker容器化技术优秀“管家”】
  
<br>  
  
</div>

##  🤝跟大厂一起认识K8s

- [Kubernetes 的概述---官方](https://github.com/0voice/k8s_awesome_document/blob/main/%E8%B7%9F%E5%A4%A7%E5%8E%82%E8%AE%A4%E8%AF%86K8s/Kubernetes%20%E7%9A%84%E6%A6%82%E8%BF%B0.md)
- [Kubernetes是什么?---红帽redhat](https://github.com/0voice/k8s_awesome_document/blob/main/%E8%B7%9F%E5%A4%A7%E5%8E%82%E8%AE%A4%E8%AF%86K8s/Kubernetes%E6%98%AF%E4%BB%80%E4%B9%88%3F.md)
- [Kubernetes是什么?---mirantis](https://github.com/0voice/k8s_awesome_document/blob/main/%E8%B7%9F%E5%A4%A7%E5%8E%82%E8%AE%A4%E8%AF%86K8s/%E4%BB%80%E4%B9%88%E6%98%AF%20Kubernetes%EF%BC%9F---mirantis.md)
- [深入研究 Kubernetes 核心概念---阿里巴巴](https://github.com/0voice/k8s_awesome_document/blob/main/%E8%B7%9F%E5%A4%A7%E5%8E%82%E8%AE%A4%E8%AF%86K8s/%E6%B7%B1%E5%85%A5%E7%A0%94%E7%A9%B6%20Kubernetes%20%E6%A0%B8%E5%BF%83%E6%A6%82%E5%BF%B5---%E9%98%BF%E9%87%8C%E5%B7%B4%E5%B7%B4.md)

## 🏗相关开源项目

- [etcd-io/etcd](https://github.com/etcd-io/etcd)---Etcd是分布式系统中最关键的数据的分布式可靠的键值存储

- [istio/istio](https://github.com/istio/istio)---Istio是一个开放平台，提供统一的方式来集成微服务、管理微服务之间的流量、执行策略和聚合遥测数据。Istio的控制平面在底层集群管理平台(如Kubernetes)上提供了一个抽象层。

- [knative/docs](https://github.com/knative/docs)---基于kubernetes的平台来部署和管理现代的无服务器工作负载。

- [Helm](https://helm.sh/zh/)---Helm 帮助您管理 Kubernetes 应用——Helm 图表，即使是最复杂的 Kubernetes 应用程序，都可以帮助您定义，安装和升级。

- [prometheus/prometheus](https://github.com/prometheus/prometheus)---prometheus是云本地计算基金会的一个项目，是一个系统和服务监控系统。它以给定的时间间隔从配置的目标收集指标，计算规则表达式，显示结果，并在观察到指定的条件时触发警报。

- [linkerd/linkerd2](https://github.com/linkerd/linkerd2)---Linkerd是Kubernetes的一款超轻、安全优先的服务网。Linkerd为您的Kubernetes堆栈添加了关键的安全性、可观察性和可靠性特性，而不需要更改代码。

### Oracle
- [fn](https://github.com/fnproject/fn)---Fn是一个事件驱动的、开源的、功能即服务(FaaS)计算平台，可以在任何地方运行。
- [weblogic-kubernetes-operator](https://github.com/oracle/weblogic-kubernetes-operator)---支持在Kubernetes上运行WebLogic服务器和融合中间件基础架构域，Kubernetes是一个行业标准、云中立部署平台。它允许您将整个WebLogic Server安装和分层应用程序封装到一组可移植的云中立图像和简单的资源描述文件中。您可以在部署操作员的任何支持Kubernetes的本地云或公共云上运行它们。
- [mysql-operator](https://github.com/mysql/mysql-operator)---MYSQL Operator for Kubernetes是Kubernetes在Kubernetes集群中管理MYSQL InnoDB集群设置的操作符。
- [coherence-operator](https://github.com/oracle/coherence-operator)---通过支持Docker和Kubernetes等行业标准，Oracle允许使用Coherence的组织将其集群移动到云中，并促进在云中立的基础设施上运行Coherence。
- [verrazzano](https://github.com/verrazzano/verrazzano)---Verrazzano是一个端到端企业容器平台，用于在多云和混合环境中部署云本地和传统应用程序。它由一组精心设计的开源组件组成——许多您可能已经在使用和信任，还有一些是专门编写的，将所有组件组合在一起，使其成为一个内聚的、易于使用的平台。
- [oci-cloud-controller-manager](https://github.com/oracle/oci-cloud-controller-manager)---OCI - Cloud - Controller - Manager是Kubernetes云控制器管理器实现(或out- tree云提供商)，用于Oracle云基础设施(OCI)。
- [terraform-oci-oke](https://github.com/oracle-terraform-modules/terraform-oci-oke)---Oracle Container Engine (OKE)是Oracle在Oracle Cloud Infrastructure (OCI)上管理的Kubernetes服务。
- [fn-helm](https://github.com/fnproject/fn-helm)---这个图表使用Helm包管理器在Kubernetes集群上部署了Fn平台的一个功能完整的实例。
- [weblogic-image-tool](https://github.com/oracle/weblogic-image-tool)---Oracle WebLogic镜像工具
- [oci-service-broker](https://github.com/oracle/oci-service-broker)---Oracle Cloud Infrastructure Service Broker是面向OCI服务的开放服务代理API规范的开源实现。客户可以使用此实现在Kubernetes或其他Kubernetes集群的Oracle容器引擎中安装Open Service Broker。
- [fmw-kubernetes](https://github.com/oracle/fmw-kubernetes)---Kubernetes用于Oracle Fusion Middleware产品的部署脚本
- [oci-manager](https://github.com/oracle/oci-manager)---Kubernetes控制器集合，用于对Oracle云基础设施资源进行自治管理
- [oci-service-operator](https://github.com/oracle/oci-service-operator)---Kubernetes的OCI Service Operator (OSOK)可以方便地从Kubernetes环境中运行的云本地应用程序连接和管理OCI服务。
- [terraform-oci-olcne](https://github.com/oracle-terraform-modules/terraform-oci-olcne)---一个可重用和可扩展的Terraform模块，在Oracle云基础设施上提供Oracle Linux云本地环境。
- [mysql-ndb-operator](https://github.com/mysql/mysql-ndb-operator)---MySQL NDB Operator 是一个 Kubernetes 运算符，用于管理 Kubernetes 集群内的 MySQL NDB 集群设置。
- [weblogic-azure](https://github.com/oracle/weblogic-azure)---该项目支持在Azure Virtual Machines和Azure Kubernetes Service (AKS)中运行Oracle WebLogic Server。
- [zfssa-csi-driver](https://github.com/oracle/zfssa-csi-driver)---Kubernetes容器存储接口(CSI)插件用于Oracle ZFS存储设备。
- [weblogic-toolkit-ui](https://github.com/oracle/weblogic-toolkit-ui)---WebLogic Kubernetes Toolkit (WKT) 是一组开源工具，可帮助您配置基于 WebLogic 的应用程序以在 Kubernetes 集群上的 Linux 容器中运行。

## 📀学习视频

- [阿里云：课时1：Kubernetes核心概念]()
- [阿里云：课时2：理解Pod和容器设置模式]()
- [阿里云：课时3：应用编排与管理：核心原理]()
- [阿里云：课时4：应用编排与管理：Deployment]()
- [阿里云：课时5：应用编排与管理：Job和DaemonSet]()
- [阿里云：课时6：应用配置管理]()
- [阿里云：课时7：应用存储和持久化数据卷：核心知识]()
- [阿里云：课时8：应用存储和持久化数据卷：存储快照与拓扑调查]()
- [阿里云：课时9：可观测性-你的应用健康吗？]()
- [阿里云：课时10：可观测性：监控与日志]()
- [阿里云：课时11：Kubernetes网络概念及策略控制]()
- [阿里云：课时12：Kubernets Service]()

## 📂文档库
- [白皮书:Kubernetes如何拯救OpenStack](https://github.com/0voice/k8s_awesome_document/blob/main/%E6%96%87%E6%A1%A3/%E7%99%BD%E7%9A%AE%E4%B9%A6%EF%BC%9AKubernetes%E5%A6%82%E4%BD%95%E6%8B%AF%E6%95%91OpenStack.pdf)
- [2021年云原生行业研究报告](https://github.com/0voice/k8s_awesome_document/blob/main/%E6%96%87%E6%A1%A3/2021%E5%B9%B4%E4%BA%91%E5%8E%9F%E7%94%9F%E8%A1%8C%E4%B8%9A%E7%A0%94%E7%A9%B6%E6%8A%A5%E5%91%8A.pdf)



