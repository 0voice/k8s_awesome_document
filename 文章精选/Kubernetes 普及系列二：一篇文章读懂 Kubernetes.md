### 简介

Kubernetes 是一个 **可移植的**、**可扩展的** 开源平台，用于管理 **容器化的** 工作负载和服务，可促进 **声明式** 配置和 **自动化**。Kubernetes 拥有一个庞大且快速增长的 **生态系统** 。Kubernetes 的服务、支持和工具广泛可用。

#### 可移植的

Kubernetes 的系统组件采用 Go 语言开发，系统组件均具备较强的移植性，可以以较低成本移植到各种主流服务器操作系统以及计算平台中。

#### 可扩展的

Kubernetes 自身只负责建立工作负载、服务、网络、存储的声明式规范，以及实现资源管理，服务调度等算法。Kubernetes 自身并不负责实现容器的计算，网络以及存储能力，而是通过遵循 CRI，CNI、CSI 规范来对计算，网络，存储能力提供支持。

使用者可以通过开发与集成自己需要的插件来打造属于自己的 Kubernetes 集群，只要相应的插件能够符合 CRI、CNI、CSI 等标准。

#### 容器化的

Kubernetes 的设计之初是为了解决复杂的容器化服务群难以管理，调度，维护的问题，所以可以说 Kubernetes 是面向容器化计算而生的。但是这也不是绝对的，随着 Kubernetes 的普及，社区中已经出现了许多虚拟机以及物理机插件用于让 Kubernetes 能够管理和调度非容器化的计算资源。

#### 声明式

Kubernetes 将应用、服务、网络、配置等逻辑资源都抽象成了各种资源对象，作为使用者，需要以声明式的方式编写资源对象清单文件，通过向 Kubernetes 集群传递资源对象清单文件可以定义集群中有哪些资源，以及这些资源预期的状态、行为是什么。

#### 自动化

当我们将资源对象清单文件传递给了 Kubernetes 之后，Kubernetes 强大的自动化能力会自动创建，更新和维护集群内相关资源的，尽可能的使得真实运行的资源对象达到我们所预期的状态与行为。

#### 生态系统

Kubernetes 本身属于开源软件，其开放的扩展能力也为许多第三方工具、软件、服务提供了便捷的集成能力。鉴于此社区中已经有大量成熟和新兴的工具，平台，服务能够支持与 Kubernetes 集群，进一步延展了 Kubernetes 的使用场景并形成了一个庞大的体系及生态。

*在本文尾部笔者将与大家分享 Kubernetes 相关的工具，插件，服务。*

### 解决了什么问题

在了解 Kubernetes 解决了我们什么问题之前，我们先复习一下软件系统部署模式的演变，然后再探讨 Kubernetes 解决了什么问题，以及带来了一些什么新的特性。

