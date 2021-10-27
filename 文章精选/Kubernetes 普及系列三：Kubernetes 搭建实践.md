现在，我们尝试在 Ubuntu 18 LTS 搭建 Kubernetes，将会进行如下的步骤：

1、安装 Docker
2、安装 Kubeadm
3、初始化 Kubernetes 集群

## 安装 Docker

用脚本更方便安装：

```
$ curl -fsSL https://get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh
```

创建 `/etc/docker/daemon.json`，配置一些基础内容，主要包括 Mirrors 以及配置 Systemd（Kubeadm会需要）。

```
{
  "registry-mirrors": [
    "https://docker.mirrors.ustc.edu.cn",
    "https://mirror.ccs.tencentyun.com"
  ],
  "exec-opts": [
    "native.cgroupdriver=systemd"
  ],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
```

现在执行 Docker version 确认安装成功。

## 安装 Kubeadm

首先安装基础依赖：

```
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
```

安装 Gpg 证书：

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

如果遇到无法下载的情况，就先 Wget 下来再安装进去：

```
wget https://packages.cloud.google.com/apt/doc/apt-key.gpg
sudo apt-key add apt-key.gpg
```

设置国内源：

```
cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb http://mirrors.ustc.edu.cn/kubernetes/apt kubernetes-xenial main
EOF
sudo apt-get update
```

安装：

```
sudo apt-get install -y kubelet kubeadm kubectl
```

安装结束后，Kubeadm version 确认安装成功。

## 初始化 Kubernetes 集群

一般来说，为了安装好 Kubernetes 集群，我们会进行两个步骤：

1、Kubeadm init

2、安装网络插件

### Kubeadm init

首先，我们需要执行 Kubeadm init 来启动本地 Kubernetes 集群。**建议生成 Kubeadm 的启动配置文件。**

```
kubeadm config print init-defaults > kubeadm.yaml
```

然后编辑 Kubeadm.yaml 调整配置（如果有需要）。现在让我们在 Root 账号执行 `kubeadm init --config kubeadm.yaml`，这时会执行一些前置检查，如果检查不通过，按照提示修复即可（比如需要禁用 Swap）。如果成功，会看到类似如下的输出：

```
[init] Using Kubernetes version: vX.Y.Z
[preflight] Running pre-flight checks
[preflight] Pulling images required for setting up a Kubernetes cluster
[preflight] This might take a minute or two, depending on the speed of your internet connection
[preflight] You can also perform this action in beforehand using 'kubeadm config images pull'
[kubelet-start] Writing kubelet environment file with flags to file "/var/lib/kubelet/kubeadm-flags.env"
[kubelet-start] Writing kubelet configuration to file "/var/lib/kubelet/config.yaml"
[kubelet-start] Activating the kubelet service
[certs] Using certificateDir folder "/etc/kubernetes/pki"
[certs] Generating "etcd/ca" certificate and key
[certs] Generating "etcd/server" certificate and key
[certs] etcd/server serving cert is signed for DNS names [kubeadm-cp localhost] and IPs [10.138.0.4 127.0.0.1 ::1]
[certs] Generating "etcd/healthcheck-client" certificate and key
[certs] Generating "etcd/peer" certificate and key
[certs] etcd/peer serving cert is signed for DNS names [kubeadm-cp localhost] and IPs [10.138.0.4 127.0.0.1 ::1]
[certs] Generating "apiserver-etcd-client" certificate and key
[certs] Generating "ca" certificate and key
[certs] Generating "apiserver" certificate and key
[certs] apiserver serving cert is signed for DNS names [kubeadm-cp kubernetes kubernetes.default kubernetes.default.svc kubernetes.default.svc.cluster.local] and IPs [10.96.0.1 10.138.0.4]
[certs] Generating "apiserver-kubelet-client" certificate and key
[certs] Generating "front-proxy-ca" certificate and key
[certs] Generating "front-proxy-client" certificate and key
[certs] Generating "sa" key and public key
[kubeconfig] Using kubeconfig folder "/etc/kubernetes"
[kubeconfig] Writing "admin.conf" kubeconfig file
[kubeconfig] Writing "kubelet.conf" kubeconfig file
[kubeconfig] Writing "controller-manager.conf" kubeconfig file
[kubeconfig] Writing "scheduler.conf" kubeconfig file
[control-plane] Using manifest folder "/etc/kubernetes/manifests"
[control-plane] Creating static Pod manifest for "kube-apiserver"
[control-plane] Creating static Pod manifest for "kube-controller-manager"
[control-plane] Creating static Pod manifest for "kube-scheduler"
[etcd] Creating static Pod manifest for local etcd in "/etc/kubernetes/manifests"
[wait-control-plane] Waiting for the kubelet to boot up the control plane as static Pods from directory "/etc/kubernetes/manifests". This can take up to 4m0s
[apiclient] All control plane components are healthy after 31.501735 seconds
[uploadconfig] storing the configuration used in ConfigMap "kubeadm-config" in the "kube-system" Namespace
[kubelet] Creating a ConfigMap "kubelet-config-X.Y" in namespace kube-system with the configuration for the kubelets in the cluster
[patchnode] Uploading the CRI Socket information "/var/run/dockershim.sock" to the Node API object "kubeadm-cp" as an annotation
[mark-control-plane] Marking the node kubeadm-cp as control-plane by adding the label "node-role.kubernetes.io/master=''"
[mark-control-plane] Marking the node kubeadm-cp as control-plane by adding the taints [node-role.kubernetes.io/master:NoSchedule]
[bootstrap-token] Using token: <token>
[bootstrap-token] Configuring bootstrap tokens, cluster-info ConfigMap, RBAC Roles
[bootstraptoken] configured RBAC rules to allow Node Bootstrap tokens to post CSRs in order for nodes to get long term certificate credentials
[bootstraptoken] configured RBAC rules to allow the csrapprover controller automatically approve CSRs from a Node Bootstrap Token
[bootstraptoken] configured RBAC rules to allow certificate rotation for all node client certificates in the cluster
[bootstraptoken] creating the "cluster-info" ConfigMap in the "kube-public" namespace
[addons] Applied essential addon: CoreDNS
[addons] Applied essential addon: kube-proxy

Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a Pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  /docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

现在我们切换到用户账号执行上面提示的命令：

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

找个地方记录下最后这行（如果单节点的话用不上）：

```
kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
```

检查运行状态：

```
kubectl get pods -n kube-system
```

此时 Coredns 的 2 个 Pod 都在 Pending，因为缺少 Cni 网络插件，我们在后面选择安装 calico 作为网络插件。如果我们打算单节点运行，需要设置 Master 节点：

1、允许 Pod 调度到 Master 节点：

```
kubectl taint nodes --all node-role.kubernetes.io/master-
```

2、允许 Load balance 将流量 Route 到 Master 节点：

```
kubectl label nodes --all node-role.kubernetes.io/master-
```

### 安装网络插件

我们选用较为常见的 Calico 作为网络插件，直接执行：

```
kubectl apply -f https://docs.projectcalico.org/v3.14/manifests/calico.yaml
```

成功后继续检查运行状态 `kubectl get pods -n kube-system`，等到 Coredns 的 2 个 Pod 都从 Pending 变成 Running，就全部大功告成了。

## 清理集群

如果遇到什么问题，需要重置集群，我们可以使用命令 `kubeadm reest`重置集群，再重新 `kubeadm init` 即可。
