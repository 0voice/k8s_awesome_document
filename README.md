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
- [Kubernetes 开源知识---华为](https://github.com/0voice/k8s_awesome_document/blob/main/%E6%96%87%E6%A1%A3/Kubernetes%20%E5%BC%80%E6%BA%90%E7%9F%A5%E8%AF%86.pdf)

## 🚩核心组件
- [etcd cluster](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/) –存储Kubernetes集群数据的分布式密钥值存储
- [kube-apiserver](https://kubernetes.io/docs/reference/generated/kube-apiserver/) – 接收所有修改集群元素的REST请求的中央管理实体
- [kube-controller-manager](https://kubernetes.io/docs/reference/generated/kube-controller-manager/) – 运行控制器进程，如复制控制器(设置pod中的副本数量)和端点控制器(填充服务、pod和其他对象)
- [cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager) – 负责管理依赖于底层云提供商的控制器流程
- [kube-scheduler](https://kubernetes.io/docs/reference/generated/kube-scheduler/)– 帮助根据资源利用率调度集群节点上的pod(应用程序进程在其中运行的一组共存的容器)

## 🏗相关开源项目

- [etcd-io/etcd](https://github.com/etcd-io/etcd)---Etcd是分布式系统中最关键的数据的分布式可靠的键值存储

- [knative/docs](https://github.com/knative/docs)---基于kubernetes的平台来部署和管理现代的无服务器工作负载。


### K8s集群部署工具

- [Kubespray](https://github.com/kubernetes-incubator/kubespray)---Kubespray为Kubernetes的部署和配置提供了一组Ansible角色。Kubespray可以使用AWS、GCE、Azure、OpenStack或裸金属基础设施即服务(IaaS)平台。Kubespray是一个开放开发模型的开源项目。对于已经了解Ansible的人来说，这个工具是一个很好的选择，因为不需要使用其他工具来进行配置和编排。Kubespray在引擎盖下使用了kubeadm。

- [Minikube](https://github.com/kubernetes/minikube)---Minikube允许您在本地安装和试用Kubernetes。该工具是Kubernetes探索的一个很好的起点。在笔记本电脑上的虚拟机(VM)中轻松启动单节点Kubernetes集群。Minikube支持Windows、Linux和OSX操作系统。在短短5分钟内，您将能够探索Kubernetes的主要功能。只需一个命令就可以直接启动Minikube仪表板。

- [Kubeadm](https://github.com/kubernetes/kubeadm)---Kubeadm是Kubernetes的1.4版发布工具。该工具有助于在现有基础设施上引导最佳实践Kubernetes集群。但是Kubeadm不能为你提供基础设施。它的主要优势是能够在任何地方启动最小可行的Kubernetes集群。插件和网络设置都超出了Kubeadm的范围，所以您需要手动安装或使用其他工具。

- [Kops](https://github.com/kubernetes/kops)---Kops帮助您从命令行创建、销毁、升级和维护生产级高可用的Kubernetes集群。Amazon Web Services (AWS)目前得到官方支持，GCE支持测试版，VMware vSphere支持测试版，其他平台支持也在计划之中。Kops允许您控制Kubernetes集群的完整生命周期;从基础设施配置到集群删除。

- [Bootkube](https://github.com/kubernetes-incubator/kube-aws)---Kube-AWS是CoreOS提供的控制台工具，使用AWS CloudFormation部署一个功能齐全的Kubernetes集群。Kube-AWS允许您部署一个传统的Kubernetes集群，并自动提供带有本地AWS特性的每个k8服务(例如，ELB、S3和Auto Scaling，等等)。
- [JAAS](https://jaas.ai/)---JAAS是Juju作为一种服务，它简化了配置、扩展和操作当今复杂软件的方式。Juju部署在任何地方:公共云或私有云。JAAS将您的工作负载部署到您选择的云。

- [Conjure-up](https://conjure-up.io/)---Conjure-up是另一个Canonical产品，它允许你用几个简单的命令部署“Kubernetes在Ubuntu上的Canonical分布”。支持AWS、GCE、Azure、Joyent、OpenStack、VMware、裸金属、本地主机部署。Juju, MAAS和LXD是magic -up的基础技术。

- [Amazon EKS]( https://aws.amazon.com/eks/)---Amazon Elastic Container Service for Kubernetes (Amazon EKS)是一种托管服务，可以使用Kubernetes简单地部署、管理和扩展容器化应用。Amazon EKS跨多个AWS可用区管理您的Kubernetes基础设施，同时自动检测和替换不健康的控制平面节点，并提供按需升级和补丁。您只需提供工作节点并将它们连接到所提供的Amazon EKS端点。

### 监控工具

- [Kubebox](https://github.com/astefanutti/kubebox)---Kubebox是Kubernetes集群的终端控制台，它允许您使用漂亮的老式界面来管理和监控集群活动状态。Kubebox显示pod资源使用情况、集群监控和容器日志等。此外，您可以轻松导航到所需的名称空间，并执行到所需的容器中，以便快速进行故障排除/恢复。

- [Kubernetes Operational View (Kube-ops-view)](https://github.com/hjacobs/kube-ops-view)---Kube-ops-view是用于多个k8集群的只读系统仪表板。使用Kube-ops-view，您可以轻松地在集群和监视节点之间导航，以及pod的健康状况。Kube-ops-view动画一些Kubernetes过程，如pod的创建和终止。

- [Kubetail](https://github.com/johanhaleby/kubetail)---Kubetail是一个小型的bash脚本，它允许您将多个pod的日志聚合到一个流中。最初的Kubetail版本没有过滤或突出显示功能，但在Github上有一个额外的Kubetail分叉。这可以使用多尾工具形成和执行日志着色。

- [Kubewatch](https://github.com/bitnami-labs/kubewatch)---Kubewatch是Kubernetes的一个观察者，它可以将K8s事件发布到团队沟通应用Slack上。Kubewatch作为Kubernetes集群中的pod运行，监控系统中发生的更改。您可以通过编辑配置文件来指定要接收的通知。

- [Weave Scope](https://www.weave.works/oss/scope/)---Weave Scope是一个用于Docker和Kubernetes集群的故障排除和监控工具。它可以自动生成应用程序和基础结构拓扑，帮助您轻松识别应用程序性能瓶颈。您可以将Weave Scope作为独立应用部署在本地服务器/笔记本电脑上，也可以在Weave Cloud上选择Weave Scope Software as a Service (SaaS)解决方案。使用Weave Scope，您可以使用名称、标签和/或资源消耗轻松地对容器进行分组、筛选或搜索。

- [prometheus](https://github.com/prometheus/prometheus)---prometheus是云本地计算基金会的一个项目，是一个系统和服务监控系统。它以给定的时间间隔从配置的目标收集指标，计算规则表达式，显示结果，并在观察到指定的条件时触发警报。

- [Searchlight](https://github.com/appscode/searchlight)---Searchlight by AppsCode是Kubernetes的Icinga运营商。Searchlight定期对Kubernetes集群进行各种检查，如果出现问题，会通过电子邮件、短信或聊天提醒你。Searchlight包括一套默认的支票，专门为Kubernetes写的。此外，它还可以通过外部黑箱监视增强Prometheus监视，并在内部系统完全失败时充当后备。

- [cAdvisor](https://github.com/google/cadvisor)---CAdvisor默认安装在所有集群节点上，用于收集Kubernetes关于运行容器和节点的指标。CAdvisor Kubelet通过Kubelet api公开这些指标(默认分辨率为1分钟)。Metrics Server识别所有可用节点，并在通过Kubernetes聚合API公开指标之前调用Kubelet API来获取容器和节点资源的使用情况。

- [Kube-state-metrics](https://github.com/kubernetes/kube-state-metrics)---kube-state-metrics从Kubernetes API对象生成度量，而不需要通过侦听Kubernetes API服务器进行修改。它不太关注单个Kubernetes组件的健康状况，而是关注内部各种对象(如部署、节点和荚)的健康状况。

- [Sumo Logic App](https://www.sumologic.com/application/kubernetes/)---Sumo Logic Kubernetes应用程序提供了对集群中的工作节点及其应用程序日志的完整可见性。该应用程序允许用户监视容器运行状况、复制、负载平衡、pod状态和硬件资源分配并排除故障。应用程序利用Falco事件来监视和检测异常的容器、应用程序、主机和网络活动。

- [Dynatrace](https://www.dynatrace.com/)---Dynatrace OneAgent是容器感知的，并内置了对Kubernetes开箱即用监控的支持。Dynatrace为Kubernetes提供全栈监控，即从应用程序到基础设施层的监控。但是，如果您不能访问基础设施层，Dynatrace还提供了只监视应用程序的选项。

### 测试


- [Kube-monkey]( https://github.com/asobti/kube-monkey)---Kube-monkey是Kubernetes的翻版。Kube-monkey是一种遵循混沌工程原理的工具。它可以随机删除k8豆荚，检查服务具有故障恢复能力，并有助于您的系统的健康。Kube-monkey还通过一个TOML文件进行配置，您可以在该文件中指定要终止哪个应用程序，以及何时实践您的恢复策略。

- [K8s-testsuite](https://github.com/mrahbar/k8s-testsuite)---K8s-testsuite由2个Helm图表组成，用于单个Kubernetes集群的网络带宽测试和负载测试。负载测试用loadbots模拟简单的web服务器，loadbots作为Kubernetes基于Vegeta的微服务运行。网络测试在内部使用iperf3和netperf-2.7.0，并运行三次。这两组测试都生成包含所有结果和指标的全面日志消息。

- [Test-infra](https://github.com/kubernetes/test-infra)---Test-infra是Kubernetes测试和结果验证工具的集合。Test-infra包括一些仪表板，用于显示历史记录、聚合失败和显示当前正在测试的内容。您可以通过创建自己的测试作业来增强测试基础设施套件。Test-infra可以使用Kubetest工具在不同的提供商上使用完整的Kubernetes生命周期模拟执行端到端Kubernetes测试。

- [Sonobuoy](https://sonobuoy.io/)---Sonobuoy允许您以可访问和非破坏性的方式运行一组测试，以了解当前Kubernetes集群状态。Sonobuoy生成包含集群性能详细信息的翔实报告。Sonobuoy支持3个Kubernetes小版本:当前版本和之前的2个小版本。Sonobuoy Scanner是一个基于浏览器的工具，允许您在几次单击中测试Kubernetes集群，但CLI版本有更大的测试集可用。

- [PowerfulSeal](https://github.com/bloomberg/powerfulseal)---PowerfulSeal是一个类似于Kube-monkey的工具，遵循混沌工程的原则。PowerfulSeal可以杀死pod，并从集群中移除/添加vm。与Kube-monkey相比，powerfulseal有一个交互模式，允许您手动破坏特定的集群组件。此外，除了SSH, powerfulseal不需要外部依赖。

### 安全

- [Trireme](https://github.com/aporeto-inc/trireme-kubernetes)---Trireme是Kubernetes网络策略的一个灵活而直接的实现。Trireme可以在任何Kubernetes集群中工作，并允许您管理来自不同集群的pod之间的流量。Trireme的主要优点是不需要任何集中的策略管理，能够轻松地组织部署在Kubernetes中的两种资源的交互，并且不需要复杂的SDN、VLAN标签和子网(Trireme使用传统的l3网络)。

- [Aporeto](https://www.aporeto.com/)---Aporeto基于工作负载标识、加密和分布式策略为容器、微服务、云和遗留应用程序提供安全性。由于Aporeto策略独立于底层基础设施运行，因此可以跨Kubernetes集群或在包括Kubernetes和非Kubernetes部署的混合环境中启用安全策略。

- [Twistlock](https://www.twistlock.com/)---Twistlock持续监视部署在k8上的应用程序的漏洞和遵从性问题，包括底层主机、容器和映像。此外，Twistlock Runtime Defense自动建模容器行为，允许已知的良好行为，同时警告或阻止异常活动。最后，Twistlock提供了第3层微分割和第7层防火墙，可以保护前端微服务免受常见攻击。

- [Falco](https://sysdig.com/opensource/falco/)---Falco是一个行为活动监视器，旨在检测您的应用程序中的异常活动。Falco基于Sysdig Project，这是一个开源工具(现在是一个商业服务)，通过跟踪内核系统调用来监视容器性能。Falco允许您使用一组规则连续监视和检测容器、应用程序、主机和网络活动。

- [Sysdig Secure](https://sysdig.com/product/secure/)---sysddig Secure是sysddig容器智能平台的一部分，具有无与伦比的容器可视性和与容器编排工具的深度集成。其中包括Kubernetes、Docker、AWS ECS和Apache Mesos。使用Sysdig Secure，您可以实现服务感知策略，阻止攻击，分析历史，并监控集群性能。sysddig Secure可以作为云和内部软件提供。

- [Kubesec.io](https://kubesec.io)---Kubesec。io是一个服务，允许您为安全特性使用的Kubernetes资源评分。Kubesec。io根据Kubernetes安全最佳实践验证资源配置。因此，对于如何提高整个系统的安全性，您将拥有完全的控制和额外的建议。该网站还包含大量与集装箱和Kubernetes安全相关的外部链接。

### 有用的CLI工具

- [Cabin](https://github.com/bitnami-labs/cabin)---Cabin可以作为Kubernetes集群远程管理的移动仪表板。有了Cabin，用户可以从他们的Android或iOS设备上快速管理应用程序、扩展部署，并对整个k8集群进行故障排除。对于k8集群的运营商来说，机舱是一个很好的工具，因为它允许您在发生事故时执行快速补救行动。

- [Kubectx/Kubens](https://github.com/ahmetb/kubectx)---Kubectx是一个小型的开源实用工具，它增强了Kubectl的功能，可以轻松切换上下文，同时连接到几个Kubernetes集群。Kubens允许在Kubernetes名称空间之间导航。这两种工具在bash/zsh/fish shell上都有一个自动完成功能。

- [Kube-shell](https://github.com/cloudnativelabs/kube-shell)---Kube-shell在使用kubectl时提高了生产力。Kube-shell支持命令自动完成和自动建议。此外，Kube-shell将提供关于已执行命令的内联文档。Kube-shell甚至可以搜索和纠正错误输入的命令。它是在k8控制台中提高性能和生产率的一个很好的工具。

- [Kail](https://github.com/boz/kail)---Kail是Kubernetes tail的缩写，为Kubernetes集群工作。使用Kail，你可以跟踪所有匹配的吊舱的Docker日志。Kail允许您根据服务、部署、标签和其他特性过滤豆荚。如果pod符合条件，那么它将在启动后自动添加(或删除)到日志中。

### Development Tools

- [Telepresence](https://www.telepresence.io/)---Telepresence 提供了从Kubernetes环境到本地进程的代理数据在本地调试Kubernetes集群的可能性。网真能够为您的本地代码提供Kubernetes服务和AWS/GCP资源的访问，因为它将被部署到集群中。使用Telepresence，Kubernetes将本地代码视为集群中的一个普通pod。

- [Helm](https://helm.sh/zh/)---Helm 帮助您管理 Kubernetes 应用——Helm 图表，即使是最复杂的 Kubernetes 应用程序，都可以帮助您定义，安装和升级。

- [Jaeger](https://www.jaegertracing.io/ )---Jaeger Operator是Kubernetes Operator的实现，提供了封装、部署和管理Kubernetes应用程序的另一种方法。

- [turbonomic](https://turbonomic.com/product/integrations/kubernetes/)---turbonomic的Kubernetes -as-a- Service (KaaS)管理功能包括支持Amazon弹性容器服务(EKS)、微软Azure Kubernetes服务(AKS)、谷歌Kubernetes引擎(GKE)和关键容器服务(PKS)。自管理Kubernetes优化了性能、效率和遵从性，因此IT组织可以扩展和加速云原生计划。

- [Supergiant](https://supergiant.io/toolkit/)---Supergiant是一个开源的实用程序集合，可以简化Kubernetes集群的安装和管理。Supergiant Kubernetes工具箱是三个独立的应用程序:Control、Analyze和Capacity。从本质上讲，Supergiant是一个微服务应用程序，允许分别使用这三种工具。

- [Keel](https://keel.sh/)---Keel允许您自动化Kubernetes部署更新，并可以在专用的名称空间中作为Kubernetes服务启动。通过这样的组织，Keel为您的环境引入了最小的负载，并增加了显著的健壮性。Keel通过标签、注释和图表帮助部署Kubernetes服务。您只需要为每个部署或Helm版本指定一个更新策略。只要存储库中有新的应用程序版本，Keel就会自动更新您的环境。

- [Apollo](https://github.com/logzio/apollo)---Apollo是一个开源应用程序，为团队提供了自助用户界面，用于创建和部署他们的服务到Kubernetes。Apollo允许操作人员查看日志，只需点击一下鼠标就可以将部署恢复到任何时间点。阿波罗具有灵活的部署权限模型。每个用户只能部署他需要部署的内容。

- [Draft](https://github.com/azure/draft)---Draft是Azure团队提供的一个工具，可以简化应用程序开发和部署到任何Kubernetes集群中。Draft在代码部署和代码提交之间创建了“内部循环”，显著加快了更改验证过程。使用Draft，开发人员可以用两个命令准备应用程序Dockerfiles和Helm图表，并将应用程序部署到远程或本地Kubernetes集群。

- [Deis Workflow](https://deis.com/workflow/)---Deis Workflow是一个开源工具。平台即服务(PaaS)在Kubernetes集群之上创建了额外的抽象层。这些层允许您部署和/或更新Kubernetes应用程序，而无需开发人员提供特定领域的知识。工作流建立在Kubernetes概念之上，提供简单的、开发人员友好的应用程序部署。Kubernetes提供了一套微服务，运营商可以轻松安装该平台。Workflow可以在零停机时间下部署应用的新版本。

- [Kel](http://www.kelproject.com/)---Kel是Eldarion公司的一个开源PaaS，帮助管理Kubernetes应用程序的整个生命周期。Kel在Kubernetes之上提供了另外两个用Python和Go编写的层。级别0允许您提供Kubernetes资源，级别1帮助您在k8上部署任何应用程序。

- [Kong](https://konghq.com/)---Kong，原名Kong Community (CE)，是由Kong Inc发起的一项可扩展的开源API网关技术，拥有一个不断发展的社区。Kong允许开发者使用Kubernetes管理认证、数据加密、日志记录、速率限制和其他标准功能，这些功能都是他们期望从基本API管理系统中获得的。所有这些都是由一个简单的RESTful API提供的，平台本身构建在NGINX代理服务器和Apache Cassandra数据库管理系统之上。

### 持续集成/持续交付管道

- [Cloud 66](https://www.cloud66.com/)---Cloud 66为生产中的容器化应用提供了完整的DevOps工具链，通过专门的运维工具，为开发人员自动化了许多繁重的工作。该平台目前在Kubernetes上运行4000个客户工作负载，并管理2500行配置。通过提供端到端基础设施管理，Cloud 66使工程师能够在任何云或服务器上构建、交付、部署和管理任何应用程序。

### Serverless /函数工具

- [Kubeless](https://github.com/kubeless/kubeless)---Kubeless是kubernetes本地的无服务器框架，它允许您部署少量代码，而不必担心底层基础设施。Kubeless了解Kubernetes的开箱即用资源，并提供自动伸缩、API路由、监控和故障排除。Kubeless完全依赖于k8的原语，因此Kubernetes用户也能够使用本地k8的API服务器和API网关。

- [Fission](https://fission.io/)---Fission是Kubernetes的一个快速无服务器框架，专注于开发人员的生产力和高性能。Fission可以在任何地方的Kubernetes集群上工作:在您的笔记本电脑上，在任何公共云中，或者在私有数据中心中。您可以使用Python、NodeJS、Go、c#或PHP编写函数，并使用Fission将其部署到k8集群上。

- [Funktion](https://github.com/funktionio/funktion)---Funktion是一个为Kubernetes设计的开源事件驱动的lambda风格编程模型。Funktion与fabric8平台紧密结合。使用Funktion，您可以创建从200多个事件源订阅的流来调用函数，包括大多数数据库、消息传递系统、社交媒体和其他中间件和协议。

- [IronFunction](https://github.com/iron-io/functions)---IronFunctions是一个开源的无服务器平台或FaaS平台，你可以在任何地方运行。IronFunction是在Golang上编写的，真的支持任何语言的函数。IronFunction的主要优点是它支持AWS Lambda格式。直接从Lambda导入函数，并在任何你想要的地方运行它们。

- [OpenWhisk](https://console.bluemix.net/openwhisk/)---Apache OpenWhisk是一个由IBM和Adobe驱动的健壮的开源FaaS平台。OpenWhisk可以部署在本地设备上，也可以部署在云上。Apache OpenWhisk的设计意味着它充当一个异步和松耦合的执行环境，可以针对外部触发器运行函数。OpenWhisk作为Bluemix上的SaaS解决方案可用，或者您可以在本地部署一个基于vagrant的VM。

- [OpenFaaS](https://github.com/openfaas/faas)---OpenFaaS框架旨在管理Docker Swarm或Kubernetes上的无服务器功能，在这些功能中，它将收集和分析广泛的指标。您可以将任何进程打包到函数中并使用它，而无需重复编码或任何其他例程操作。FaaS具有普罗米修斯标准，这意味着它可以根据需求自动缩放功能。FaaS本地支持基于web的界面，您可以在其中尝试您的功能。

- [Nuclio](https://github.com/nuclio/nuclio)---Nuclio是一个旨在处理高性能事件和大量数据的无服务器项目。Nuclio可以作为独立库在内部设备上启动，也可以在VM/Docker容器中启动。此外，Nuclio支持Kubernetes的盒子。Nuclio以最大的并行度和最小的开销提供实时数据处理。

- [Virtual-Kubelet](https://virtual-kubelet.io/)---Virtual Kubelet是一个开源的Kubernetes Kubelet实现，它将Kubernetes伪装成Kubelet，以便将Kubernetes连接到其他api。Virtual Kubelet允许节点由其他服务支持，如ACI、Hyper.sh和AWS等。该连接器具有可插拔的体系结构和直接使用Kubernetes原语的特点，使构建更加容易。

### 服务网格工具

- [istio/istio](https://github.com/istio/istio)---Istio是一个开放平台，提供统一的方式来集成微服务、管理微服务之间的流量、执行策略和聚合遥测数据。Istio的控制平面在底层集群管理平台(如Kubernetes)上提供了一个抽象层。

- [linkerd/linkerd2](https://github.com/linkerd/linkerd2)---Linkerd是Kubernetes的一款超轻、安全优先的服务网。Linkerd为您的Kubernetes堆栈添加了关键的安全性、可观察性和可靠性特性，而不需要更改代码。

- [Hashicorp's Consul](https://www.hashicorp.com/products/consul/)---Consul是一种服务网络解决方案，可跨任何运行时平台和公共或私有云连接和保护服务。和上面的服务网格技术一样，Istio和Linkerd, HashiCorp的Consul Connect选择了一个部署为sidecar的代理。代理透明地保护微服务之间的通信，并通过一个称为意图的概念实现策略定义。

### 本地服务发现

- [Kubernetes Dashboard](https://github.com/kubernetes/dashboard#kubernetes-dashboard)---Kubernetes Dashboard是一个通用的、基于web的Kubernetes集群UI。使用本机仪表板更容易对k8集群进行故障排除和监视。您需要在计算机和Kubernetes API服务器之间创建一个安全的代理通道来访问仪表板。原生Kubernetes仪表板依赖于Heapster数据收集器，因此它也需要安装在系统中。

### 成本管理

- [Replex](https://www.replex.io/)---Replex是为在Kubernetes环境中工作而设计的同名治理和成本管理平台。该工具通过统一云中部署的成本和治理管理，解决了围绕Kubernetes的动态特性的挑战。

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


## 🧾学术论文


## 📂文档库(提取码：1024)
- [白皮书:Kubernetes如何拯救OpenStack](https://github.com/0voice/k8s_awesome_document/blob/main/%E6%96%87%E6%A1%A3/%E7%99%BD%E7%9A%AE%E4%B9%A6%EF%BC%9AKubernetes%E5%A6%82%E4%BD%95%E6%8B%AF%E6%95%91OpenStack.pdf)
- [2021年云原生行业研究报告](https://github.com/0voice/k8s_awesome_document/blob/main/%E6%96%87%E6%A1%A3/2021%E5%B9%B4%E4%BA%91%E5%8E%9F%E7%94%9F%E8%A1%8C%E4%B8%9A%E7%A0%94%E7%A9%B6%E6%8A%A5%E5%91%8A.pdf)
- [石墨文档Go在K8S上微服务的实践-彭友顺](https://pan.baidu.com/s/1uRCajVK2qPqvtLlBwPnKYw)
- [K8s 为 AI 应用提供大规模 GPU 算力之实践-李程](https://pan.baidu.com/s/1VqdLvfdm0YJz7wvLSKoTOg)
- [kubernetes在深度学习场景下的优化以及使用-薛磊](https://pan.baidu.com/s/1UQbaOwMcGBcHTytbaEL10g)
- [K8S在华为云的实践与发展-王泽锋](https://pan.baidu.com/s/1ErXlkSIB-bZhV9ce1MM14g)
- [基于Istio+on+Kubernetes云原生应用的最佳实践-王夕宁](https://pan.baidu.com/s/1_FHirCEUWfCo42z5jTQCUQ)
