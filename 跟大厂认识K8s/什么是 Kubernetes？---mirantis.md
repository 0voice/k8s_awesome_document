# 什么是 Kubernetes？
> 本文为译文，机器翻译而成，如有错误，请多多包涵

### Kubernetes 是一种软件，可自动管理、扩展和维护处于所需状态的多容器工作负载

![img](https://www.mirantis.com/wp-content/uploads/2021/03/k8s-mark-280x272-1.png)

现代软件越来越多地以容器队列的形式运行，有时也称为微服务。一个完整的应用程序可能包含许多容器，所有容器都需要以特定方式协同工作。Kubernetes 是一种软件，可将一组物理或虚拟主机（服务器)转变为一个平台：

- 托管容器化工作负载，为它们提供计算、存储和网络资源，以及
- 自动管理大量容器化应用程序——通过适应变化和挑战保持它们的健康和可用

## Kubernetes 是如何工作的？

1. 当开发人员创建一个多容器应用程序时，他们会计划所有部分如何配合和协同工作，每个组件应该运行多少，以及遇到挑战（例如，大量用户同时登录）时应该发生的大致情况。
2. 他们将容器化的应用程序组件存储在容器注册表（本地或远程）中，并在一个或多个包含*配置的*文本文件中捕获这种想法。为了启动应用程序，他们将配置“应用”到 Kubernetes。
3. Kubernetes 的工作是评估和实施此配置并维护它，直到另有说明。它：
   - 分析配置，将其要求与系统上运行的所有其他应用程序配置的要求保持一致
   - 查找适合运行新容器的资源（例如，某些容器可能需要并非在每个主机上都存在的 GPU 等资源）
   - 从注册表中获取容器映像，启动新容器，并帮助它们相互连接并连接到系统资源（例如，持久存储），使应用程序作为一个整体运行
4. 然后 Kubernetes 监控一切，当真实事件与预期状态不同时，Kubernetes 会尝试修复和适应。例如，如果容器崩溃，Kubernetes 会重新启动它。如果底层服务器出现故障，Kubernetes 会在别处寻找资源来运行该节点托管的容器。如果应用程序的流量突然激增，Kubernetes 可以根据配置中规定的规则和限制扩展容器以处理额外的负载。

## 为什么要使用 Kubernetes？

因为它使构建和运行复杂的应用程序变得更加简单。以下是众多 Kubernetes 功能中的一小部分：

- 大多数应用程序需要的标准服务，如本地 DNS 和基本负载平衡，并且易于使用。
- 易于调用的标准行为（例如，如果容器终止，则重新启动该容器），并完成保持应用程序运行、可用和高性能的大部分工作。
- 一组标准的抽象“对象”（称为“pods”、“replicasets”和“deployments”之类的东西），它们围绕着容器并使得围绕容器集合构建配置变得容易。
- 应用程序可以调用的标准 API，以轻松启用更复杂的行为，从而更轻松地创建管理其他应用程序的应用程序。

对“Kubernetes 的用途”的简单回答是，它为开发人员和运营商节省了大量时间和精力，让他们专注于为应用程序构建功能，而不是找出和实施保持应用程序良好运行的方法，在规模上。

通过在面临挑战（例如，服务器故障、容器崩溃、流量高峰等）的情况下保持应用程序运行，Kubernetes 还减少了业务影响，减少了使损坏的应用程序重新上线的消防演习的需要，并防止其他责任，如成本未能遵守服务水平协议 (SLA)。

## 我可以在哪里运行 Kubernetes？

Kubernetes 几乎可以在任何地方运行，可以在各种 Linux 操作系统上运行（工作节点也可以在 Windows Server 上运行）。单个 Kubernetes 集群可以跨越数据中心、私有云或任何公共云中的数百台裸机或虚拟机。Kubernetes 还可以在开发人员桌面、边缘服务器、微型服务器（如 Raspberry Pi）或非常小的移动和物联网设备和设备上运行。

通过一些深谋远虑（以及正确的产品和架构选择），Kubernetes 甚至可以提供跨所有这些基础设施的功能一致的平台。这意味着在桌面 Kubernetes 上编写和初步测试的应用程序和配置可以无缝快速地转移到更正式的测试、大规模生产、边缘或物联网部署。原则上，这意味着企业和组织可以跨一系列平台构建“混合”和“多云”，快速、经济地解决容量问题而不会被锁定。

## 什么是 Kubernetes 集群？

K8s架构比较简单。您永远不会直接与托管应用程序的节点进行交互，而只会与控制平面进行交互，该控制平面提供 API 并负责调度和复制名为 Pod 的容器组。Kubectl 是命令行界面，允许您与 API 交互以共享所需的应用程序状态或收集有关基础架构当前状态的详细信息。

让我们来看看不同的部分。

#### 节点