![软件系统运行环境的演变](https://help-assets.codehub.cn/enterprise/1%E3%80%81container_evolution-01.png)

#### 传统部署模式

在软件行业与互联网普及的初期，我们开发的应用/网站相对来说都较为简单，这个时候我们通常会准备一台服务器设备，在这个服务器设备中安装基本的操作系统，然后将我们的应用/网站直接部署在这台服务器中，因为开发的应用/网站非常简单（可能是个人博客，企业网站，简单的 CMS 或 BBS 系统），加上用户基数较小，只需要一台服务器提供计算、网络、存储资源就足以承载应用所需的运行条件。甚至在资源充裕，为了便于管理和维护，我们会将多个应用部署在同一台服务器设备中。

##### 不足之处

###### 扩展性差

这种传统的部署模式适合业务稳定且用户规模较小的网站，应用，如果用于部署具有业务增长趋势的应用时扩展性有很大局限，当规模（业务规模与用户规模）增长至单台服务器上的资源已无法满足稳定运行条件时，服务器的扩容是非常困难的，我们除了要对应用进行分布式改造之外，还需要额外购买和托管新的服务器设备、安装操作系统、部署应用、链接服务。

###### 安全性较低

当我们将一台资源过剩的服务器用于部署多个应用（从而避免资源浪费）的情况下，因为缺少一定的隔离策略，应用越多安全风险也骤然升高，因为多个应用都运行在同一操作系统中，假如其中一个应用存在安全漏洞使得黑客能够通过这个漏洞入侵到操作系统层面，那么这台服务器上所有的应用的数据及安全就受到了威胁。

###### 维护成本高

因为是物理服务器部署，物理服务器通常都被托管在 IDC 机房当中，我们需要远程操作就必须保证操作系统和网络是正常且可以访问的。所以涉及系统级的备份与还原异常困难，必须需要前往机房现场进行操作。日常对操作系统或应用进行配置的时候也要格外小心，一旦配置项导致网络断线或者损坏操作系统启动项导致系统无法启动，也只能前往机房现场调试修复了，这些故障都属于灾难性的。

###### 资源分配不均

当我们在同一台服务器设备中部署多个应用，该服务器设备的资源都被操作系统管理并分配和使用，操作系统并不能为特定的应用分配特定的资源，导致我们很难去维护和配置不同应用之间对资源的配额，操作系统很可能把大量的资源分配给了不重要的应用，导致重要的应用无法更高效的运行，甚至可能因为资源不足被系统驱逐。

###### 部分条件受限

因为缺少一定的隔离策略，部署应用会受到一些特定的限制，例如有些应用所依赖的运行时或组件需要系统级的注册，而同名不同版本的运行时或组件只能在系统中注册一个实例，导致部分应用无法使用所依赖的特定版本运行时或组件。

#### 虚拟化部署模式

虚拟化技术能够让我们将一台服务器设备虚拟化成多台虚拟服务器设备，我们可以对每台虚拟服务器分配资源配额，每台虚拟服务器设备都具有自己的 Guest OS 环境，虚拟服务器之间是完全隔离的。

通过合理的规划应用和虚拟服务器部署的排列组合关系，能够较好的解决传统部署模式的部分不足。

##### 不足之处

###### 性能较差，资源利用率较低

因为每个虚拟机都是独立且完整的计算机系统，虚拟机可能占用主机的大量资源用于运行其操作系统服务。在虚拟服务器上运行单个应用意味着还要运行 Guest OS 以及 Guest OS 运行所需的所有硬件的虚拟副本，这样无疑增加了资源的耗损。

###### 扩展性较差

将我们的应用打包到虚拟机镜像中，每当我们需要扩容一个新的应用实例，可以通过虚拟机镜像在虚拟化平台创建新的虚拟服务器实例，但是因为虚拟机镜像中包含完整的 Guest OS 数据，每当创建新的虚拟服务器实例时将消耗大量磁盘与时间资源。往往为一个非常小的应用创建虚拟服务器实例，直到应用启动完成需要耗时 20 分钟以上。

###### 维护成本较高

当我们需要对应用进行备份/还原、迁移的维护操作时，与创建一个新的应用副本一样，也需要对完整的 Guest OS 数据进行操作，所以也会需要消耗很大的存储空间及时间。

虚拟机技术只解决了应用的运行环境问题，并没有提供一套高度自动化的工具帮助我们更有效的对应用进行调度、扩所容、升级回滚，所有的维护性工作几乎全部要人工操作。

#### 容器化部署模式

在容器化部署模式中，我们将应用打包成容器镜像，当需要运行多个应用副本时，我们会基于容器镜像运行多个容器实例。容器中的进程本质上是运行在宿主机上的一种特殊的进程，而多个容器之间能够共用同一个宿主机的操作系统内核。

因为容器可以共用宿主机系统内核，所以将应用打包成容器镜像时可以大幅度缩减容器镜像的体积，并且因为容器运行时可以共用宿主机内核所以运行一个应用除了该应用自身的开销，并不会产生额外的资源损耗。

##### 不足之处

###### 维护成本较高

容器化技术也只是解决了应用运行环境的问题，并没有提供一套高度自动化的工具帮助我们更有效的对应用进行调度、扩所容、升级回滚，所有的维护性工作几乎全部要人工操作。

#### Kubernetes 部署模式

Kubernetes 包含了对容器化技术的使用，通过容器化镜像解决应用打包与分发问题，通过容器化运行时解决应用运行环境的问题。Kubernetes 提供了一系列资源对象抽象，用户通过对这些对象进行声明从而告诉 Kubernetes 期望的资源状态及行为是什么，之后 Kubernetes 强大的自动化系统会尽可能使得集群中的工作负载、服务、网络、配置项等资源尽可能与用户期望的保持一致。

##### Kubernetes 特点

- 服务发现和负载均衡
  Kubernetes 可以使用 DNS 名称或自己的 IP 地址公开容器，如果进入容器的流量很大， Kubernetes 可以负载均衡并分配网络流量，从而使部署稳定。
- 存储编排
  Kubernetes 允许你自动挂载你选择的存储系统，例如本地存储、公共云提供商等。
- 自动部署和回滚
  你可以使用 Kubernetes 描述已部署容器的所需状态，它可以以受控的速率将实际状态 更改为期望状态。例如，你可以自动化 Kubernetes 来为你的部署创建新容器， 删除现有容器并将它们的所有资源用于新容器。
- 自动二进制打包
  Kubernetes 允许你指定每个容器所需 CPU 和内存（RAM）。 当容器指定了资源请求时，Kubernetes 可以做出更好的决策来管理容器的资源。
- 自我修复
  Kubernetes 重新启动失败的容器、替换容器、杀死不响应用户定义的 运行状况检查的容器，并且在准备好服务之前不将其通告给客户端。
- 密钥与配置管理
  Kubernetes 允许你存储和管理敏感信息，例如密码、OAuth 令牌和 ssh 密钥。 你可以在不重建容器镜像的情况下部署和更新密钥和应用程序配置，也无需在堆栈配置中暴露密钥。

## Kubernetes 架构

### 物理架构（系统组件）【摘选自 Kubernetes 官网】

![系统组件](https://help-assets.codehub.cn/enterprise/2%E3%80%81components-of-kubernetes-01.png)

#### Control Plane 中的组件

Control Plane 的组件对集群做出全局决策（比如调度），以及检测和响应集群事件（例如，当不满足部署的 Replicas 字段时，启动新的 Pod）。

Control Plane 组件可以在集群中的任何节点上运行。然而，为了简单起见，设置脚本通常会在同一个计算机上启动所有 Control Plane 组件，并且不会在此计算机上运行用户容器。

##### API Server

API Server 组件公开了 Kubernetes API。API Server 是 Kubernetes Control Plane 的前端。Kubernetes API 服务器的主要实现是 kube-apiserver。Kube-apiserver 设计上考虑了水平伸缩，也就是说，它可通过部署多个实例进行伸缩。你可以运行 kube-apiserver 的多个实例，并在这些实例之间平衡流量。

##### Etcd

Etcd 是兼具一致性和高可用性的键值数据库，可以作为保存 Kubernetes 所有集群数据的后台数据库。

##### Scheduler

Scheduler 组件负责监视新创建的、未指定运行节点（Node）的 Pods，选择节点让 Pod 在上面运行。

调度决策考虑的因素包括单个 Pod 和 Pod 集合的资源需求、硬件/软件/策略约束、亲和性和反亲和性规范、数据位置、工作负载间的干扰和最后时限。

##### Controller Manager

从逻辑上讲，每个 Controller 都是一个单独的进程， 但是为了降低复杂性，它们都被编译到同一个可执行文件，并在一个进程中运行。

这些控制器包括:

- 节点控制器（Node Controller）: 负责在节点出现故障时进行通知和响应
- 副本控制器（Replication Controller）: 负责为系统中的每个副本控制器对象维护正确数量的 Pod
- 端点控制器（Endpoints Controller）: 填充端点(Endpoints)对象(即加入 Service 与 Pod)
- 服务帐户和令牌控制器（Service Account & Token Controllers）: 为新的命名空间创建默认帐户和 API 访问令牌

##### Cloud Controller Manager (可选)

Cloud Controller Manager 是指嵌入特定云的控制逻辑的 控制平面组件。Cloud Controller Manager 允许您链接聚合到云提供商的应用编程接口中，并分离出相互作用的组件与您的集群交互的组件。

Cloud-controller-manager 仅运行特定于云平台的控制回路。如果你在自己的环境中运行 Kubernetes，或者在本地计算机中运行学习环境，所部署的环境中不需要 Cloud Controller Manager。

与 kube-controller-manager 类似，cloud-controller-manager 将若干逻辑上独立的控制回路组合到同一个可执行文件中，供你以同一进程的方式运行。你可以对其执行水平扩容（运行不止一个副本）以提升性能或者增强容错能力。

下面的控制器都包含对云平台驱动的依赖：

- 节点控制器（Node Controller）: 用于在节点终止响应后检查云提供商以确定节点是否已被删除
- 路由控制器（Route Controller）: 用于在底层云基础架构中设置路由
- 服务控制器（Service Controller）: 用于创建、更新和删除云提供商负载均衡器

#### Node 中的组件

Node 组件在每个节点上运行，维护运行的 Pod 并提供 Kubernetes 运行环境。

##### Kubelet

一个在集群中每个节点（Node）上运行的代理。 它保证容器（Containers）都运行在 Pod 中。

Kubelet 接收一组通过各类机制提供给它的 PodSpecs，确保这些 PodSpecs 中描述的容器处于运行状态且健康。Kubelet 不会管理不是由 Kubernetes 创建的容器。

##### Kube-proxy

Kube-proxy 是集群中每个节点上运行的网络代理， 实现 Kubernetes 服务（Service） 概念的一部分。
Kube-proxy 维护节点上的网络规则。这些网络规则允许从集群内部或外部的网络会话与 Pod 进行网络通信。
如果操作系统提供了数据包过滤层并可用的话，kube-proxy 会通过它来实现网络规则。否则， kube-proxy 仅转发流量本身。

##### 容器运行时（Container Runtime）

容器运行环境是负责运行容器的软件。
Kubernetes 支持多个容器运行环境: Docker、 containerd、CRI-O 以及任何实现 Kubernetes CRI (容器运行环境接口)。

#### 插件（Addons）

插件使用 Kubernetes 资源（DaemonSet、 Deployment等）实现集群功能。 因为这些插件提供集群级别的功能，插件中命名空间域的资源属于 kube-system 命名空间。下面描述众多插件中的几种——

##### DNS

尽管其他插件都并非严格意义上的必需组件，但几乎所有 Kubernetes 集群都应该 有集群 DNS， 因为很多示例都需要 DNS 服务。

集群 DNS 是一个 DNS 服务器，和环境中的其他 DNS 服务器一起工作，它为 Kubernetes 服务提供 DNS 记录。Kubernetes 启动的容器自动将此 DNS 服务器包含在其 DNS 搜索列表中。

##### Web 界面（Dashboard）

Dashboard 是 Kubernetes 集群的通用的、基于 Web 的用户界面。 它使用户可以管理集群中运行的应用程序以及集群本身并进行故障排除。

##### 容器资源监控

容器资源监控，将关于容器的一些常见的时间序列度量值保存到一个集中的数据库中，并提供用于浏览这些数据的界面。

##### 集群层面日志

集群层面日志，机制负责将容器的日志数据保存到一个集中的日志存储中，该存储能够提供搜索和浏览接口。

### 逻辑架构（用户资源对象）

[![用户资源对象](https://help-assets.codehub.cn/enterprise/3%E3%80%81objects-of-users.png)](https://help-assets.codehub.cn/enterprise/3、objects-of-users.png)用户资源对象

上图是一个简单且常见的，通过 Kubernetes 承载和调度的系统。下面让我们来简单分析一下应用是如何运行，以及网络流量是如何到达应用的。

#### 工作负载相关

Controller 和 Pod 对象属于 Kubernetes 工作负载类对象，Pod 用于运行实际的应用程序容器，Controller 通过 Selector 选取特定 Labels 的 Pods 从而确定和它们之间的关系，Controller 会持续检查 Pods 是否按预期的状态和数量运行，当满足 Selector 的 Pod 数量小于 Controller 所预期的副本数量，Controller 会自动创建并运行新的 Pod，并为它添加对应的 Lables。

#### 网络负衡相关

Ingress 和 Service 对象属于 Kubernetes 网络负载对象，Service 和 Controller 类似，都是通过 Selector 选取特定 Labels 的 Pods 从而确定和它们之间的关系。

Ingress 根据客户端所发出的 URL 特征对流量进行分发，反向代理至目标 Service 上，Service 会根据其自身配置结合算法将流量转发至特定 Pod 中处理。

## 拓展内容：Kubernetes 相关工具，插件

### Kubeadm

Kubeadm 是 Google 开源的一个用于安装和初始化 Kubernetes 集群实例的工具，通过使用 Kubeadm 可以快速搭建满足最佳实践的 Kubernetes 集群。

相关链接：[Kubeadm](https://github.com/kubernetes/kubeadm)

### Kubespray

Kubespray 是 Google 开源的一个部署生产级别的 Kubernetes 服务器集群的开源项目，它整合了 Ansible 作为部署的工具。

相关链接：[Kubespray](https://github.com/kubernetes-sigs/kubespray)

### Minikube

Minikube 在 macOS、Linux 和 Windows 上实现了本地 Kubernetes 集群。Minikube 的主要目标是成为本地 Kubernetes 应用程序开发的最佳工具，并支持所有合适的 Kubernetes 功能。

相关链接：[minikube](https://github.com/kubernetes/minikube)

### Microk8s

Microk8s 是一款适用 42 种 Linux 发行版的完全符合标准的、轻量级的单机 Kubernetes，适用于：

- 开发人员工作站
- 物联网
- 边缘计算
- CI/CD

相关链接：[microk8s](https://github.com/ubuntu/microk8s)

### K3s

K3s 是轻量级的 Kubernetes，可用于生产，易于安装，只需要标准 Kubernetes 一半的内存，所有二进制文件不到 100MB 的 Kubernetes，适用于：

- 边缘计算
- 物联网
- CI
- 开发环境
- ARM
- 嵌入式系统

相关链接：[k3s](https://github.com/k3s-io/k3s)

### Kubectl

Kubectl 是 Kubernetes 官方开源的 Kubernetes 命令行客户端工具，使用 kubectl 可以连接并管理目标 Kubernetes 集群

相关链接：[kubectl](https://github.com/kubernetes/kubectl)

### Lens

Lens 是一款开源、免费、功能强大、易用的 Kubernetes 图形化客户端工具，支持 macOS、Windows 和 Liunx 操作系统

相关链接：[lens](https://github.com/lensapp/lens)

### Ingress-nginx

Ingress-nginx 是使用 Nginx 作为反向代理和负载均衡器的 Kubernetes Ingress 控制器。

相关链接：[ingress-nginx](https://github.com/kubernetes/ingress-nginx)

### Traefik

Traefik 是一个为了让部署微服务更加便捷而诞生的现代 HTTP 反向代理、负载均衡工具，它可以作为 Kubernetes Ingress 控制器使用。

相关链接：[traefik](https://github.com/traefik/traefik)

### MetalLB

MetalLB 是符合标准路由协议的，用于裸机 Kubernetes 集群使用的软件负载均衡器，它可以弥补自建 Kubernetes 因为没有硬件负载均衡器导致无法使用 LoadBalancer 类型 Service 的功能缺陷

相关链接：[MetalLB](https://github.com/metallb/metallb)

### Longhorn

Longhorn 是 Kubernetes 的分布式块存储系统，它轻巧，可靠且功能强大。

相关链接：[Longhorn](https://github.com/longhorn/longhorn)
