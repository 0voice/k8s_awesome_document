在前面的 Kubernetes 普及系列中，相信大家已经对 Kubernetes 有一个大概的认识。在这篇文章中，我们将进入到 Kubernetes 的第一个细节中进行学习。

大家都知道，Kubernetes 是一个容器编排和调度的系统, 但是 Kubernetes 调度资源的原子单位并不是容器，而是一个叫 Pod 的东西，Pod 在英文里是豌豆的意思：

![img](https://help-assets.codehub.cn/enterprise/20210604151733.png)

这个豌豆的比喻非常的恰当，Pod 是指 1 个或多个容器组合而成的对象。

那么为什么一个容器编排系统调度的单位是 Pod 而不是 container 呢，这就要容器的本质了。

容器的本质就是一个进程，Kubernetes 就是而管理这些进程的操作系统。当我们在系统上使用 `pstree -g` 时，会发现进程并不是孤零零的存在，而是成组的一起出现

![img](https://help-assets.codehub.cn/enterprise/20210604151843.png)

稍微复杂的任务，真实世界的程序都比较喜欢用多个进程组合在一起的方式来解决问题。而 Pod 其实就是代表着一个进程组。进程组之间往往有共享磁盘，管道等通讯，如果 Kubernetes 不是把进程组一起调度而是把他们拆开，死板地按进程调度，将会让这些程序的进程可能分布在不同的主机上，导致程序不可用。你也可以把 Pod 类比成虚拟机。想象一下你在虚拟机下有一个 Java 应用，虚拟机里面装了 tomcat，Java war 包，日志搜集程序，如果没有 Pod，如果这些都是用一个个容器去替换，是很难把这个应用搬到 K8s 上的。

另外要注意的是，我们说容器本质是一个进程，并不是说容器不能运行两个进程，只不过能运行不等于能管理，如果你在 dockerfile 里面一次启动两个进程，当容器被杀掉后，第二个进程就不会被系统管到，直接就泄漏了。

接下来我们来看看 Pod 到底长什么样子。还是使用前面我们的示例集群，使用命令 `kubectl get Pods`，

![img](https://help-assets.codehub.cn/enterprise/20210604151858.png)

我们看到有 2 个之前部署的和 nginx 有关的 Pod 对象，取其中一个看看，运行 `kubectl get Pods nginx-deployment-66b6c48dd5-qw9lp -o yaml`，终端中将会输出一堆 yaml:

```
apiVersion: v1
kind: Pod
metadata:
  annotations:
    ....
  labels:
    app: nginx
  name: nginx-deployment-66b6c48dd5-qw9lp
  namespace: jimmy
spec:
  containers:
   - image: nginx:1.14.2
     imagePullPolicy: IfNotPresent
     		name: nginx
     		ports:
        - containerPort: 80
          			protocol: TCP
```

上面代码中，我省略了一些信息，你现在还不用关注这些细节。这个 yaml 的内容，就是一个 Pod 对象，里面包含这个 Pod 在 Kubernetes 集群里运行的绝大部分信息。

### 重要属性

#### Metadata

Metadata 是一个对象的元数据，里面包含的基本是这个 Pod 的标识，例如 name 也就是这个 Pod 的名字, namespace 也就是这个 Pod 所在的命名空间，uid 是这个 Pod 在集群里的唯一 id，creationTimestamp 表示这个 Pod 的创建时间。这些字段大多数都是 immutable 的，也就是一旦这个 Pod 创建，就不能再修改这些字段了。

#### Spec

Spec 是这个 Pod 里面具体的规格，包括容器的配置，volume 的配置等。

#### Annotations

Annotations 与 metadata 都属于一个对象的额外信息，但是 metadata 通常是非常重要的信息, 而 arhaenotation 通常来说都是相对没那么重要的信息，很多持续部署系统，云管平台之类的会利用 annotation 属性去做信息的维护。

#### 镜像，端口

Kubernetes 中，Pod 最重要的属性肯定是镜像和端口了，而他们的作用也很明显了，就不展开了

#### ImagePullPolicy

在这个属性决定你对 Kubernetes 发起一个 apply 操作时，镜像拉取的策略，ImagePullPolicy 的值默认是 Always，即每次创建 Pod 都重新拉取一次镜像。另外，当容器的镜像是类似于 nginx 或者 nginx:latest 这样的名字时，ImagePullPolicy 也会被认为 Always，而如果它的值被定义为 Never 或者 IfNotPresent，则意味着 Pod 永远不会主动拉取这个镜像，或者只在宿主机上不存在这个镜像时才拉取。

#### Volume

这个和 docker 的 volume 很相似，只不过他能挂的类型非常多的，从 git 到空目录，到 S3 储存，都不满足的话还可以自己扩展。volume 的定义类似这样：

```
apiVersion: v1
kind: Pod
metadata:
  name: configmap-pod
spec:
  containers:
    - name: test
      image: busybox
      volumeMounts:
        - name: config-vol
          mountPath: /etc/config
  volumes:
    - name: config-vol
      configMap:
        name: log-config
        items:
          - key: log_level
            path: log_level
```

上面例子中，我们声明了一个 volume， 名字叫 config-vol，他的内容引用了一个 Kubernetes 中专门用于保存配置的 configmap 对象。然后在名字叫 test 的容器的 volumeMounts 属性里面，把这个 volume 挂载到了 /etc/config 目录下。

## Pod 的生命周期

Pod 一共有 5 种状态，这个状态反映在 Pod 的 status 属性中，这是 Pod 除了 Metadata 和 Spec 之外的第三个重要字段。这 5 种状态分别是：

1. Pending。这个状态意味着，Pod 的 YAML 文件已经提交给了 Kubernetes，API 对象已经被创建并保存在 Etcd 当中。但是这个 Pod 还没有被调度成功，最常见的原因比如 Pod 中某个容器启动不成功
2. Running。这个状态下，Pod 已经调度成功。也就是它包含的容器都已经创建成功，并且至少有一个正在运行中
3. Succeeded。这个状态意味着，Pod 里的所有容器都正常运行成功并退出了。这种情况在运行一次性任务时最为常见
4. Failed。这个状态下，Pod 里至少有一个容器以不正常的状态退出。这个状态出现时，你得想办法 Debug 这个容器，比如查看 Pod 的事件和日志。
5. Unknown。这是一个异常状态，意味着 Pod 的状态不能集群检测到，这很有可能是主从节点（Master 和 Kubelet）间的通信出现了问题。

## Pod 容器间如何共享东西

Pod 里的所有容器，共享的是同一个 Network Namespace，并且可以声明共享同一个 Volume。实际上，Pod 是共享了 linux namespace 的东西。

我们不妨来做个实验，在下面这个 Pod 的 YAML 文件中，我定义了 shareProcessNamespace=true：

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  shareProcessNamespace: true
  containers:
  - name: nginx
    image: nginx
  - name: shell
    image: busybox
    stdin: true
    tty: true
```

我们通过 `kubectl -n jimmy attach -it nginx -c shell` 能够进入到这个 Pod 的第二个容器，也就是 shell 容器里面。通过 ps -ef 命令，在这个容器里居然能看到 nginx 容器的进程。

![img](https://help-assets.codehub.cn/enterprise/20210604151919.png)

显然，Pod 把 linux namespace 共享了。

那么 Pod 是怎么做到这一点的呢？实际上，Pod 在启动的时候会先启动一个 Infra Container 去设置网络、Volume 等 namespace（如果 Volume 要共享的话），其他容器通过加入的方式共享这些 Namespace。实际上我们在上面的 ps -ef 里面也能看到这个 infra container 的进程 /pause。

![img](https://help-assets.codehub.cn/enterprise/20210604151931.png)

## 使用 Pod 的容器设计模式

Pod 在 Kubernetes 的意义是实现容器设计模式。容器的设计思想，实际上就是希望，当用户想在一个容器里跑多个功能并不相关的应用时，应该优先考虑它们是不是更应该被描述成一个 Pod 里的多个容器。

例如说一个 web 服务的服务本身，和日志收集，他们的业务并不相关，最合理的方式就是使用两个容器去实现。又例如你如果想做一些服务流量的治理，也应该使用一个别的容器而不是耦合在业务代码里。

## 结语

上面的文章中，我们讲述了 Pod 的基本属性，Pod 的生命周期，以及 Pod 的容器设计模式。希望你能从中有所收获，谢谢阅读。