托管部分分布式应用程序的每个节点都通过利用 Docker 或类似的容器技术（例如 CoreOS 的 Rocket）来实现。这些节点还运行两个额外的软件：kube-proxy，它可以访问您正在运行的应用程序，以及 kubelet，它从 k8s 控制平面接收命令。节点还可以运行 flannel，这是一种由 etcd 支持的容器网络结构。

#### 掌握

控制平面本身运行 API 服务器 (kube-apiserver)、调度程序 (kube-scheduler)、控制器管理器 (kube-controller-manager) 和 etcd，这是一个用于共享配置和服务发现的高可用键值存储，实现了Raft 共识算法。

 [![图片缩略图](https://www.mirantis.com/wp-content/uploads/2021/03/k8s-arch-768x450.png)](https://www.mirantis.com/wp-content/uploads/2021/03/k8s-arch.png)

## 什么是“企业 Kubernetes”？

Kubernetes 本身为容器和资源管理、默认服务以及 API 提供了一个核心软件框架。它被设计为可通过标准接口进行扩展以提供重要的功能，例如：

- 运行容器——容器运行时或“引擎”
- 让容器通信——容器网络
- 提供持久化存储——容器存储解决方案
- 以安全有序的方式将入站流量路由到容器——入口解决方案
- 功能齐全的负载平衡——通过与外部负载平衡解决方案的集成，将入站流量均匀地分配给容器工作负载

… 以及许多其他对于高效使用和大规模运营必不可少的组件。为了让 Kubernetes 正常工作——您或其他人需要选择和集成解决方案来填补这些关键位置。

免费提供的 Kubernetes 替代方案通常从开源替代方案中进行选择以提供这些功能。这些通常是非常好的学习和小规模使用解决方案。

希望使用 Kubernetes 大规模运行生产软件的组织需要更多、更成熟的功能：

- 他们需要功能完整、加固且安全的 Kubernetes，并且可以轻松与集中 IT 资源（如目录服务、监控和可观察性、通知和票务等）集成。
- 他们需要能够以一致的方式部署、扩展、管理和更新的 Kubernetes，或许可以跨多种不同类型的基础设施。
- 他们需要将 Kubernetes 的所有不同部分一起进行验证，并由一个供应商提供支持。

“企业 Kubernetes”是指满足这些需求的产品和产品套件：用同类最佳的解决方案填充 Kubernetes 的所有功能槽，解决跨多个基础设施的 Kubernetes 管理问题，实现一致性，并提供完整的支持。

## 如何开始使用 Kubernetes？

Mirantis 制作了多种 Kubernetes 解决方案，适用于不同的用途。我们的开源产品可以在社区支持下免费使用。我们的旗舰产品可以免费试用，并提供分层支持直至完全托管的服务。

[**Mirantis Container Cloud**](https://www.mirantis.com/software/docker/docker-enterprise-container-cloud/)（以前称为 Docker Enterprise Container Cloud）是一种用于在任何基础架构上部署、观察、管理和无中断更新 Kubernetes（以及在 Kubernetes 之上运行的其他应用程序，如容器化 OpenStack）的解决方案 - 如果您需要以安全、简单和自由选择的方式大规模可靠地运行 Kubernetes。([下载 Mirantis Container Cloud](https://www.mirantis.com/download/container-orchestration/mirantis-container-cloud/) )

[**Mirantis Kubernetes Engine**](https://www.mirantis.com/software/docker/docker-enterprise/)（以前称为 Docker Enterprise/UCP）是完全成熟的 Enterprise Kubernetes，用于开发、测试和生产。它包括用于轻松管理的通用控制平面 webUI、用于私有容器映像存储和安全扫描的 Mirantis Secure Registry（以前称为 Docker Trusted Registry），并在 Mirantis Container Runtime（以前称为 Docker Engine – Enterprise）上运行——一种具有可选 FIPS 的强化容器运行时140-2 加密和其他安全性和可靠性功能。（[下载 Mirantis Kubernetes Engine](https://www.mirantis.com/download/container-orchestration/mirantis-kubernetes-engine/)）

[**K0S**](https://k0sproject.io/) –（发音为“K-zeroes”）是零摩擦的开源 Kubernetes，它从一个命令开始，几乎可以在任何规模的 Linux 上运行，从 Raspberry Pi 到巨型数据中心。是我们学习者的最佳选择。([下载 k0s – 零摩擦 Kubernetes](https://www.mirantis.com/download/open-source/k0s-zero-friction-kubernetes/) )

最后，[**Lens – 开源 Kubernetes IDE**](https://www.mirantis.com/software/lens/)，加速了 Kubernetes 的学习和开发。Lens 让您可以使用上下文感知终端轻松管理多个 Kubernetes 集群并与之交互、可视化其中的对象层次结构、查看容器日志、直接登录到容器命令 shell 等。（[下载 Lens – Kubernetes IDE](https://www.mirantis.com/download/open-source/lens-kubernetes-ide/)）
