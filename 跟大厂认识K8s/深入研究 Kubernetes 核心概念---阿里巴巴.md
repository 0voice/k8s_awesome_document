## 什么是 Kubernetes？

[Kubernetes](https://www.alibabacloud.com/product/kubernetes)是一个工业级的容器编排平台。Kubernetes 这个名字来源于希腊语，意思是舵手或飞行员。“K8s（或一些文章中的“ks”）是将八个字母“ubernete”替换为“8”的缩写。在下图中。

![image](https://user-images.githubusercontent.com/87457873/138668186-58571656-5c94-43e9-b9bf-0f9bce8859bc.png)

这是一艘载着一堆集装箱的船。这艘船正驶向大海，将集装箱运送到目的地。在英语中，这个词也意味着包装要运输的货物的“容器”。因此，从字面意思来看，Kubernetes 希望成为一艘运输集装箱的船。换句话说，它旨在帮助管理这些容器。所以用“Kubernetes”这个词来代表这个项目。更具体地说，Kubernetes 是一个自动化的容器编排平台，负责基于容器的应用程序的部署、弹性伸缩和管理。

## Kubernetes 的核心特性

**服务发现和负载平衡**

- **自动容器包装：**此功能也称为“调度”。通过将容器放置在集群中的节点上，Kubernetes 有助于编排存储系统，以便将存储的声明期与容器的生命周期联系起来。
- **自愈：** Kubernetes 有助于自动恢复失败的容器。在集群中，主机或操作系统问题可能会导致容器停止服务。如果是这种情况，Kubernetes 会自动恢复这些容器。
- **自动推出和回滚：** Kubernetes 有助于自动推出和回滚应用程序并管理与应用程序相关的配置密文。
- **批量执行：** Kubernetes 允许批量运行作业。
- **水平扩展：**为了使集群和应用程序更具弹性，Kubernetes 还支持水平扩展。

以下部分通过三个示例详细描述了 Kubernetes 的关键功能。

### 1) 调度

在Kubernetes中，用户提交的容器被部署到Kubernetes管理的集群中的一个节点上。Kubernetes 中的调度器是实现此功能的组件。它监视正在调度的容器的大小和规格。例如，调度器估计所需的 CPU 和内存容量，然后将容器放置在集群中相对空闲的节点上。在本例中，调度器可以将红色容器放置到第二个空闲节点上来完成调度任务。

![image](https://user-images.githubusercontent.com/87457873/138668423-a0c669e2-5066-45d7-937c-723aff782b6b.png)

### 2) 自动恢复

Kubernetes 提供节点健康检查。此功能允许系统监控集群中的所有主机。当主机或软件出现问题时，Kubernetes 会自动检测故障，并自动将运行在故障节点上的容器迁移到健康的主机上，以自动恢复集群中的容器。

!![image](https://user-images.githubusercontent.com/87457873/138668467-8159c5bb-fab1-4240-8e3d-09bd73e588f2.png)

### 3) 水平缩放

Kubernetes 能够通过监控来检查服务负载。如果服务的 CPU 使用率过高或对服务的响应过慢，Kubernetes 会相应地横向扩展该特定服务。在下面的例子中，第一个黄色节点过于繁忙，因此 Kubernetes 将黄色节点的负载分为三个部分。然后通过负载均衡，Kubernetes 将第一个黄色节点上的原始负载平均分配给三个黄色节点，包括第一个黄色节点本身，以提高响应速度。

![image](https://user-images.githubusercontent.com/87457873/138668507-9735d722-2526-45b0-8fcd-f0abf3c49d84.png)

## Kubernetes 架构

Kubernetes 架构是典型的两层服务器-客户端架构。Master作为中控节点，连接多个节点。所有 UI 客户端和用户端组件都连接到 Master，以向 Master 发送所需的状态或要执行的命令。然后，master 将这些命令或状态发送到相应的节点以供最终执行。

![image](https://user-images.githubusercontent.com/87457873/138668518-1a691c34-9f87-4840-97fb-a9b4dc81e20a.png)

在 Kubernetes 中，master 运行四个关键组件，包括 API 服务器、控制器、调度程序和 etcd。下图展示了详细的Kubernetes架构。

![image](https://user-images.githubusercontent.com/87457873/138668532-6ce06050-cff4-49f0-bcdb-ece07bec6f28.png)

- **API Server：**顾名思义，API Server 处理 API 操作。Kubernetes 中的所有其他组件都连接到 API 服务器。通常，这些组件不会单独相互连接。但是，它们依赖 API 服务器来相互传输消息。
- **控制器：** Kubernetes 附带的控制器监视和管理集群状态。例如，在前面的例子中，容器的自动恢复和自动水平扩展都是由 Kubernetes 中的控制器完成的。
- **调度器：**顾名思义，调度器执行调度。如第一个示例中所述，调度程序根据请求的 CPU 和内存容量将用户提交的容器放置到适当的节点上。
- **etcd：**它是一个分布式存储系统，API服务器所需的所有原始信息都存储在etcd中。作为一个高可用系统，etcd 负责保证 Kubernetes 中 master 的所有组件都是高可用的。

API 服务器是一个部署组件，允许在部署结构方面进行横向扩展。此外，控制器代表实现热备份的部署组件。只有一个控制器处于活动状态并具有其相应的调度程序。尽管如此，仍然可以实现热备份。

### Kubernetes 架构 - 节点

在 Kubernetes 中，服务负载实际上是由节点承载的，每个服务负载都作为一个 Pod 运行。Pod 的概念将在后面介绍。此外，一个或多个容器正在一个 Pod 中运行。实际运行这些 Pod 的组件称为**kubelet**，它也是节点上最关键的组件。它从 API 服务器接收所需 Pod 的运行状态，并将运行状态提交给如下图所示的容器运行时组件。

![image](https://user-images.githubusercontent.com/87457873/138668550-d28d5580-5b2f-4a56-a4ec-63889294d8ee.png)

管理存储和网络对于在操作系统上为容器创建运行环境并最终运行容器或 Pod 至关重要。Kubernetes 不直接执行任何存储或网络操作，而是依赖存储插件或网络插件来完成这些操作。通常，用户或云厂商开发相应的**存储插件**或**网络插件**来执行实际的存储或网络操作。

Kubernetes 还包括一个 Kubernetes 网络，它为联网提供服务网络。服务的概念将在后面介绍。真正完成服务联网的组件是**kube-proxy。**它利用 iptables 在 Kubernetes 中建立集群网络。到目前为止，您已经了解了节点上的所有四个组件。在 Kubernetes 中，节点不直接与用户交互，而是依赖于主节点。用户通过主节点将消息传递到节点。在 Kubernetes 中，每个节点都运行上述四个组件。

以下示例演示了这些组件如何在 Kubernetes 架构中相互交互。

![image](https://user-images.githubusercontent.com/87457873/138668571-11e49cc1-0b5e-407e-bd58-2653238d42bc.png)

用户可以通过 UI 或 CLI 向 Kubernetes 提交 pod 部署请求。此请求首先通过 CLI 或 UI 提交到 Kubernetes 中的 API 服务器。然后，API 服务器将请求信息写入 etcd 存储。最后，调度器通过 API 服务器的监视或通知机制获取这些信息。该信息表明需要调度 pod。

这时候调度器会根据自己的内存状态做出调度决策。完成调度后，向API服务器报告“OK！这个pod需要调度到某个节点”。

API server 收到此报告后，将调度结果写入 etcd。然后，API server 通知对应节点启动 pod。接收到这个通知后，对应节点上的 kubelet 会与容器运行时进行通信，真正开始配置容器和容器的运行环境。此外，kubelet 分别调度存储插件来配置存储和网络插件来配置网络。这个例子展示了这些组件如何相互通信并协同工作以完成 Pod 的调度。

## Kubernetes 的核心概念和 API

### 核心概念

#### 概念 1) Pod

Pod 是 Kubernetes 中最小的调度和资源单元。用户通过Kubernetes的Pod API创建一个Pod，由Kubernetes调度Pod。具体来说，pod 被放置并运行在由 Kubernetes 管理的节点上。简而言之，Pod 是一组容器的抽象，包含一个或多个容器。

如下图所示，pod包含两个容器，每个容器指定其所需的资源大小，比如1GB内存和1个CPU核心，或者0.5GB内存和0.5个CPU核心。

此 Pod 还包含其他所需资源，例如称为卷的存储资源，或 100 GB 或 20 GB 内存。

![image](https://user-images.githubusercontent.com/87457873/138668593-5799c1a0-f2a7-4dcd-b8bf-a3529412028d.png)

在 pod 中，定义运行容器的方式，例如运行容器的命令或环境变量。Pod 还为其中的容器提供了一个共享的运行环境。在这种情况下，这些容器共享一个网络环境，直接通过localhost相互查找。此外，Pod 之间是相互隔离的。

#### 概念 2) 体积

在 Kubernetes 中，卷用于管理存储并声明 Pod 中容器访问的文件目录。一个卷可以挂载到一个 Pod 中一个或多个容器的指定路径。

卷本身是一个抽象。一个卷支持多种类型的后端存储。比如Kubernetes中的volume就支持很多存储插件。支持本地存储，Ceph、GlusterFS等分布式存储，以及阿里云、AWS、谷歌磁盘等云存储。

![image](https://user-images.githubusercontent.com/87457873/138668614-af1c73c2-ec8e-4189-8d82-71b208e74142.png)

#### 概念 3) 部署

部署是 Pod 之上的抽象，它定义了一组 Pod 和 Pod 版本的副本数量。通常，这种抽象用于实际管理应用程序，而 Pod 是构成部署的最小单元。在 Kubernetes 中，控制器维护部署中的 Pod 数量，并帮助部署自动恢复失败的 Pod。例如，定义一个包含两个 Pod 的部署。如果一个 Pod 发生故障，相应的控制器会检测到故障并通过创建 Pod 将部署中的 Pod 数量从 1 恢复到 2。Kubernetes 中的控制器还允许我们实施已发布的策略，例如滚动升级、再生升级或版本回滚。

![image](https://user-images.githubusercontent.com/87457873/138668631-b95eb485-8eb4-4c4a-9c72-66668b15aa27.png)

#### 理念 4) 服务

一项服务为一个或多个 pod 实例提供静态 IP 地址。在前面的示例中，一个部署可能包括两个或多个相同的 Pod。对于外部用户，访问任何 Pod 都是一样的，因此首选负载均衡。为了实现负载均衡，用户希望访问一个静态虚拟 IP（VIP）地址，而不是知道所有 Pod 的具体 IP 地址。如前所述，一个 pod 可能处于终端 go（终止）状态。如果是这种情况，它可能会被一个新的 pod 替换。

对于外部用户，如果提供了多个 Pod 的特定 IP 地址，则该用户需要不断更新 Pod 的 IP 地址。如果 Pod 发生故障然后重新启动，则抽象可能会将对所有 Pod 的访问抽象为第三方 IP 地址。在 Kubernetes 中实现此功能的抽象称为服务。Kubernetes 支持多种服务入口模式，包括 ClusterIP、NodePort 和 LoadBalancer 模式。它还支持使用 kube-proxy 通过网络访问。

![image](https://user-images.githubusercontent.com/87457873/138668642-e54fd2b9-e094-4276-a6f9-656350d95d51.png)

#### 概念 5) 命名空间

命名空间用于在集群内实现逻辑隔离，涉及到身份验证和资源管理。Kubernetes 中的每个资源，例如 pod、部署和服务，都属于一个命名空间。资源名称在一个命名空间内必须是唯一的，但在不同的命名空间中可以相同。下面描述了命名空间的一个用例。在阿里巴巴，有很多业务部门（BU）。为了在视图级别隔离每个BU，使它们在认证和计算统一设备架构（CUDA）上有所不同，我们将使用命名空间为每个BU提供这样一种视觉隔离机制。

![image](https://user-images.githubusercontent.com/87457873/138668658-bfe73dd1-5b39-46fe-b594-3fa485164b5a.png)

### Kubernetes API

下图描述了 Kubernetes API 的基础知识。从高层的角度来看，Kubernetes API 是基于 HTTP 和 JSON 的。具体来说，用户通过HTTP访问API，访问的API内容为JSON格式。在 Kubernetes 中，kubectl 命令行工具、Kubernetes UI，有时甚至是 curl 用于基于 HTTP 和 JSON 直接与 Kubernetes 通信。在以下示例中，Pod 的 HTTP 访问路径由以下部分组成：API、apiVesion：V1、命名空间、Pod 和 Pod 名称。

![image](https://user-images.githubusercontent.com/87457873/138668678-fdd18de5-eacc-47fd-ac97-c4600b6795df.png)

相比之下，如果我们提交一个 pod 或者获取一个 pod，那么 pod 的内容是用 JSON 或 YAML 格式表示的。上图显示了一个 YAML 文件示例。在这个 YAML 文件中，pod 的描述由几个部分组成。

一般来说，第一部分是API**版本。**在本示例中，API 版本为 V1。第二部分是正在处理的资源类型。例如，如果资源的**种类**是一个 Pod，这个 Pod 的名称就写在元数据中。如果资源类型是Nginx，我们会**为其**添加一些**标签。**稍后将描述标签的概念。在元数据中，有时我们也会写**注解**，从用户的角度额外描述资源。

另一个重要部分是**规范，**它指示 pod 的所需状态。例如，规范显示了需要在 pod 中运行的容器、包含在 pod 中的 Nginx 容器的映像以及暴露端口的 ID。

当我们通过 Kubernetes API 获取该资源时，spec 通常会附带一个名为 status 的项，它表示该资源的当前状态。例如，一个 Pod 可能处于调度、运行或终止状态。终止状态意味着 pod 已经执行。

在描述 API 时，我们提到了一个有趣的元数据元素，称为**“标签”。**标签可以是一组键值对。例如，对于下图中的第一个 Pod，标签可能是红色，表示该 Pod 是红色的。也可以添加其他标签，例如size big，表示size定义为big。此外，还可以添加一组标签。这些标签由选择器查询。事实上，此功能与 SQL 选择语句的功能非常相似。例如，您可以从下图所示的三个 Pod 中进行选择。当颜色被命名为红色时，意味着一个 pod 的颜色是红色，注意只有两个 pod 被选中，因为只有它们的标签表示红色。另一个 pod 的标签说颜色是黄色，说明这个 pod 是黄色的，因此没有被选中。

![image](https://user-images.githubusercontent.com/87457873/138668700-5490b350-bee8-44d8-9d67-d4c116e9238b.png)

标签允许 Kubernetes API 过滤这些资源。过滤也是在 Kubernetes 中指示资源集合的默认方式。

例如，一个部署可能代表一组 pod，或者是一组 pod 的抽象。这组 pod 是通过使用标签选择器来指示的。如前所述，一项服务对应一个或多个 Pod，以集中方式访问它们。在这个描述中，pods 集也是由标签选择器选择的。

因此，标签是 Kubernetes API 的核心概念。在后续教程中，我们将深入探讨标签的概念以及如何充分利用标签。

## 示范

最后，让我们尝试一个 Kubernetes 集群演示。在此之前，请确保通过执行以下步骤在本地安装 Kubernetes 集群和 Kubernetes 沙箱环境：

- **第一步：**安装虚拟机，在虚拟机中启用Kubernetes。我们推荐使用 VirtualBox 作为虚拟机的运行环境。

安装前，从https://www.virtualbox.org/wiki/Downloads下载 VirtualBox

- **第二步：**在虚拟机中启动Kubernetes。Kubernetes 包含一个名为 minikube 的有趣工具。这是启动最小本地 Kubernetes 集群的环境。我们推荐使用[阿里云版本的 minikube](https://yq.aliyun.com/articles/221687)。这个 minikube 版本与官方 minikube 版本的主要区别在于，后者所需的 Google 特定依赖项被替换为在中国更容易访问的图像。这有利于安装。
- **第 3 步：**安装 VirtualBox 和 minikube 后，通过运行`minikube start —vm-driver virtualbox`启动命令启动 minikube 。

**注意：**如果您的电脑不是在Mac系统上运行，请访问下面这个[链接](https://kubernetes.io/docs/tasks/tools/install-minikube/)，查看如何在其他操作系统上安装minikube沙箱环境。

安装完成后，实现一个用例如下。

**1) 提交 Nginx 部署：** `kubectl apply -f https://k8s.io/examples/application/deployment.yaml`
**2) 更新 Nginx 部署：** `kubectl apply -f https://k8s.io/examples/application/deployment-update.yaml`
**3) 横向扩展 Nginx 部署：** `kubectl apply -f https://k8s.io/examples/application/deployment-update.yaml`

总而言之，首先提交一个 Nginx 部署，然后升级此部署的版本以更改其 pod 的版本。最后，横向扩展 Nginx 部署。现在让我们继续进行三个操作。首先，检查 minikube 的状态。输出显示 kubelet master 和 kubectl 都已正确配置。

![image](https://user-images.githubusercontent.com/87457873/138668738-e9e444a5-0144-4a35-b5a5-d73fd292d0d4.png)

然后通过kubectl查看这个集群中节点的状态。输出显示 master 正在运行。

![image](https://user-images.githubusercontent.com/87457873/138668755-d24bb18a-c53c-4139-a499-938a9ce49d42.png)

让我们检查一下基于master的集群中的部署。

![image](https://user-images.githubusercontent.com/87457873/138668774-79f4b4a9-3cbe-4b3b-bbc9-1c58c87ddb42.png)

输出显示集群不包括任何部署。使用监视语义查看集群中部署的更改。现在，它已准备好执行前面的三个操作。首先，创建部署。下面的第一张图显示了一个 API 的内容。具体来说，kind是一个deployment，名字是nginx-deployment。如第二张图，副本数为2，镜像版本为1.7.9。

![image](https://user-images.githubusercontent.com/87457873/138668795-758716c8-c230-4119-8644-1a655f944de1.png)

![image](https://user-images.githubusercontent.com/87457873/138668812-f598b06f-34b7-4ac7-ab72-d6f8bf038f64.png)

现在，运行 kubectl 命令来创建部署。请注意，一个简单的操作使部署能够不断生成副本。

![image](https://user-images.githubusercontent.com/87457873/138668828-e375ef83-1aa8-4d29-b31a-6dbc8fcb17ac.png)

副本数为 2。名为 nginx-deployment 的部署之前不存在。现在让我们描述此部署的当前状态。

在下图中，请注意已生成名为 nginx-deployment 的部署。副本数量随心所欲，selector满足要求，镜像版本也是1.7.9。此外，请注意名为 deployment-controller 的控制器正在管理生成。

![image](https://user-images.githubusercontent.com/87457873/138668839-72c6a596-605a-4c38-8854-56c955bd8f76.png)

接下来，让我们更新此部署的版本。首先，下载另一个名为`deployment-update.yaml.`Also 的YAML 文件，注意这个文件中的镜像版本从 1.7.9 更新到 1.8。

![image](https://user-images.githubusercontent.com/87457873/138668857-fdff54d9-aaed-42c2-821c-1b4eee0376cc.png)

然后，应用新`deployment-update.yaml file.`的本次部署更新的一些操作出现在另一侧的屏幕上，最新值从0变为2。这表明所有容器和pod都是最新的。执行describe命令查看所有Pod的版本是否已经更新。输出显示映像版本已从 1.7.9 更新到 1.8。

另外需要注意的是，控制器随后会执行几个新的操作来维护部署和 Pod 的状态。

![image](https://user-images.githubusercontent.com/87457873/138668875-ca1b818a-7d10-403a-bc6a-099612c3ae1b.png)

现在，让我们通过下载另一个来横向扩展部署。`deployment-scale.yaml file.`这个文件显示副本的数量已经从 2 变成了 4。

![image](https://user-images.githubusercontent.com/87457873/138668891-b71f371a-255d-4396-9ef0-5e3d7ad21eec.png)

回到初始窗口，使用 kubectl 将新的应用到`deployment-scale.yaml file.`另一个窗口中，注意`deployment-scale.yaml`应用文件后 pod 的数量从 2 变为 4 。再次描述当前集群中的部署。输出显示副本数量从 2 个增加到 4 个，并且控制器执行了几个新的操作。这表明放大已完成。

![image](https://user-images.githubusercontent.com/87457873/138668908-4ae0ba79-f826-42d2-9fe2-143bb2f6786c.png)

最后，让我们执行删除操作来删除生成的部署。如下图，kubectl delete deployment也是原deployment的名字。删除后，所有需要的操作都完成了。因此，此部署不再存在并且集群返回到其原始干净状态。

![image](https://user-images.githubusercontent.com/87457873/138668922-859f0f67-9643-4a37-a5bf-10ed7cea14a4.png)

## 结论

本文重点介绍Kubernetes的核心概念和架构设计，主要包括以下几点：

- Kubernetes 是一个自动化的容器编排平台。它负责部署、弹性伸缩和管理基于容器的应用程序。
- Kubernetes 架构是典型的两层服务器-客户端架构。
