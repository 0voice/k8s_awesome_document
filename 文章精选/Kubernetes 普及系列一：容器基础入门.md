随着云原生时代的来临，云以及分布式计算已经是时下最受欢迎的技术之一了。其中 Docker 作为最知名的容器平台，到底有着怎样的魅力来让其无人不知无人不晓？废话不多说，让我们开始逐层掀开容器技术的神秘面纱吧！

## Docker

![从传统 IT 到 IaaS 到 PaaS 的能力变迁](https://help-assets.codehub.cn/enterprise/%E5%9B%BE%E7%89%871.png)

**让时间回到 2013 年**，在该时候，虚拟机和云服务已经很流行了。主流用户的常见做法，就是在云平台（比如腾讯云、AWS、OpenStack 等），像管理物理服务器一样用脚本来做管理和部署应用。

这样的做法一直存在本地环境和线上环境不一致导致部署出现问题的风险，所以各家云平台的思路都是去模拟出更加接近本地服务器的环境，来给用户提供更好的上云体验。所以开源的 PaaS 项目提供“应用托管”的能力，就是解决该问题的一个最佳方案。

在众多开源 PaaS 项目中，最热门的 Cloud Foundry 基本上已经吸引了所有云厂商的目光，开启了以开源 PaaS 为核心构建平台层服务能力的变革。

大家可能并不是很熟悉 Cloud Foundry，简单的说，Cloud Foundry 所做的就是提供一个 “cf push” 命令行工具，让大家能够对一些主流语言的代码进行打包上传和分发。然后 Cloud Foundry 通过调用操作系统的 CGroups 和 Linux Namespace，单独为每一个应用创建一个隔离的沙盒环境，然后在其中启动这些应用的进程。

![Cloud Foundry 的最核心命令 cf push 的业务流程图](https://help-assets.codehub.cn/enterprise/%E5%9B%BE%E7%89%872.png)

所以当时 Cloud Foundry 最核心的能力，就是提供隔离的运行环境，也就是“容器”了。

![当时的 PaaS 风潮参与者，dotCloud 是最不起眼的公司之一](https://help-assets.codehub.cn/enterprise/%E5%9B%BE%E7%89%873.png)

**同期，有一家名叫 dotCloud 的公司，因为它的主打产品跟 Cloud Foundry 社区是脱节的，所以长期以来都无人问津。终于，dotCloud 公司决定开源自己的容器项目 Docker。**

但很可惜在当时并没有人关注 dotCloud 的该决定，因为“容器”该概念从来就不是什么新鲜的东西，也不是 Docker 公司发明的。哪怕是在当时最热门的 PaaS 项目 Cloud Foundry 里，容器也只是其最底层，最没人关注的那一部分。

而 Docker 项目，实际上和 Cloud Foundry 的容器并没有太大的不同，所以在 Docker 发布后不久，Cloud Foundry 的首席产品经理 James Bayer 就在社区里做了一次详细对比，告诉用户 Docker 实际上只是一个同样使用 Cgroups 和 Namespace 实现的“沙盒”而已，没有什么特别的黑科技，也不需要特别关注。

然而，几个月后，James Bayer 就被打脸了。Docker 只用了短短几个月，就让所有 PaaS 社区都出局了。事实上，Docker 项目确实和 Cloud Foundry 的容器在大部分功能和实现原理上并没有什么区别，但仅有的一个不一样的功能，成了 Docker 项目的制胜关键。

**该功能就是 Docker 镜像。**

当时主流的 PaaS 项目，如 Cloud Foundry，都通过提供一套应用打包功能，帮助用户大规模部署到集群。但就是该打包功能，需要用户为每个应用做大量的配置工作和调试工作，才能让本地能供正确运行的应用，在集群里也能正确运行。

而 Docker 镜像，恰好解决了该根本性的问题。Docker 镜像的本质，就是一个压缩包，但和 PaaS 的应用打包相比，该压缩包里则是多了完整的运行环境依赖内容，比如操作系统的所有文件和目录。只要用户拿着该压缩包，便可以通过某些技术手段在任何地方创建一个沙盒来运行用户的应用了，因为其做到了本地环境和云端环境高度的一致，再加上 Docker 充满趣味性的推广，比如 “1 分钟部署一个 WordPress 网站”、“3 分钟部署一个 Nginx 集群”等，最终通过与开发者的亲密关系，加上解决了打包的根本性难题，从而一举登天。

## Linux Namespace，Linux **Cgroups** ，rootfs

我们前面已经介绍了 Docker 的发展，那么，回归到技术本身，容器到底是什么呢？这里可以先下一个定义：

**一个“容器”，实际上是一个由 Linux Namespace、Linux Cgroups 和 rootfs 三种技术构建出来的进程的隔离环境。**

- **Linux Namespace** 和 **Linux Cgroups**，提供了运行时的隔离和资源的授予。
- **rootfs**，也就是镜像，提供了容器的运行内容。

比如对于如下 Dockerfile：

```
# 使用官方提供的 Python 开发镜像作为基础镜像
FROM python:3.8-slim-buster

# 将工作目录切换为 /app
WORKDIR /app

# 拷贝应用依赖描述文件到工作目录
COPY requirements.txt requirements.txt

# 使用 pip 命令安装应用以及其所需的依赖
RUN pip3 install -r requirements.txt

# 拷贝应用文件到工作目录
COPY . .

# 设置容器进程为 "python3 app.py"，也是该 Python 应用的启动命令
CMD [ "python3", "app.py"]
```

在该 Dockerfile 里，我们先通过一个基础镜像 python:3.8-slim-buster，安装依赖并复制应用到工作目录，最后指定应用的进程，即启动命令。在该描述下，我们会得到如下容器视图：

[![img](https://help-assets.codehub.cn/enterprise/%E5%9B%BE%E7%89%874.png)](https://help-assets.codehub.cn/enterprise/图片4.png)

该容器的进程是”python3 app.py“，运行在由 Linux namespace + Linux cgroups 构成的隔离环境里。而它所需要的各种文件，包括 Python、app.py 和整个操作系统文件，则由多个联合挂载在一起的 rootfs 提供。该 rootfs 的最下层，是只读的 Docker 镜像。在 Docker 镜像之上，是 Docker 的管理器添加的 init 层，用于临时存放被管理器修改过的 /etc/hosts 等文件。在 rootfs 的最上层是读写层，以 Copy-On-Write 的方式存放所有对只读层文件的修改，和容器声明的 Volume 挂载点。从该容器视图里，我们可以总结出一个运行中的 Linux 容器，由以下内容构成：

- 一组联合挂载的 rootfs，这部分我们称之为容器的”镜像“（Image）。
- 一个由 Linux namespace + Linux cgouprs 构成的隔离环境，这部分我们称之为容器的”运行时“（Runtime）。

## Docker install

前文已经介绍了容器的本质和其背后的逻辑，我们现在以 `Ubuntu 18 LTS` 为例，介绍如何安装 Docker，为后面的 Kubernetes 做好准备。

### 配置 REPOSITORY

1、更新 `apt` 包管理器索引和配置 `apt` 能够使用 HTTPS 的仓库。

```
sudo apt-get update

sudo apt-get install \
   apt-transport-https \
   ca-certificates \
   curl \
   gnupg \
   lsb-release
```

2、添加 Docker 官方 GPG 公钥。

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

3、指定使用稳定版的 Docker 版本。

```
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### 安装 Docker engine

1、更新 `apt`包管理器索引，然后安装最新的稳定版 Docker engine。

```
sudo apt-get update

sudo apt-get install docker-ce docker-ce-cli containerd.io
```

2、安装完成后，通过执行 `hello-world`镜像，验证 Docker engine。

```
sudo docker run hello-world
```

**现在安装完成，可以开始使用 Docker 了。**

## 容器编排

作为一名开发者，我们其实并不关心容器运行时的差异，因为在整个“开发-发布”流程中，真正发布的其实是容器镜像。对于云服务商来说，则可以通过容器镜像将他们和潜在用户（如开发者）直接关联起来。因此，能够定义容器组织和管理规范的“容器编排”技术，成为了云计算最热门的技术。**这其中，最具代表性的容器编排工具有如下两个：**

• Docker 公司的 Compose+Swarm 组合；

• Google 与 RedHat 公司共同主导的 Kubernetes 项目。而目前该项目已经成为业界标准。

接下来的 Kubernetes 普及系列，将会带大家深入了解目前承载着云原生发展的绝对主角——Kubernetes，究竟有着怎样的魔力，那么让我们下回再见！
