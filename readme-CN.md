<p align="center">
  <img src="https://user-images.githubusercontent.com/24803604/67205502-87c43800-f42d-11e9-9941-2a27d5dea0fe.png" />
</p>

这是一个帮助理解Kubernetes如何工作的简单说明。我通过这一方式学习Kubernetes并留下这一仓库来记录我学习过程中解决的问题，使得可能为其他初学者带来帮助。我们不会深入docker，但是会有足够的内容来帮你建立起学习Kubernetes的基础理解。希望你能够享受这一学习。如果你觉得有帮助，可以给这个项目一个star。

**Important :-** 通过查看README文件的大小，您可能会有害怕的想法。但说实话，如果你按照其从头学到尾，你不会遇到任何棘手的问题，并在可以在此过程中学习。

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/tripathi.kautilya@gmail.com)

## 正文

- [正文](#正文)
- [前置需求](#前置需求)
- [先了解下简单的概念](#先了解下简单的概念)
    - [Docker是什么](#docker是什么)
- [边写边学](#边写边学)
    - [创建一个web server](#创建一个web-server)
    - [建立docker镜像](#建立docker镜像)
    - [获取docker镜像](#获取docker镜像)
    - [运行容器镜像](#运行容器镜像)
    - [访问你的应用](#访问你的应用)
    - [列出所有正在运行的容器](#列出所有正在运行的容器)
  - [在已存在的容器中运行shell](#在已存在的容器中运行shell)
    - [从内部探索容器](#从内部探索容器)
    - [停止并删除容器](#停止并删除容器)
  - [将镜像推送到镜像仓库](#将镜像推送到镜像仓库)
    - [将镜像推送到DockerHub](#将镜像推送到dockerhub)
  - [Kubernetes是什么](#kubernetes是什么)
    - [分割应用成为微服务](#分割应用成为微服务)
    - [微服务扩容](#微服务扩容)
    - [部署微服务](#部署微服务)
    - [用Kubernetes工作](#用kubernetes工作)
    - [建立Kubernetes集群](#建立kubernetes集群)
  - [在本地通过minikube运行单节点Kubernetes集群](#在本地通过minikube运行单节点kubernetes集群)
    - [通过minikube启动Kubernetes集群](#通过minikube启动kubernetes集群)
    - [检查集群是否已启用并且可以与Kubernetes通信](#检查集群是否已启用并且可以与kubernetes通信)
    - [部署你的节点应用](#部署你的节点应用)
    - [列举pod](#列举pod)
  - [访问你的Web应用](#访问你的web应用)
    - [创建service对象](#创建service对象)
    - [监听services](#监听services)
  - [应用的水平扩容](#应用的水平扩容)
    - [增加应需要的副本数量](#增加应需要的副本数量)
    - [查看扩容后的结果](#查看扩容后的结果)
    - [在列举pod时展示pod的ip以及pod的节点](#在列举pod时展示pod的ip以及pod的节点)
    - [在使用Minikube时访问面板（Dashboard）](#在使用minikube时访问面板dashboard)
  - [Pods](#pods)
    - [检查一个已经存在的pod的yaml描述](#检查一个已经存在的pod的yaml描述)
    - [介绍POD定义的主要部分](#介绍pod定义的主要部分)
    - [为pod创建一个简单的YAML描述](#为pod创建一个简单的yaml描述)
    - [使用kubectl create创建pod](#使用kubectl-create创建pod)
    - [通过Kubectl logs取回pod日志](#通过kubectl-logs取回pod日志)
      - [在获取包含多个容器的pod的日志时标注容器的名称](#在获取包含多个容器的pod的日志时标注容器的名称)
    - [为pod的端口添加本地网络](#为pod的端口添加本地网络)
  - [介绍标签](#介绍标签)
    - [在创建pod时指定标签](#在创建pod时指定标签)
    - [修改已存在pod的标签](#修改已存在pod的标签)
  - [通过标签选择器列出pod的子集](#通过标签选择器列出pod的子集)
    - [通过标签选择器罗列pod](#通过标签选择器罗列pod)
    - [在同一标签选择器中使用多个参数](#在同一标签选择器中使用多个参数)
  - [利用标签限制pod调度](#利用标签限制pod调度)
    - [Using labels for categorizing worker nodes](#using-labels-for-categorizing-worker-nodes)
    - [Scheduling pods to specific nodes](#scheduling-pods-to-specific-nodes)
    - [Scheduling to one specific node](#scheduling-to-one-specific-node)
  - [Annotating pods](#annotating-pods)
    - [Looking up an objects annotations](#looking-up-an-objects-annotations)
    - [Adding and modifying annotations](#adding-and-modifying-annotations)
  - [Using namespace to group resources](#using-namespace-to-group-resources)
    - [Discovering other namespaces and their pods](#discovering-other-namespaces-and-their-pods)
  - [Creating a namespace](#creating-a-namespace)
    - [Managing objects in other namespaces](#managing-objects-in-other-namespaces)
    - [Understanding the isolation provided by namespaces](#understanding-the-isolation-provided-by-namespaces)
  - [Stopping and removing pods](#stopping-and-removing-pods)
    - [Deleting a pod by name](#deleting-a-pod-by-name)
    - [Deleting pods using label selectors](#deleting-pods-using-label-selectors)
    - [Deleting pods by deleting the whole namespace](#deleting-pods-by-deleting-the-whole-namespace)
    - [Deleting all pods in namespace, while keeping the namespace](#deleting-all-pods-in-namespace-while-keeping-the-namespace)
    - [Delete almost all resources in namespace](#delete-almost-all-resources-in-namespace)
  - [Replication and other controllers: Deploying managed pods](#replication-and-other-controllers-deploying-managed-pods)
    - [Keeping pods healthy](#keeping-pods-healthy)
    - [Introducing liveness probes](#introducing-liveness-probes)
    - [Creating an HTTP based liveness probe](#creating-an-http-based-liveness-probe)
    - [Seeing a liveness probe in action](#seeing-a-liveness-probe-in-action)
    - [Configuring additional properties of liveness probe](#configuring-additional-properties-of-liveness-probe)
    - [Creating effective liveness probe](#creating-effective-liveness-probe)
      - [WHAT A LIVENESS PROBE SHOULD CHECK](#what-a-liveness-probe-should-check)
      - [KEEPING PROBES LIGHT](#keeping-probes-light)
      - [DON’T BOTHER IMPLEMENTING RETRY LOOPS IN YOUR PROBES](#dont-bother-implementing-retry-loops-in-your-probes)
      - [LIVENESS PROBE WRAP-UP](#liveness-probe-wrap-up)
  - [Introducing ReplicationControllers](#introducing-replicationcontrollers)
    - [The operation of a ReplicationController](#the-operation-of-a-replicationcontroller)
    - [Introducing the controller reconciliation loop](#introducing-the-controller-reconciliation-loop)
    - [Creating a ReplicationController](#creating-a-replicationcontroller)
    - [Seeing the ReplicationController in action](#seeing-the-replicationcontroller-in-action)
    - [Understanding exactly what caused the controller to create a new pod](#understanding-exactly-what-caused-the-controller-to-create-a-new-pod)
    - [Moving pods in and out of the scope of a ReplicationController](#moving-pods-in-and-out-of-the-scope-of-a-replicationcontroller)
    - [Changing the pod template](#changing-the-pod-template)
    - [Horizontally scaling pods](#horizontally-scaling-pods)
    - [Deleting a ReplicationController](#deleting-a-replicationcontroller)
  - [Using ReplicaSets instead of ReplicationControllers](#using-replicasets-instead-of-replicationcontrollers)
    - [Defining a ReplicaSet](#defining-a-replicaset)
    - [Using the ReplicaSets more expressive label selectors](#using-the-replicasets-more-expressive-label-selectors)
  - [Running exactly one pod on each node with DaemonSets](#running-exactly-one-pod-on-each-node-with-daemonsets)
    - [Using a DaemonSet to run a pod on every node](#using-a-daemonset-to-run-a-pod-on-every-node)
    - [Explaning Daemon sets with an example](#explaning-daemon-sets-with-an-example)
    - [Creating the DaemonSet](#creating-the-daemonset)
  - [Running Pod that perform a single completable task](#running-pod-that-perform-a-single-completable-task)
    - [Introducing the Job resource](#introducing-the-job-resource)
    - [Defining a Job resource](#defining-a-job-resource)
    - [Seeing a Job run a pod](#seeing-a-job-run-a-pod)
- [Todo](#todo)


## 前置需求

你需要:
-  在你的操作系统上安装[Docker](https://www.docker.com/);
- 在本地安装并运行[minikube](https://github.com/kubernetes/minikube)并
- 安装[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

## 先了解下简单的概念

#### Docker是什么

docker是用于打包、分发和运行应用的平台。它允许年在打包你将整个运行环境连同应用一起打包。这可以是应用程序所需的几个库，甚至是已安装操作系统的文件系统上通常可用的所有文件。 docker可以将包传输到中央存储库，并使从该存储库将其传输到运行docker的任何计算机执行变为可能。

三个构成docker的主要概念:
- **镜像（Images）** :- docker镜像是指你包装你的应用和其运行环境形成的东西。它包含了可供应用程序使用的文件系统和其他元数据，例如运行映像时应执行的可执行文件的路径。
- **镜像仓库（Registries）** :- docker镜像仓库是一个存储库，用于存储你的 docker 映像，并有助于在不同用户和计算机之间轻松共享这些镜像。生成镜像时，可以在生成镜像的计算机上运行它，也可以将镜像推送（上传）到镜像仓库，然后在另一台计算机上拉取（下载）镜像并运行它。某些镜像仓库是公共的，允许任何人从中拉取镜像，而有些镜像仓库是私有的，只有某些用户或机器才能访问。
- **容器（Containers）** :- docker的容器就是通过docker镜像创建的常规的linux容器。 一个运行的容器在运行 Docker 的主机会是一个运行中的进程，但它与主机上的其它进程完全隔离。该进程还会受到资源限制，这意味着它只能访问和使用分配给它的资源（CPU、RAM或是其它资源）。

## 边写边学

#### 创建一个web server

你需要先创建一个容器镜像。我们将使用docker完成它。我们创建一个简单的web server来查看kubernetes是如何工作的。（TODO:此处疑为docker，但原文为kubernetes，有待向原作者核实）

- 创建名为 `app.js` 的文件并将下列代码粘贴到其中

```js
const http = require('http');
const os = require('os');
console.log("Kubia server starting...");
var handler = function (request, response) {
  console.log("Received request from " + request.connection.remoteAddress);
  response.writeHead(200);
  response.end("You've hit " + os.hostname() + "\n");
};
var www = http.createServer(handler);
www.listen(8080);

```

现在我们将创建一个Dockerfile，它会在我们创建docker image之后运行在集群上。

- 创建名为 `Dockerfile` 的文件并将下列代码粘贴到其中

```Dockerfile
FROM node:8 

RUN npm i

ADD app.js /app.js

ENTRYPOINT [ "node", "app.js" ]

```

#### 建立docker镜像

确认你的 **Docker server已经启用并运行**。现在我们将在本地创建一个docker镜像。在当前项目目录打开你的Terminal（命令行），并运行

`docker build -t kubia .`

你正在基于当前文件夹内的内容(注意命令末尾的“`.`”)，使用docker创建名字为“**kubia**”的镜像。docker会查看文件夹内的Dockerfile文件并通过文件内的工具建立镜像。

通过运行以下命令查看你的docker镜像：

`docker images`

#### 获取docker镜像

`docker images`

这个命令会以列表形式给出全部镜像。

#### 运行容器镜像

`docker run --name kubia-container -p 8080:8080 -d kubia`

这个命令会使docker通过kubia镜像运行一个名为 **kubia-container** 的新容器。 其与终端分离 (`-d` 参数), 这表示它会在后台运行。 宿主机本地`端口 8080` 会与容器内的 `端口 8080` 匹配 (`-p 8080:8080` 参数), 所以你可以通过访问本地端口8080来查看容器 [localhost](http://localhost:8080).

#### 访问你的应用

在你的命令行中输入如下命令:

`curl localhost:8080`
> You’ve hit 44d76963e8e1

#### 列出所有正在运行的容器

你可以通过如下命令列出所有你正在运行的容器。

`docker ps`

`docker ps` 这一命令只显示容器的大部分主要信息。

如果要获取某个容器的更多信息，可以运行以下命令。

`docker inspect kubia-container`

你可以通过以下命令获悉所有容器。

`docker ps -a`

### 在已存在的容器中运行shell

你构建镜像所使用的Node.js的镜像包含了bash shell，所以你可以在你的容器里运行shell命令，例如：

`docker exec -it kubia-container bash`

这会在已存在的 **kubia-container** 容器中运行bash。  **bash** 进程会与容器主进程共享相同的linux命名空间（namespace）。这可以使得你从内部探索容器并观察node.js和你的应用是如何在容器内运行的。

**`-it`** 参数是下列两个参数的缩写：

- `-i`, 用于确保 STDIN 被保持打开。你需要用它来在shell中输入指令。
- `-t`, 用于重定向一个伪终端（TTY）。

#### 从内部探索容器

让我们来使用下列的shell命令来观察容器中的进程。

```bash
root@c61b9b509f9a:/# ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.4  1.3 872872 27832 ?        Ssl  06:01   0:00 node app.js
root        11  0.1  0.1  20244  3016 pts/0    Ss   06:02   0:00 bash
root        16  0.0  0.0  17504  2036 pts/0    R+   06:02   0:00 ps aux
```

你只看见三个进程。你不能看见宿主机上的其它进程。


正如像拥有一个隔离的进程树一样，每个容器也有一个隔离的文件系统。列出容器内根目录的内容将仅显示容器中的文件，并将包括镜像中的所有文件以及容器运行时创建的任何文件（日志文件或其它类似文件），如以下列表所示。

```bash
root@c61b9b509f9a:/# ls
app.js  bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  package-lock.json  proc  root  run  sbin  srv  sys  tmp  usr  var
```

它包含了 **app.js** 文件和其它 `node:8` （你使用的基础镜像）中的系统文件。

你可以使用To exit the container, you exit the shell by running the **exit** 命令退出容器并返回你的宿主机（正如退出ssh会话一样）。

#### 停止并删除容器

`docker stop kubia-container`

这一命令会停止容器内的主进程并因此停止容器（因为容器内没有其它进程在运行）。容器本身仍会继续存在，你可以通过 **docker ps -a** 命令来查看它。 `-a` 参数会列出所有容器，包括运行中的和已经被停止的。为了真正地删除容器，年需要使用 **docker rm** 命令，例如：

`docker rm kubia-container`

这一命令删除了容器。它的所有内容都被删除了，并且无法被再次重启。

### 将镜像推送到镜像仓库

你之前构建的镜像只在你的本地主机上可用。为了你能够在其它机器上运行它，你需要将它推送到外部的镜像仓库。为简单起见，您不需要设置私有镜像仓库，而是将镜像推送到 [Docker Hub](http://hub.docker.com)。 

在你如此操作之前，你需要根据Docker Hub的规则将你的镜像重新定义标签（tag）。 如果你的镜像名字以你的Docker Hub的ID为开头，Docker Hub 将会允许你推送你的镜像。

你可以在 [hub-docker](http://hub.docker.com) 注册并创建ID。这里我将会以我的ID (`knrt10`) 为例。记得在每次尝试时改为你自己的ID。

当你获知你的ID后，你可以重新命名你的镜像，由现在的 `kubia`改为 `knrt10/kubia` （用你自己的DockerHub ID替换掉 knrt10）：

`docker tag kubia knrt10/kubia`

这个命令不会重新命名tag，它会为这个镜像添加一个额外的tag。你可以通过列出你所有的镜像（使用docker images命令）来确认这一点，正如下面列出的：

`docker images | head`

正如你所看见的， `kubia` 和 `knrt10/kubia` 都指向了同一个镜像ID，所以它们是同一个镜像的不同tag。

#### 将镜像推送到DockerHub

在你推送你的镜像之前，你需要通过 **docker login** 命令使用你的user ID登录。 你在登录后，就可以将 `yourid/kubia` 镜像推送到DockerHub，正如下面所示：

`docker push knrt10/kubia`     

### Kubernetes是什么

很久之前，大多数软件应用是巨大的`屎山`（原文为“monoliths”，直译为独石柱），其作为一个独立进程或者作为少数服务器上的小数量进程进行运行。

如今，这些大型屎山式的应用程序正在慢慢分解为更小的、独立运行的组件，称为 `微服务（microservices）`. 

因为微服务彼此间更`分离`，它们可以被独立开发、部署、更新或扩容。这使得你可以更快地更换部件以应对今日日益加快变化的业务需求。

但随着部署组件数量的增加和数据中心的变大，配置、管理、把持整个系统平稳运行变得日渐困难。

找出降本增效的解决方案变得更加困难。用手动操作去处理这类问题会十分艰难。

我们需要：

- 自动化（包括为我们的servers自动调度组件）；
- 自动化的配置；
- 监督；和 
- 错误处理。

这就是为什么我们需要 **Kubernetes**。

> <em>Kubernetes使得开发者可以在没有运维团队的协助下就能频繁得部署应用。（Kubernetes enables developers to deploy their applications themselves and as often as they want, without requiring any assistance from the operations (ops) team.）</em>

但是Kubernetes不止惠及开发者，它同样通过自动化管理和硬件错误时的重启惠及了运维团队。

系统运维（sysadmins）的重点从监管单个应用程序转移到主要监督和管理Kubernetes和其他基础设施，而Kubernetes负责监管应用程序。

#### 分割应用成为微服务

每一个微服务都运行一个独立的进程并和其它微服务通过简单又定义完善的接口（API）通信。依据下图：

![Microservice](https://user-images.githubusercontent.com/24803604/68068406-bf4bb200-fd54-11e9-8565-6214d30616bb.png)

> <em>- Image taken from other source.</em>


微服务通信通过同步或异步的方式，前者例如HTTP，它们经常使用RESTful (REpresentational State Transfer) API，后者则常见为消息队列。

这些协议都很简单，大多数开发人员都能理解，并且不需要特殊的编程语言。每个微服务都可以被写成它们最合适的语言。

因为单个的微服务是带有一套静态外接API的独立进程，所以可以独立地开发和部署任何一个微服务。改变它们其中之一并不需要重新部署其余微服务，API则不需要更改或者只需要做出先后兼容的更改。

#### 微服务扩容

微服务扩容，有别于屎山程序，你仅仅只需要扩容那些需要更多资源的服务，而让其它服务保持原有的规模。如下图所示：

![Scaling](https://user-images.githubusercontent.com/24803604/68068433-03d74d80-fd55-11e9-87fe-5fad885168d1.png)

> <em>- Image taken from other source.</em>

旧有的大型应用不能被如此扩容，因为它的组件不能被单独扩容；将你的应用分离成微服务使得你可以水平得进行扩容。未能水平扩容的部分亦可进行垂直扩容。


#### 部署微服务

一直以来，微服务也有局限，当你的系统只有小部分组件组成时，管理它们显得较为容易。选择如何部署组建是微不足道的，因为并没有太多的选择。

当组件的数量增加，与部署有关的选择变得显著困难，因为不止是组件的数量增加了，组件间的内在联系、依赖关系也变得更为复杂。

微服务也带来了其它问题，例如难以调试和跟踪执行调用，因为它们跨越多个进程和计算机。幸运的是，这些问题现在正在通过分布式跟踪系统（如Zipkin）来解决。

![Drawback](https://user-images.githubusercontent.com/24803604/68068466-62043080-fd55-11e9-867f-971dc4df862f.png)

> <em>在同一主机上运行的多个应用程序可能具有冲突的依赖项</em>

#### 用Kubernetes工作

现在你可以将你的应用在你的容器镜像内打包，并通过DockerHub使其可以部署在Kubernetes集群中或者直接使用docker运行。但首先，你需要建立Kubernetes集群本身。

#### 建立Kubernetes集群

建立一个完整的、多节点的Setting up a full-fledged, multi-node Kubernetes集群不是一个简单的工作，特别是当你不熟悉linux和网络管理时。

一个正确的Kubernetes安装在多个物理或虚拟的机器并需要通过网络来正确建立，这样所有的Kubernetes集群中运行的容器都可以通过同样的平面网络空间建立连接。

### 在本地通过minikube运行单节点Kubernetes集群

使用minikube是最简单而且最快的运行全功能Kubernetes集群的方式。minikube是一个可以用于建立足以用于测试Kubernetes或开发本地应用的单节点集群的工具。

#### 通过minikube启动Kubernetes集群

当你在本地安装minikube后，你可以立即启动使用以下命令启动Kubernetes：

`minikube start`
```bash
Starting local Kubernetes cluster...
Starting VM...
SSH-ing files into VM...
...
Kubectl is now configured to use the cluster.
```

启动集群可能需要花费一分钟以上，所以不要在命令完成前打断它。

#### 检查集群是否已启用并且可以与Kubernetes通信

为了与Kubernetes交互，你需要 **kubectl** 命令行客户端， 它可以被容易地[安装](https://kubernetes.io/docs/tasks/tools/install-kubectl/) 。

为了校验你的集群是否已在工作，你可以使用下面这条 **kubectl cluster-info** 命令。

`kubectl cluster-info`
```bash
Kubernetes master is running at https://192.168.99.100:8443

kubernetes-dashboard is running at https://192.168.99.100:8443/api/v1/...

KubeDNS is running at https://192.168.99.100:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```

这表示集群已被启用，它展示了多个不同Kubernetes的组件，也包括了API server和Web控制台。

#### 部署你的节点应用

部署你的应用的一种简单方式是通过 **kubectl create** 命令，这会在无需JSON或者YAML的情况下创建所有的必要的组件。

`kubectl create deployment kubia --image=knrt10/kubia --port=8080`

`--image=knrt10/kubia` 显然表示你想要运行的容器镜像，而 `--port=8080` 选项告知了你的应用在监听8080端口。

#### 列举pod

你不能列出单个容器，因为它们不是独立的 Kubernetes 对象，那你能列出 pod 吗？是的，你可以。让我们看看如何告诉 kubectl 在下面的列表中列出 pod。

`kubectl get pods`

```bash
$ kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
kubia-57c4d74858-tflb8   1/1     Running   0          24s
```

### 访问你的Web应用

该如何在pod运行时访问它？每一个pod都含有它自己的IP地址，但这个地址只能在集群内交互而不能从外部访问。你必须通过service对象暴露。

你需要创建一个特殊的LoadBalancer类型的service，而非常规的service（一个集群内IP的service），因为它会像pod一样只能供集群内部访问。通过创建一个LoadBalancer类型的service，会有一个外部的调度器被同步创建，我们可以通过调度器的公共IP来连接内部的pod。

#### 创建service对象

为了创建service，必须告诉Kubernetes暴露你之前创建的部署。

`kubectl expose deploy kubia --type=LoadBalancer --name kubia-http`
> service/kubia-http exposed

**Important:** 我们正在使用缩写 `deploy` 代替 `deployments`。很多资源类型拥有类似的缩写，所以你无需打出它们的全名。（例如， `po` 缩写为 `pods`, `svc` 缩写为 `services`等）

#### 监听services

暴露指令的命令的输出描述了一个名为 `kubia-http` 的服务。服务是类似于pod或者node一样的对象。你可以通过 **kubectl get services | svc** 命令来查看新创建的对象，正如下面所列出的。

`kubectl get svc`

```bash
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes   ClusterIP      10.96.0.1      <none>        443/TCP          30h
kubia-http   LoadBalancer   10.107.88.67   <pending>     8080:32718/TCP   81s
```

**Important** :- Minikube不支持LoadBalancer的服务，所以服务永远不会得到外部IP。但你仍然可以通过外部IP访问它，所以它的外部IP将一直处于pending状态。当你使用minikube时，你可以使用以下命令访问service：

`minikube service kubia-http`

### 应用的水平扩容

你现在拥有一个正在运行的应用，被Deployment管理和保持运行并通过service暴露自身端口。现在，让我们为它增添一点奇迹。
使用Kubernetes的好处之一是可以方便地将部署扩容。让我们来看看增加pod的数量可以变得多么容易。你接下来会使正在运行的容器数量增加到三个。

你的pod被Deployment管理。让我们通过kubectl get命令查看它：

`kubectl get deploy`

```bash
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
kubia   1/1     1            1           4m58s
```

#### 增加应需要的副本数量

为了顺利扩容pod的副本数量，你需要在Deployment改变应需要的副本数量（the desired replica count），方法如下：

`kubectl scale deploy kubia --replicas=3`
> deployment.apps/kubia scaled

你现在已经告诉Kubernetes确保有三个你的pod副本保持时刻运行。注意，你不是在指示Kubernetes采取何种行动。你不是告诉它增加两个pod，而是设置了一个新的“应需要的数量（the desired number）”，并让Kubernetes决定它应采取何种行动来达到你的需求。

#### 查看扩容后的结果

再回来谈谈复制数量的增加。让我们再次列举Deployment来查看应用数量的更新。

`kubectl get deploy`

```bash
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
kubia   3/3     3            3           6m43s
```

因为pod的实际数量已经被增加到三个（正如 CURRENT 列所示），列出所有pod时应显示出三个，而非只有一个。

`kubectl get pods`

```bash
NAME                     READY   STATUS    RESTARTS   AGE
kubia-57c4d74858-d284g   1/1     Running   0          94s
kubia-57c4d74858-tflb8   1/1     Running   0          7m9s
kubia-57c4d74858-wfgmb   1/1     Running   0          94s
```

正如你所见，现在存在三个pod而非先前的一个。如果正在运行的容器处于pending状态，它会在短时间内变为ready，这通常是下载容器镜像和启动容器所需要花费的时间。

如你所见，扩容一个应用是如此难以置信得简单。当你的应用正在产品中在线运行并需要扩容时，你可以通过一个即时的简单命令而不需要安装或运行额外的副本。

记住，应用本身需要支持水平扩容。Kubernetes并非使用魔法让你的应用变得可被扩容，它只是让应用的扩容或缩容变得简单。

#### 在列举pod时展示pod的ip以及pod的节点

如果你之前集中了注意力，那么你可能已经注意到 **kubectl get pods** 命令并没有展示pod被调度的节点（node）的任何信息。这是因为这一信息在通常情况下并不重要。

但你可以通过 **-o wide** 命令请求显示这一额外内容。当列出pod时，这一命令也会同时展示pod的ip以及pod正在运行的节点（node）：

`kubectl get pods -o wide`

```bash
$ kubectl get pods -o wide
NAME                     READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
kubia-57c4d74858-d284g   1/1     Running   0          2m53s   172.17.0.5   minikube   <none>           <none>
kubia-57c4d74858-tflb8   1/1     Running   0          8m28s   172.17.0.3   minikube   <none>           <none>
kubia-57c4d74858-wfgmb   1/1     Running   0          2m53s   172.17.0.4   minikube   <none>           <none>
```

#### 在使用Minikube时访问面板（Dashboard）

在使用minikube运行k8s集群时，可以通过以下命令在你的浏览器中打开面板（dashboad）：

`minikube dashboard`

### Pods

pod和其它Kubernetes资源通常被JSON或YAML列表发送给k8s的REST API.你也可以通过其它更简单的方式来创建资源，例如 **kubectl run** 命令，但它们通常只允许你配置有限的一组资源，而非全部。另外，用yaml文件定义所有你的k8s对象可以使它们能够被储存在同一个版本控制系统中。

#### 检查一个已经存在的pod的yaml描述

 你将使用 **kubectl get** 命令和 **-o yaml** 选项来获取该pod的完整的yaml定义，或者使用 **-o json** 选项来获得完整的json定义，如下列所示：

`kubectl get po kubia-bsksp -o yaml`

#### 介绍POD定义的主要部分

pod的定义包含了几个部分。其一，包含了yaml中使用的k8s的API版本和yaml描述的资源的类型。其次，有三个几乎可以在任何k8s资源中被发现的重要部分：

- **元数据（Metadata）** 包括name, namespace, labels, 和pod的其它信息。
- **Spec** 包括pod的实际内容的描述，例如pod的容器、储存卷和其它数据。
- **Status** 包括正在运行的pod的当前信息，例如pod的状态，每个容器的描述和状态，pod的内部IP和其它的基础信息。

状态部分包含只读运行时数据，用于显示资源在给定时刻的状态。创建新容器时，永远不需要提供状态部分。

前面描述的三个部分显示了 Kubernetes API 对象的典型结构。所有其他对象具有相同的解剖结构。这使得理解新对象相对容易。

博览学习一个 YAML 中的所有单个属性没有多大意义，因此，让我们看看用于创建 Pod 的最基本 YAML 是什么样子的。

#### 为pod创建一个简单的YAML描述

你正要创建一个名为 **kubia-manual.yaml** 的文件（你可以在任何你想要的目录下创建它），或者从仓库的 [kubia-manual.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/kubia-manual.yaml) 处复制。下面展示了这一文件的全部内容。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kubia-manual
spec:
  containers:
  - image: knrt10/kubia
    name: kubia
    ports:
    - containerPort: 8080
      protocol: TCP
```

让我们来测试这一描述的细节。它表示这是 **v1** 版本的Kubernetes API。你描述的资源是一个pod，名为 **kubia-manual** 。这个pod包含了基于 **knrt10/kubia** 镜像的单个容器。你也已经给予了它名字并让它监听 **8080** 端口。

#### 使用kubectl create创建pod

为了从yaml文件创建对象，使用 **kubectl create** 命令：

`kubectl create -f kubia-manual.yaml`
> pod/kubia-manual created

**kubectl create -f** 命令被用于从yaml或json文件创建任何资源（不限于pod）。

#### 通过Kubectl logs取回pod日志

你的node.js应用通过进程的标准输出（standard output）输出日志。容器化的应用通常使用标准输出和标准错误（standard error）而不是输出日志到文件。这可以使用户在一个简单、标准化的方式下查看不同应用的日志。

可以通过在你的本地机器（不需要ssh任何地方）运行下面命令来查看你的pod日志（更精确地，容器的日志）：

`kubectl logs kubia-manual`
> Kubia server starting...

你没有向你的node.js应用发送任何web请求，所以日志只显示了一条简单关于服务启动的日志。正如你所见，取出k8s中正在运行的应用是如此难以置信得简单（如果pod中只包含单个容器）。

##### 在获取包含多个容器的pod的日志时标注容器的名称

如果你的pod包含了多个容器，你不得不在运行 **kubectl logs** 时通过 **-c container name** 选项清楚地标注容器名称。在你的kubia-manual pod中，你设置名称为**kubia**，如果所添加的容器存在于pod中，你会需要如下面所示以获取它的日志：

`kubectl logs kubia-manual -c kubia`

注意你只能获取仍然存在的容器的日志。如果pod已经被删除，那么其日志也会一同被删除。

#### 为pod的端口添加本地网络

当你需要不通过service而访问特定的pod（例如为了debug或者其它理由）， Kubernetes允许你配置pod的端口转发。这通过 **kubectl port-forward** 指令完成。下面的指令会转寄你本地机器的端口 **8888** 到 你的 **kubia-manual** pod的 **8080** 端口。

`kubectl port-forward kubia-manual 8888:8080`

在一个不同的终端中，你可以使用curl来通过运行于本地8888端口的kubectl port-forward代理向你的pod发送HTTP请求：

`curl localhost:8888`
> You've hit kubia-manual

使用端口转发是测试单个pod的有效方式。

### 介绍标签

我们通过标签（labels）来组织pod和其它所有的Kubernetes对象。标签是一种简单、但相当牛逼的Kubernetes特性用以组织pod和其它Kubernetes资源。一个标签是你贴向一个资源的一组随意的key-value对，接着你可以通过选择表情来利用它（根据资源是否包含选择器中指定的标签来筛选资源）。

#### 在创建pod时指定标签

现在，通过创建一个包含两个标签的新pod，您将看到标签的运行情况。创建一个名为 **kubia-manual-with-labels.yaml** 的新文件，或者你可以从[kubia-manual-with-labels.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/kubia-manual-with-labels.yaml)复制。

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kubia-manual-v2
  labels:
    creation_method: manual
    env: prod
spec:
  containers:
  - image: knrt10/kubia
    name: kubia
    ports:
    - containerPort: 8080
      protocol: TCP
```

你已经包含了标签 *creation_method=manual* 和 *env=data.labels* 。你现在可以创建这一pod： 

`kubectl create -f kubia-manual-with-labels.yaml`
> pod/kubia-manual-v2 created

**kubectl get po** 命令默认不会列出任何标签，但你可以通过 **--show-labels** 参数看见它们：

`kubectl get po --show-labels`

```bash
NAME              READY     STATUS    RESTARTS   AGE       LABELS
kubia-5k788       1/1       Running   1          8d        run=kubia
kubia-7zxwj       1/1       Running   1          5d        run=kubia
kubia-bsksp       1/1       Running   1          5d        run=kubia
kubia-manual      1/1       Running   0          7h        <none>
kubia-manual-v2   1/1       Running   0          3m        creation_method=manual,env=prod
```

如果你只关心某一特定的label而非所有的label，你可以通过 **-L** 选项来寻找特定列。再次列出label并展示你在 **kubia-manual-v2** 所贴的label的特定列：

`kubectl get po -L creation_method,env`

#### 修改已存在pod的标签

已经存在的pod也可以被添加或者修改label。因为 **kubia-manual** pod已经被手动创建。让我们为它添加 **creation_method=manual（创建方法：手动）** 标签：

`kubectl label po kubia-manual creation_method=manual`

现在，让我们将 **kubia-manual-v2** pod的 **env=prod** 标签改为 **env=debug** 标签，来演示已存在的标签是如何被修改的。在修改已存在的标签时你需要添加 **--overwrite** 选项。

`kubectl label po kubia-manual-v2 env=debug --overwrite`

### 通过标签选择器列出pod的子集

将标签附加到资源中以便在列出标签时可以看到每个资源旁边的标签，这在列出资源时并不显得那么方便。但是标签与 *标签选择器（label selectors）* 是同步的。标签选择器允许您选择带有特定标签的pod的子集，并对这些pod执行操作。

一个标签选择器可以通过以下方式选择资源：
- 资源包含（或不包含）一个特定键（key）
- 资源包含一个标签含有某一特定键值对（key-value pair）
- 资源包含一个带有特定键的标签，但该键的值与你给出的特定值不同。

#### 通过标签选择器罗列pod

让我们在你之前已经创建的pod上使用标签选择器。你可以通过以下指令来查看所有你之前手动创建的pod（你已经为它们带上了 **creation_method=manual** 标签）：

`kubectl get po -l creation_method=manual`
```bash
NAME              READY     STATUS    RESTARTS   AGE
kubia-manual      1/1       Running   0          22h
kubia-manual-v2   1/1       Running   0          14h
```

可以用以下指令查看其中不带有 **env** 标签的pod：

`kubectl get po -l '!env'`
```bash
NAME           READY     STATUS    RESTARTS   AGE
kubia-5k788    1/1       Running   1          9d
kubia-7zxwj    1/1       Running   1          5d
kubia-bsksp    1/1       Running   1          5d
kubia-manual   1/1       Running   0          22h
```

确保在 **！env** 周围使用单引号，这样bash shell就不会计算感叹号。

#### 在同一标签选择器中使用多个参数

一个标签选择器可以包含多个由逗号分割的选择标准。资源需要满足所有列出的选择标准。你可以执行下面给出的命令：

`kubectl get po -l '!env , !creation_method' --show-labels`

### 利用标签限制pod调度

All the pods you’ve created so far have been scheduled pretty much randomly across your worker nodes. Certain cases exist, however, where you’ll want to have at least a little say in where a pod should be scheduled. A good example is when your hardware infrastructure isn’t homogenous. You never want to say specifically what node a pod should be scheduled to, because that would couple the application to the infrastructure, whereas the whole idea of Kubernetes is hiding the actual infrastructure from the apps that run on it.

#### Using labels for categorizing worker nodes

The pods aren't only kubernetes resource type that you can attach label to. Labels can be attached to any Kubernetes resource including nodes.

Let’s imagine one of the nodes in your cluster contains a GPU meant to be used for general-purpose GPU computing. You want to add a label to the node showing this feature. You’re going to add the label **gpu=true** to one of your nodes (pick one out of the list returned by **kubectl get nodes**):

`kubectl label node minikube gpu=true`
> node/minikube labeled

Now you can use a label selector when listing the nodes, like you did before with pods. List only nodes that include the label *gpu=true*:

`kubectl get node -l gpu=true`

```bash
NAME       STATUS    ROLES     AGE       VERSION
minikube   Ready     master    9d        v1.10.0
```

As expected, only one node has this label. You can also try listing all the nodes and tell kubectl to display an additional column showing the values of each node’s gpu label.

`kubectl get nodes -L gpu`
```bash
NAME       STATUS    ROLES     AGE       VERSION   GPU
minikube   Ready     master    9d        v1.10.0   true
```

#### Scheduling pods to specific nodes

Now imagine you want to deploy a new pod that needs a GPU to perform its work. To ask the scheduler to only choose among the nodes that provide a GPU, you’ll add a node selector to the pod’s YAML. Create a file called **kubia-gpu.yaml** with the following listing’s contents and then use **kubectl create -f kubia-gpu.yaml** to create the pod. The contents of file are

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kubia-gpu
spec:
  nodeSelector:
    gpu: "true"
  containers:
  - image: luksa/kubia
    name: kubia
```

You’ve added a **nodeSelector** field under the spec section. When you create the pod, the scheduler will only choose among the nodes that contain the *gpu=true* label (which is only a single node in your case).

#### Scheduling to one specific node

Similarly, you could also schedule a pod to an exact node, because each node also has a unique label with the key **kubernetes.io/hostname** and value set to the actual hostname of the node. Example shown below

`kubectl get nodes --show-labels`
```bash
NAME       STATUS    ROLES     AGE       VERSION   LABELS
minikube   Ready     master    9d        v1.10.0   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,gpu=true,kubernetes.io/hostname=minikube,node-role.kubernetes.io/master=
```
But setting the *nodeSelector* to a specific node by the hostname label may lead to the pod being unschedulable if the node is offline.

### Annotating pods

In addition to other labels, pods and other objects can also contain annotations. They are also key value pairs, so in essence they are similar to labels, but aren't meant to hold identifying information. They can't be used to group objects the way label can. While objects can be selected through label selectors, there’s no such thing as an annotation selector. On the other hand, annotations can hold much larger pieces of information and are primarily meant to be used by tools. Certain annotations are automatically added to objects by Kubernetes, but others are added by users manually.

A great use to annotating pods is to add desciption to each pod or other API object so that everyone using the cluster can quickly look up information about each individual object. 

#### Looking up an objects annotations

Let’s see an example of an annotation that Kubernetes added automatically to the pod you created in the previous section. To see the annotations, you’ll need to request the full YAML of the pod or use the `kubectl describe` command. You’ll use the first option in the following listing.

`kubectl get po kubia-zb95q -o yaml`
```bash
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubernetes.io/created-by: |
      {"kind":"SerializedReference", "apiVersion":"v1",
      "reference":{"kind":"ReplicationController", "namespace":"default", ...
```

Without going into too many details, as you can see, the `kubernetes.io/created-by`
annotation holds JSON data about the object that created the pod. That’s not something
you’d want to put into a label. Labels should be **short**, whereas annotations can
contain relatively large blobs of data **(up to 256 KB in total)**.

**Important**:- The kubernetes.io/created-by annotations was deprecated in version
`1.8` and will be removed in `1.9`, so you will no longer see it in the YAML.

#### Adding and modifying annotations

Annotations can obviously be added to pods at creation time, the same way label can. But we can also add it after using the following command. Let's try adding this to `kubia-manual` pod now.

`kubectl annotate pod kubia-manual knrt10.github.io/someannotation="messi ronaldo"`

You added the annotation `knrt10.github.io/someannotation` with the value `messi ronaldo`. It’s a good idea to use this format for annotation keys to prevent key collisions. When different tools or libraries add annotations to objects, they may accidentally override each other’s annotations if they don’t use unique prefixes like you did here. You can check your pod now using following command

`kubectl describe po kubia-manual`

### Using namespace to group resources

Previously we saw how labels organize pods and objects into groups. Because each object can have multiple labels, those groups of objects can overlap. Plus, when working with the cluster (through kubectl for example), if you don’t explicitly specify a label selector, you’ll always see all objects.

#### Discovering other namespaces and their pods

Let us first list all the namespaces in our cluster, type the following command

`kubectl get ns`
```bash
NAME          STATUS    AGE
default       Active    9h
kube-public   Active    9h
kube-system   Active    9h
```

Up to this point, you’ve operated only in the `default` namespace. When listing resources with the `kubectl get` command, you’ve never specified the namespace explicitly, so kubectl always defaulted to the default namespace, showing you only the objects in that namespace. But as you can see from the list, the kube-public and the kube-system namespaces also exist. Let’s look at the pods that belong to the `kube-system` namespace, by telling kubectl to list pods in that namespace only:

`kubectl get po -n kube-system`
```bash
NAME                                    READY     STATUS    RESTARTS   AGE
etcd-minikube                           1/1       Running   0          4h
kube-addon-manager-minikube             1/1       Running   1          9h
kube-apiserver-minikube                 1/1       Running   0          4h
kube-controller-manager-minikube        1/1       Running   0          4h
kube-dns-86f4d74b45-w8mqv               3/3       Running   4          9h
kube-proxy-25t92                        1/1       Running   0          4h
kube-scheduler-minikube                 1/1       Running   0          4h
kubernetes-dashboard-5498ccf677-2zcw5   1/1       Running   2          9h
storage-provisioner                     1/1       Running   2          9h
```

I will explain about these pods later (don’t worry if the pods shown here
don’t match the ones on your system exactly). It’s clear from the name of the namespace that these are resources related to the Kubernetes system itself. By having them in this separate namespace, it keeps everything nicely organized. If they were all in the default namespace, mixed in with the resources you create yourself, you’d have a hard time seeing what belongs where, and you might inadvertently delete system resources.

Namespaces enable you to separate resources that don’t belong together into nonoverlapping groups. If several users or groups of users are using the same Kubernetes cluster, and they each manage their own distinct set of resources, they should each use their own namespace. This way, they don’t need to take any special care not to inadvertently modify or delete the other users’ resources and don’t need to concern themselves with name conflicts, because namespaces provide a scope for resource names, as has already been mentioned.

### Creating a namespace

A namespace is a Kubernetes resource like any other, so you can create it by posting a
YAML file to the Kubernetes API server. Let’s see how to do this now. 

You’re going to create a file called **custom-namespace.yaml** (you can create it in any directory you want), or copy from this repo, where you’ll find the file with filename [custom-namespace.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/custom-namespace.yaml). The following listing shows the entire contents of the file.

```yml
apiVersion: v1
kind: Namespace
metadata:
  name: custom-namespace
```

Now type the following command

`kubectl create -f custom-namespace.yaml`
> namespace/custom-namespace created

#### Managing objects in other namespaces

To create resources in the namespace you’ve created, either add a `namespace: customnamespace` entry to the metadata section, or specify the namespace when creating the resource with the `kubectl create` command:

`kubectl create -f kubia-manual.yaml -n custom-namespace`
> pod/kubia-manual created

You now have two pods with the same name (kubia-manual). One is in the `default`
namespace, and the other is in your `custom-namespace`.

When listing, describing, modifying, or deleting objects in other namespaces, you
need to pass the `--namespace (or -n)` flag to kubectl. If you don’t specify the namespace, kubectl performs the action in the default namespace configured in the current kubectl context. The current context’s namespace and the current context itself can be changed through `kubectl config` commands.

#### Understanding the isolation provided by namespaces

To wrap up this section about namespaces, let me explain what namespaces don’t provide at least not out of the box. Although namespaces allow you to isolate objects into distinct groups, which allows you to operate only on those belonging to the specified namespace, they don’t provide any kind of isolation of running objects. For example, you may think that when different users deploy pods across different namespaces, those pods are isolated from each other and can’t communicate but that’s not necessarily the case. Whether namespaces provide network isolation depends on which networking solution is deployed with Kubernetes. When the solution doesn’t provide inter-namespace network isolation, if a pod in namespace foo knows the IP address of a pod in namespace bar, there is nothing preventing it from sending traffic, such as HTTP requests, to the other pod.

### Stopping and removing pods

We have created a number of pods which should all be running. If you have followed from the start, you should have 5 pods in `default` namespace and one in `custom-namespace`. We are going to stop them all now, because we don't need them anymore.

#### Deleting a pod by name

Let's first delele `kubia-gpu` pod name

`kubectl delete po kubia-gpu`

#### Deleting pods using label selectors

Instead of specifying each pod to delete by name, you’ll now use what you’ve learned
about label selectors to stop both the `kubia-manual` and the `kubia-manual-v2` pod.
Both pods include the `creation_method=manual` label, so you can delete them by
using a label selector:

`kubectl delete po -l creation_method=manual`
> pod "kubia-manual" deleted
> pod "kubia-manual-v2" deleted

In the earlier microservices example, where you had tens (or possibly hundreds) of
pods, you could, for instance, delete all canary pods at once by specifying the
`rel=canary` label selector

`kubectl delete po -l rel=canary`

#### Deleting pods by deleting the whole namespace

Okay, back to your real pods. What about the pod in the `custom-namespace`? We no
longer need either the pods in that namespace, or the namespace itself. You can delete the whole namespace using the following command. Your all pods inside that workspace will be automatically deleted.

`kubectl delete ns custom-namespace`
> namespace "custom-namespace" deleted

#### Deleting all pods in namespace, while keeping the namespace

Suppose you want to keep your namespace but delete all the pods in it, so this is the approach to follow. We now have cleaned almost everything but we have some pods running if you ran the `kubectl run` command before.

This time, instead of deleting the specific pod, tell Kubernetes to delete all pods in the current namespace by using the --all option

`kubectl delete po --all`
```bash
pod "kubia-pjxrs" deleted
pod "kubia-xvfxp" deleted
pod "kubia-zb95q" deleted
```

Now, double check that no pods were left running:

`kubectl get po`
```bash
kubia-5gknm   1/1       Running   0          48s
kubia-h62k7   1/1       Running   0          48s
kubia-x4nsb   1/1       Running   0          48s
```

Wait, what!?! All pods are terminating, but a new pod which weren't there before, has appeared. No matter how many times you delete all pods, a new pod called kubia-something will emerge.

You may remember you created your first pod with the `kubectl run` command. I mentioned that this doesn’t create a pod directly, but instead creates a `ReplicationController`, which then creates the pod. As soon as you delete a pod created by the ReplicationController, it immediately creates a new one. To delete the pod, you also need to **delete the ReplicationController**.

#### Delete almost all resources in namespace

You can delete the ReplicationController and the pods, as well as all the Services
you’ve created, by deleting all resources in the current namespace with a single
command:

`kubectl delete all --all`
```bash
pod "kubia-5gknm" deleted
pod "kubia-h62k7" deleted
pod "kubia-x4nsb" deleted
replicationcontroller "kubia" deleted
service "kubernetes" deleted
service "kubia-http" deleted
```

The first all in the command specifies that you’re deleting resources of all types, and the --all option specifies that you’re deleting all resource instances instead of specifying them by name (you already used this option when you ran the previous delete command).

As it deletes resources, kubectl will print the name of every resource it deletes. In the list, you should see the kubia ReplicationController and the `kubia-http` Service you created before.

**Note**:- The kubectl delete all --all command also deletes the kubernetes
Service, but it should be recreated automatically in a few moments.

### Replication and other controllers: Deploying managed pods 

As far now, you might have understood that pods represent the basic deployment unit in Kubernetes. We know how to create, supervise and manage them manually. But in real-world use cases, you want your deployments to stay up and running automatically and remain healthy without any manual intervention. To do this, we `never almost create pods directly`. Instead we create other type of resources like **ReplicationControllers** or **Deployments** which then create and manage the actual pods.

When you create unmanaged pods (such as the ones we created previously), a cluster node is selected to run the pod and then its containers are run on that node. Now, we'll learn that Kubernetes then monitors those containers and automatically restarts them if they fail. But if the whole node fails, the pods on the node are lost and will not be replaced with new ones, unless those pods are managed by the previously mentioned ReplicationControllers or similar. 

We'll now learn how Kubernetes checks if a container is still alive and restarts it if it isn’t. We’ll also learn how to run managed pods—both those that run indefinitely and those that perform a single task and then stop.

#### Keeping pods healthy

One of the main benefits of using Kubernetes is the ability to give it a list of containers and let it keep those containers running somewhere in the cluster. You do this by creating a Pod resource and letting Kubernetes pick a worker node for it and run the pod’s containers on that node. But what if one of those containers dies? What if all containers of a pod die?

As soon as a pod is scheduled to a node, the Kubelet on that node will run its containers and, from then on, keep them running as long as the pod exists. If the container’s main process crashes, the Kubelet will restart the container. If your application has a bug that causes it to crash every once in a while, Kubernetes will restart it automatically, so even without doing anything special in the app itself, running the app in Kubernetes automatically gives it the ability to heal itself.

But sometimes apps stop working without their process crashing. For example, a Java app with a memory leak will start throwing `OutOfMemoryErrors`, but the JVM process will keep running. It would be great to have a way for an app to signal to Kubernetes that it’s no longer functioning properly and have Kubernetes restart it.

We’ve said that a container that crashes is restarted automatically, so maybe you’re thinking you could catch these types of errors in the app and exit the process when they occur. You can certainly do that, but it still doesn’t solve all your problems.

For example, what about those situations when your app stops responding because it falls into an infinite loop or a deadlock? To make sure applications are restarted in such cases, you must check an application’s health from the outside and not depend on the app doing it internally.

#### Introducing liveness probes

Kubernetes can check if a container is still alive through `liveness probes`. You can specify a liveness probe for each container in the pod's specification. Kubernetes can probe the container using one of three mechanisms:

- An `HTTP GET` probe performs an HTTP GET request on the container's IP address, a port and path you specify. If the probe receives a response and the response code doesn’t represent an error **(in other words, if the HTTP response code is 2xx or 3xx)**, the probe is considered successful. If the server returns an error response code or if it doesn’t respond at all, the probe is considered a failure and the container will be restarted as a result.

- A `TCP Socket` probe tries to open a TCP connection to the specified port of the container. If the connection is established successfully, the probe is successful. Otherwise, the container is restarted.

- An `Exec` probe executes an arbitrary command inside the container and checks the command’s exit status code. If the status code is 0, the probe is successful. All other probes are considered as failure.

#### Creating an HTTP based liveness probe

Let’s see how to add a liveness probe to your Node.js app. Because it’s a web app, it makes sense to add a liveness probe that will check whether its web server is serving requests. But because this particular Node.js app is too simple to ever fail, you’ll need to make the app fail artificially.

To properly demo liveness probes, you’ll modify the app slightly and make it return a `500 Internal Server Error HTTP status code` for each request after the fifth one—your app will handle the first five client requests properly and then return an error on every subsequent request. Thanks to the liveness probe, it should be restarted when that happens, allowing it to properly handle client requests again.

I’ve pushed the container image to Docker Hub, so you don’t need to build it yourself. If you want you can see folder [kubia-unhealthy](https://github.com/knrt10/kubernetes-basicLearning/tree/master/kubia-unhealthy) for more information. You’ll create a new pod that includes an HTTP GET liveness probe. The following listing shows the YAML for the pod.

You’re going to create a file called **kubia-liveness-probe.yaml** (you can create it in any directory you want), or copy from this repo, where you’ll find the file with filename [kubia-liveness-probe.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/kubia-liveness-probe.yaml). The following listing shows the entire contents of the file.

```yml
apiVersion: v1
kind: Pod
metadata:
  name: kubia-liveness
spec:
  containers:
  - image: knrt10/kubia-unhealthy
    name: kubia
    livenessProbe:
      httpGet:
        path: /
        port: 8080
```

The pod descriptor defines an httpGet liveness probe, which tells Kubernetes to periodically perform HTTP GET requests on path / on port 8080 to determine if the container is still healthy. These requests start as soon as the container is run.

After five such requests (or actual client requests), your app starts returning HTTP status `code 500`, which Kubernetes will treat as a probe failure, and will thus restart the container.

#### Seeing a liveness probe in action

To see what a liveness probe does, try creating a pod now. After about a minute and a half, the container will be restarted. You can see that by running `kubectl get`

`kubectl get po kubia-liveness`

```bash
NAME READY STATUS RESTARTS AGE
kubia-liveness 1/1 Running 1 2m
```

The `RESTARTS` column shows that the pod’s container has been restarted once (if you
wait another minute and a half, it gets restarted again, and then the cycle continues
indefinitely).

You can see why the container had to be restarted by looking at what `kubectl describe` prints out. You can see that the container is currently running, but it previously terminated because of an error. The `exit code` was **137**, which has a special meaning. It denotes that the process was terminated by an external signal. The number 137 is a sum of two numbers: `128+x`, where x is the signal number sent to the process that caused it to terminate.

In the example, `x equals 9`, which is the number of the `SIGKILL` signal, meaning the process was killed forcibly. When a container a killed, a completely new container is created it's not the same container being restarted again.

#### Configuring additional properties of liveness probe

You may have noticed that `kubectl describe` also displays additional information
about the liveness probe:

```yml
Liveness: http-get http://:8080/ delay=0s timeout=1s period=10s #success=1
➥ #failure=3
```

Beside the liveness probe options you specified explicitly, you can also see additional properties, such as `delay, timeout, period`, and so on. The delay=0s part shows that  the probing begins immediately after the container is started. The timeout is set to only 1 second, so the container must return a response in 1 second or the probe is counted as failed. The container is probed every 10 seconds (period=10s) and the container is restarted after the probe fails three consecutive times (#failure=3).

If you don’t set the initial delay, the prober will start probing the container as soon as it starts, which usually leads to the probe failing, because the app isn’t ready to start receiving requests. If the number of failures exceeds the failure threshold, the container is restarted before it’s even able to start responding to requests properly.

**TIP**:- Always remember to set an initial delay to account for your app’s startup time.

I’ve seen this on many occasions and users were confused why their container was being restarted. But if they’d used `kubectl describe`, they’d have seen that the container terminated with exit code 137 or 143, telling them that the pod was terminated externally. Additionally, the listing of the pod’s events would show that the container was killed because of a failed liveness probe. If you see this happening at pod startup, it’s because you failed to set `initialDelaySeconds` appropriately.

#### Creating effective liveness probe

**For pods running in production**, you should always define a liveness probe. Without one, Kubernetes has no way of knowing whether your app is still alive or not. As long as the process is still running, Kubernetes will consider the container to be healthy.

##### WHAT A LIVENESS PROBE SHOULD CHECK

Your simplistic liveness probe simply checks if the server is responding. While this may seem overly simple, even a liveness probe like this does wonders, because it causes the container to be restarted if the web server running within the container stops responding to HTTP requests. Compared to having no liveness probe, this is a major improvement, and may be sufficient in most cases.

But for a better liveness check, you’d configure the probe to perform requests on a specific URL path `(/health, for example)` and have the app perform an internal status check of all the vital components running inside the app to ensure none of them has died or is unresponsive.

**TIP**:- Make sure the /health HTTP endpoint doesn’t require authentication; otherwise the probe will always fail, causing your container to be restarted indefinitely.

Be sure to check only the internals of the app and nothing influenced by an external factor. For example, a frontend web server’s liveness probe shouldn’t return a failure when the server can’t connect to the backend database. If the underlying cause is in the database itself, restarting the web server container will not fix the problem. Because the liveness probe will fail again, you’ll end up with the container restarting repeatedly until the database becomes accessible again.

##### KEEPING PROBES LIGHT

Liveness probes shouldn’t use too many computational resources and shouldn’t take too long to complete. By default, the probes are executed relatively often and are only allowed one second to complete. Having a probe that does heavy lifting can slow down your container considerably. Later in the book, you’ll also learn about how to limit CPU time available to a container. The probe’s CPU time is counted in the container’s CPU time quota, so having a heavyweight liveness probe will reduce the CPU time available to the main application processes.

##### DON’T BOTHER IMPLEMENTING RETRY LOOPS IN YOUR PROBES

You’ve already seen that the failure threshold for the probe is configurable and usually the probe must fail multiple times before the container is killed. But even if you set the failure threshold to 1, Kubernetes will retry the probe several times before considering it a single failed attempt. Therefore, implementing your own retry loop into the probe is wasted effort.

##### LIVENESS PROBE WRAP-UP

You now understand that Kubernetes keeps your containers running by restarting them if they crash or if their liveness probes fail. This job is performed by the Kubelet on the node hosting the pod the Kubernetes Control Plane components running on the master(s) have no part in this process.

But if the node itself crashes, it’s the Control Plane that must create replacements for all the pods that went down with the node. It doesn’t do that for pods that you create directly. Those pods aren’t managed by anything except by the Kubelet, but because the Kubelet runs on the node itself, it can’t do anything if the node fails.

To make sure your app is restarted on another node, you need to have the pod managed by a ReplicationController or similar mechanism later on in this readme.

### Introducing ReplicationControllers

A Replication Controller(RC) is a Kubernetes resource that ensures its pods are always kept running. If a pod disappers for any reasons like in case of node disappearing from the cluster or because the pod was evicted from the node, the RC notes the pod missing and creates a replacement pod. Please refer to the image below

![RC](https://user-images.githubusercontent.com/24803604/70711851-6c2c2e00-1d08-11ea-90cd-1feba139645d.png)

> When a node fails, only pods backed by a ReplicationController are recreated.

The RC in the figure only manage only a single pod but in general they are meant to create and manage a mutiple copies (replicas) of a pod. That's where RC got their name from.

#### The operation of a ReplicationController

The RC contantly monitors the list of running pods and makes sure the actual number of pods of a "type" always matches the desires number. If too few such pods are running, it creates new replica from pod template. If too much pods are running, it remove the excess replicas.

You might be wondering how there can be more than the desired number of replicas. This can happen for a few reasons:

- Someone creates a pod of the same type manually.
- Someone changes an existing pod’s “type.”
- Someone decreases the desired number of pods, and so on.

I’ve used the term pod “type” a few times. But no such thing exists. Replication Controllers don’t operate on pod types, but on sets of pods that match a certain label selector, which I have told you previously.

#### Introducing the controller reconciliation loop

A ReplicationController’s job is to make sure that an exact number of pods always matches its label selector. If it doesn’t, the ReplicationController takes the appropriate action to reconcile the actual with the desired number.

![controller-reconcilition-loop](https://user-images.githubusercontent.com/24803604/70713322-c5e22780-1d0b-11ea-9334-3d9213e86d3c.png)

A ReplicationController has three essential parts:

- A label selector, which determines what pods are in the ReplicationController’s scope
- A replica count, which specifies the desired number of pods that should be running
- A pod template, which is used when creating new pod replicas

![RC three parts](https://user-images.githubusercontent.com/24803604/70715546-8964fa80-1d10-11ea-8e33-59f1a5a36698.png)

> The three key parts of a
ReplicationController (pod selector,
replica count, and pod template)

A ReplicationController’s replica count, the label selector, and even the pod template can all be modified at any time, but only changes to the replica count affect existing pods.

Changes to the label selector and the pod template have no effect on existing pods. Changing the label selector makes the existing pods fall out of the scope of the ReplicationController, so the controller stops caring about them. ReplicationControllers also don’t care about the actual “contents” of its pods (the container images, environment variables, and other things) after they create the pod. The template therefore only affects new pods created by this ReplicationController. You can think of it as a cookie cutter for cutting out new pods.

**BENEFITS**

- It makes sure a pod (or multiple pod replicas) is always running by starting a
new pod when an existing one goes missing.
- When a cluster node fails, it creates replacement replicas for all the pods that
were running on the failed node (those that were under the Replication-
Controller’s control).
- It enables easy horizontal scaling of pods—both manual and automatic

**Note**:- A pod instance is never relocated to another node. Instead, the ReplicationController creates a completely new pod instance that has no relation to the instance it’s replacing.

#### Creating a ReplicationController

You’re going to create a file called **kubia-rc.yaml** (you can create it in any directory you want), or copy from this repo, where you’ll find the file with filename [kubia-rc.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/kubia-rc.yaml). The following listing shows the entire contents of the file.

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: kubia
spec:
  replicas: 3
  selector:
    app: kubia
  template:
    metadata:
      labels:
        app: kubia
    spec:
      containers:
      - name: kubia
        image: knrt10/kubia
        ports:
        - containerPort: 8080
```

When you post the file to the API server, Kubernetes creates a new ReplicationController named `kubia`, which makes sure three pod instances always match the label selector `app=kubia`. When there aren’t enough pods, new pods will be created from the provided pod template. The contents of the template are almost identical to pod defination we created before.

The pod labels in the template must obviously match the label selector of the ReplicationController; otherwise the controller would create new pods indefinitely, because spinning up a new pod wouldn’t bring the actual replica count any closer to the desired number of replicas. To prevent such scenarios, the API server verifies the ReplicationController definition and will not accept it if it’s misconfigured.

Not specifying the selector at all is also an option. In that case, it will be configured automatically from the labels in the pod template.

To create the ReplicationController, use the `kubectl create` command, which you already know:

`kubectl create -f kubia-rc.yaml`
> replicationcontroller "kubia" created

#### Seeing the ReplicationController in action

Because no pods exist with the `app=kubia` label, the ReplicationController should spin up three new pods from the pod template. List the pods to see if the ReplicationController has done what it’s supposed to:

`kubectl get po`

```bash
NAME          READY   STATUS              RESTARTS   AGE
kubia-53thy   0/1     ContainerCreating   0          6s
kubia-k0xz6   0/1     ContainerCreating   0          6s
kubia-q3vkg   0/1     ContainerCreating   0          6s
```

Indeed, it has! We wanted three pods, and it created three pods. It’s now managing those three pods. Next we'll mess with them a little to see how the ReplicationController responds. Now try deleting a pod, the RC will spawn another pod automatically. The ReplicationController has done its job again. It’s a nice little helper, isn’t it?

#### Understanding exactly what caused the controller to create a new pod

The controller is responding to the deletion of a pod by creating a new replacement pod as we did above. Well, technically, it isn’t responding to the deletion itself, but the resulting state—the inadequate number of pods. 

While a ReplicationController is immediately notified about a pod being deleted (the API server allows clients to watch for changes to resources and resource lists), that’s not what causes it to create a replacement pod. The notification triggers the controller to check the actual number of pods and take appropriate action.

![pod-deleting-info](https://user-images.githubusercontent.com/24803604/71673599-d2700380-2d3e-11ea-92c6-fc36300db222.png)

> If a pod disappears, the ReplicationController sees too few pods and creates a new replacement pod.

Seeing the ReplicationController respond to the manual deletion of a pod isn’t too interesting, so let’s look at a better example. If you’re using Google Kubernetes Engine to run these examples, you have a three-node Kubernetes cluster. You’re going to disconnect one of the nodes from the network to simulate a node failure.

**Note**:- If you’re using Minikube, you can’t do this exercise, because you only have one node that acts both as a master and a worker node.

If a node fails in the non-Kubernetes world, the ops team would need to migrate the applications running on that node to other machines manually. Kubernetes, on the other hand, does that automatically. Soon after the ReplicationController detects that its pods are down, it will spin up new pods to replace them.

Let’s see this in action. You need to ssh into one of the nodes with the `gcloud compute ssh` command and then shut down its network interface with `sudo ifconfig eth0 down`, as shown in the following below.

```bash
gcloud compute ssh gke-kubia-default-pool-b46381f1-zwko`

Enter passphrase for key '/home/knrt10/.ssh/google_compute_engine':
Welcome to Kubernetes v1.16.2!
```

...

```bash
knrt10@gke-kubia-default-pool-b46381f1-zwko ~ $ sudo ifconfig eth0 down
```

When you shut down the network interface, the ssh session will stop responding, so you need to open up another terminal or hard-exit from the ssh session. In the new terminal you can list the nodes to see if Kubernetes has detected that the node is down. This takes a minute or so. Then, the node’s status is shown as `NotReady`:

![GCE node info](https://user-images.githubusercontent.com/24803604/71674165-27604980-2d40-11ea-9f4e-4aa27b148ff5.png)

If you list the pods now, you’ll still see the same three pods as before, because Kubernetes waits a while before rescheduling pods (in case the node is unreachable because of a temporary network glitch or because the Kubelet is restarting). If the node stays unreachable for several minutes, the status of the pods that were scheduled to that node changes to `Unknown`. At that point, the ReplicationController will immediately spin up a new pod. You can see this by listing the pods again:

![GCE pod info](https://user-images.githubusercontent.com/24803604/71674301-75754d00-2d40-11ea-8d5b-c27598eb55a5.png)

Looking at the age of the pods, you see that the kubia-dmdck pod is new. You again have three pod instances running, which means the ReplicationController has again done its job of bringing the actual state of the system to the desired state.

The same thing happens if a node fails (either breaks down or becomes unreachable). No immediate human intervention is necessary. The system heals itself automatically. To bring the node back, you need to reset it with the following command:

`gcloud compute instances reset gke-kubia-default-pool-b46381f1-zwko`

When the node boots up again, its status should return to `Ready`, and the pod whose status was `Unknown` will be deleted.

#### Moving pods in and out of the scope of a ReplicationController

Pods created by a ReplicationController aren’t tied to the ReplicationController in any way. At any moment, a ReplicationController manages pods that match its label selector. By changing a pod’s labels, it can be removed from or added to the scope of a ReplicationController. It can even be moved from one ReplicationController to another.

**TIP**:- Although a pod isn’t tied to a ReplicationController, the pod does reference it in the `metadata.ownerReferences` field, which you can use to easily find which ReplicationController a pod belongs to.

If you change a pod’s labels so they no longer match a ReplicationController’s label selector, the pod becomes like any other manually created pod. It’s no longer managed by anything. If the node running the pod fails, the pod is obviously not rescheduled. But keep in mind that when you changed the pod’s labels, the replication controller noticed one pod was missing and spun up a new pod to replace it.

`kubectl label po kubia-dmdck app=kubia2 --overwrite`

The --overwrite argument is necessary; otherwise kubectl will only print out a warning and won’t change the label, to prevent you from inadvertently changing an existing label’s value when your intent is to add a new one. There, you now have four pods altogether: one that isn’t managed by your ReplicationController and three that are. Among them is the newly created pod.

![RC pod relabelling](https://user-images.githubusercontent.com/24803604/71676804-c38d4f00-2d46-11ea-83fc-ad635ad2ae3a.png)

> Removing a pod from the scope of a ReplicationController by changing its labels

ReplicationController spins up pod kubia-2qneh to bring the number back up to three. Pod kubia-dmdck is now completely independent and will keep running until you delete it manually (you can do that now, because you don’t need it anymore).

**REMOVING PODS FROM CONTROLLERS IN PRACTICE**

Removing a pod from the scope of the ReplicationController comes in handy when you want to perform actions on a specific pod. For example, you might have a bug that causes your pod to start behaving badly after a specific amount of time or a specific event. If you know a pod is malfunctioning, you can take it out of the ReplicationController’s scope, let the controller replace it with a new one, and then debug or play with the pod in any way you want. Once you’re done, you delete the pod.

#### Changing the pod template

A ReplicationController’s pod template can be modified at any time. Changing the pod template is like replacing a cookie cutter with another one. It will only affect the cookies you cut out afterward and will have no effect on the ones you’ve already cut (see figure below). To modify the old pods, you’d need to delete them and let the Replication- Controller replace them with new ones based on the new template.

![pod template change](https://user-images.githubusercontent.com/24803604/71677160-b3c23a80-2d47-11ea-9773-3985f1cfc15e.png)

> Changing a ReplicationController’s pod template only affects pods created afterward and has no effect on existing pods.

As an exercise, you can try editing the ReplicationController and adding a label to the pod template. You can edit the ReplicationController with the following command:

`kubectl edit rc kubia`

This will open the ReplicationController’s YAML definition in your default text editor. Find the pod template section and add an additional label to the metadata. After you save your changes and exit the editor, kubectl will update the ReplicationController and print the following message:

`replicationcontroller "kubia" edited`

You can now list pods and their labels again and confirm that they haven’t changed. But if you delete the pods and wait for their replacements to be created, you’ll see the new label.

Editing a ReplicationController like this to change the container image in the pod template, deleting the existing pods, and letting them be replaced with new ones from the new template could be used for upgrading pods, but you’ll learn a better way of doing it later.

#### Horizontally scaling pods

Scaling the number of pods up or down is as easy as changing the value of the replicas field in the ReplicationController resource. After the change, the ReplicationController will either see too many pods exist (when scaling down) and delete part of them, or see too few of them (when scaling up) and create additional pods. You already know the command below

`kubectl scale rc kubia --replicas=10`

but instead of using the `kubectl scale` command, you’re going to scale it in a declarative way by editing the ReplicationController’s definition: 

`kubectl edit rc kubia`

When the text editor opens, find the spec.replicas field and change its value to 10. Now check your listing.

```bash
kubectl get rc

NAME DESIRED CURRENT READY AGE
kubia 10      10      4     21m
```

Now scale back down to 3. You can use the kubectl scale command:

`kubectl scale rc kubia --replicas=3`

Horizontally scaling pods in Kubernetes is a matter of stating your desire: "I want to have x number of instances running." You’re not telling Kubernetes what or how to do it. You’re just specifying the desired state.

This declarative approach makes interacting with a Kubernetes cluster easy. Imagine if you had to manually determine the current number of running instances and then explicitly tell Kubernetes how many additional instances to run. That’s more work and is much more error-prone. Changing a simple number is much easier and later, you’ll learn that even that can be done by Kubernetes itself if you enable horizontal pod auto-scaling.

#### Deleting a ReplicationController

When you delete a ReplicationController through kubectl delete, the pods are also deleted. But because pods created by a ReplicationController aren’t an integral part of the ReplicationController, and are only managed by it, you can delete only the ReplicationController and leave the pods running, as shown below

![deleing-RC](https://user-images.githubusercontent.com/24803604/71678495-ec174800-2d4a-11ea-909f-e87fd2f33bdf.png)

This may be useful when you initially have a set of pods managed by a ReplicationController, and then decide to replace the ReplicationController with a `ReplicaSet`. You can do this without affecting the pods and keep them running without interruption while you replace the ReplicationController that manages them.

When deleting a ReplicationController with kubectl delete, you can keep its pods running by passing the `--cascade=orphan` option to the command. Try that now:

`kubectl delete rc kubia --cascade=orphan`

You’ve deleted the ReplicationController so the pods are on their own. They are no longer managed. But you can always create a new ReplicationController with the proper label selector and make them managed again.

### Using ReplicaSets instead of ReplicationControllers

Initially, ReplicationControllers were the only Kubernetes component for replicating pods and rescheduling them when nodes failed. Later, a similar resource called a ReplicaSet was introduced. It’s a new generation of ReplicationController and replaces it completely (ReplicationControllers will eventually be deprecated).

We could have started this section by creating a ReplicaSet instead of a ReplicationController, but I felt it would be a good idea to start with what was initially available in Kubernetes **(Please Don't report me :wink:)**. Plus, we'll still see ReplicationControllers used in the wild, so it’s good for you to know about them. That said, you should always create ReplicaSets instead of ReplicationControllers from now on. They’re almost identical, so you shouldn’t have any trouble using them instead.

A ReplicaSet behaves exactly like a ReplicationController, but it has more expressive pod selectors. Whereas a ReplicationController’s label selector only allows matching pods that include a certain label, a ReplicaSet’s selector also allows matching pods that lack a certain label or pods that include a certain label key, regardless of its value.

Also, for example, a single ReplicationController can’t match pods with the label `env=production` and those with the label `env=devel` at the same time. It can only match either pods with the env=production label or pods with the env=devel label. But a single ReplicaSet can match both sets of pods and treat them as a single group.

Similarly, a ReplicationController can’t match pods based merely on the presence of a label key, regardless of its value, whereas a ReplicaSet can. For example, a ReplicaSet can match all pods that include a label with the key env, whatever its actual value is(you can think of it as env=*).

#### Defining a ReplicaSet

You’re going to create a ReplicaSet now to see how the orphaned pods that were created by your ReplicationController and then abandoned earlier can now be adopted by a ReplicaSet. 

You’re going to create a file called **kubia-replicaset.yaml** (you can create it in any directory you want), or copy from this repo, where you’ll find the file with filename [kubia-replicaset.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/kubia-replicaset.yaml). The following listing shows the entire contents of the file.

```yml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: kubia
spec:
  replicas: 3
  selector:
    matchLabels:
      app: kubia
  template:
    metadata:
      labels:
        app: kubia
    spec:
      containers:
      - name: kubia
        image: knrt10/kubia
        ports:
        - containerPort: 8080
```

The first thing to note is that ReplicaSets aren’t part of the v1 API, so you need to ensure you specify the proper apiVersion when creating the resource. You’re creating a resource of type ReplicaSet which has much the same contents as the ReplicationController you created earlier.

The only difference is in the selector. Instead of listing labels the pods need to have directly under the selector property, you’re specifying them under selector `matchLabels`. This is the simpler (and less expressive) way of defining label selectors in a ReplicaSet. Because you still have three pods matching the app=kubia selector running from earlier, creating this ReplicaSet will not cause any new pods to be created. The ReplicaSet will take those existing three pods under its wing. You can create ReplicaSet using `kubectl create` command. Then examine using `kubectl describe` command. 

As you can see, the ReplicaSet isn’t any different from a ReplicationController. It’s showing it has three replicas matching the selector. If you list all the pods, you’ll see they’re still the same three pods you had before. The ReplicaSet didn’t create any new ones.

#### Using the ReplicaSets more expressive label selectors

The main improvements of ReplicaSets over ReplicationControllers are their more expressive label selectors. You intentionally used the simpler matchLabels selector in the first ReplicaSet example to see that ReplicaSets are no different from ReplicationControllers. 

You can add additional expressions to the selector. As in the example, each expression must contain a key, an operator, and possibly (depending on the operator) a list of values. You’ll see four valid operators:

- `In`—Label’s value must match one of the specified values.
- `NotIn`—Label’s value must not match any of the specified values.
- `Exists`—Pod must include a label with the specified key (the value isn’t important).
When using this operator, you shouldn’t specify the values field.
- `DoesNotExist`—Pod must not include a label with the specified key. The values
property must not be specified.

If you specify multiple expressions, all those expressions must evaluate to true for the selector to match a pod. If you specify both matchLabels and matchExpressions, all the labels must match and all the expressions must evaluate to true for the pod to match the selector.

This was a quick introduction to ReplicaSets as an alternative to ReplicationControllers. Remember, always use them instead of ReplicationControllers, but you may still find ReplicationControllers in other people’s deployments.

Now, delete the ReplicaSet to clean up your cluster a little. You can delete the ReplicaSet the same way you’d delete a ReplicationController:

`kubectl delete rs kubia`
> replicaset "kubia" deleted

Deleting the ReplicaSet should delete all the pods. List the pods to confirm that’s the case.

### Running exactly one pod on each node with DaemonSets

Both RC and RS are used for running specifics number of pods deployed anywhere in Kubernetes cluster. But certain cases exist when you want a pod to run on each and every node in the cluster (and each node needs to run exactly one instance of the pod). Those cases include infrastructure related pods that perform system-level operations.

For example, you’ll want to run a log collector and a resource monitor on every node. Another good example is Kubernetes’ own kube-proxy process, which needs to run on all nodes to make services work.

![Daemon Sets](https://user-images.githubusercontent.com/24803604/71682868-9183e900-2d56-11ea-9cab-e645ef0564b1.png)

> DaemonSets run only a single pod replica on each node, whereas ReplicaSets scatter them around the whole cluster randomly.

#### Using a DaemonSet to run a pod on every node

To run a pod on all cluster nodes, you create a DaemonSet object, which is much like a ReplicationController or a ReplicaSet, except that pods created by a DaemonSet already have a target node specified and skip the Kubernetes Scheduler. They aren’t scattered around the cluster randomly.

A DaemonSet makes sure it creates as many pods as there are nodes and deploys each one on its own node, as shown above. Whereas a ReplicaSet (or ReplicationController) makes sure that a desired number of pod replicas exist in the cluster, a DaemonSet doesn’t have any notion of a desired replica count. It doesn’t need it because its job is to ensure that a pod matching its pod selector is running on each node.

If a node goes down, the DaemonSet doesn’t cause the pod to be created elsewhere. But when a new node is added to the cluster, the DaemonSet immediately deploys a new pod instance to it. It also does the same if someone inadvertently deletes one of the pods, leaving the node without the DaemonSet’s pod. Like a ReplicaSet, a DaemonSet creates the pod from the pod template configured in it.

#### Explaning Daemon sets with an example

Let’s imagine having a daemon called `ssd-monitor` that needs to run on all nodes that contain a solid-state drive (SSD). You’ll create a DaemonSet that runs this daemon on all nodes that are marked as having an SSD. The cluster administrators have added the `disk=ssd` label to all such nodes, so you’ll create the DaemonSet with a node selector that only selects nodes with that label,

![creating daemon sets](https://user-images.githubusercontent.com/24803604/71683593-9c3f7d80-2d58-11ea-94a0-ffc9c3cd4071.png)

You’ll create a DaemonSet that runs a mock ssd-monitor process, which prints "SSD OK" to the standard output every five seconds. I’ve already prepared the mock container image and pushed it to Docker Hub, so you can use it instead of building your own. 

You’re going to create a file called **ssd-monitor-daemonset.yaml** (you can create it in any directory you want), or copy from this repo, where you’ll find the file with filename [ssd-monitor-daemonset.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/ssd-monitor-daemonset.yaml). The following listing shows the entire contents of the file.

```yml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: ssd-monitor
spec:
  selector:
    matchLabels:
      app: ssd-monitor
  template:
    metadata:
      labels:
        app: ssd-monitor
    spec:
      nodeSelector:
        disk: ssd
      containers:
      - name: main
        image: knrt10/ssd-monitor
```

You’re defining a DaemonSet that will run a pod with a single container based on the `knrt10/ssd-monitor` container image. An instance of this pod will be created for each node that has the `disk=ssd` label.

#### Creating the DaemonSet

Use `kubectl create` command as you know.

`kubectl create -f ssd-monitor-daemonset.yaml`

Let’s see the created DaemonSet:

`kubectl get ds`

```bash
NAME          DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
ssd-monitor   0         0         0       0            0           disk=ssd        18s
```

Those zeroes look strange. Didn’t the DaemonSet deploy any pods? List the pods:

`kubectl get po`
> No resources found.

Where are the pods? Do you know what’s going on? Yes, you forgot to label your nodes with the disk=ssd label. No problem—you can do that now. The DaemonSet should detect that the nodes’ labels have changed and deploy the pod to all nodes with a matching label. Let’s see if that’s true. The DaemonSet should have created one pod now. Let’s see:

`kubectl label node minikube disk=ssd`

```bash
NAME                READY   STATUS    RESTARTS   AGE
ssd-monitor-zs6sr   1/1     Running   0          6s
```

Okay; so far so good. If you have multiple nodes and you add the same label to further nodes, you’ll see the DaemonSet spin up pods for each of them. Now, imagine you’ve made a mistake and have mislabeled one of the nodes. It has a spinning disk drive, not an SSD. What happens if you change the node’s label?

The pod is being terminated. But you knew that was going to happen, right? This wraps up your exploration of DaemonSets, so you may want to delete your ssd-monitor DaemonSet. If you still have any other daemon pods running, you’ll see that deleting the DaemonSet deletes those pods as well.

### Running Pod that perform a single completable task

So far, I have told about the pods that run continuously. We'll have cases that need to terminate once the task is completed. ReplicationContollers, RelicaSets, DaemonSets run continuously task that are never considered completed. Process in these tasks are restarted when they exit, but we do not want that. We want to stop once the process is completed. 

#### Introducing the Job resource

Kubernetes includes support for this through Job resource, which is similar to other resources we have discussed so far, but it allows you to run a pod whose container isn’t restarted when the process running inside finishes successfully. Once it does, the pod is considered complete.

In the event of node failure, pod on that node that are managed by the Job will be reschduled to other nodes the way ReplicaSets are. In the event of a failure of the process itself (when the process returns an error exit code), the Job can be configured to either restart the container or not.

As shown below, it tells how a pod created by a Job is rescheduled to a new node if the node it was initially scheduled to fails. It also shows both a managed pod, which isn’t rescheduled, and a pod backed by a ReplicaSet, which is.

For example, Jobs are useful for ad hoc tasks, where it’s crucial that the task finishes properly. You could run the task in an unmanaged pod and wait for it to finish, but in the event of a node failing or the pod being evicted from the node while it is performing its task, you’d need to manually recreate it. Doing this manually doesn’t make sense especially if the job takes hours to complete.

An example of such a job would be if you had data stored somewhere and you needed to transform and export it somewhere. You’re going to emulate this by running a container image built on top of the busybox image, which invokes the sleep command for two minutes. I’ve already built the image and pushed it to Docker Hub, but you can peek into its Dockerfile in the book’s code archive.

![Job resource](https://user-images.githubusercontent.com/24803604/72050330-e2f81f00-32e6-11ea-9bba-ec9603835138.png)

> Pods managed by Jobs are rescheduled until they finish successfully.

#### Defining a Job resource

Create the Job manifest as in the following listing. You’re going to create a file called **exporter.yaml** (you can create it in any directory you want), or copy from this repo, where you’ll find the file with filename [exporter.yaml](https://github.com/knrt10/kubernetes-basicLearning/blob/master/exporter.yaml). The following listing shows the entire contents of the file.

```yml
apiVersion: batch/v1
kind: Job
metadata:
  name: batch-job
spec:
  template:
    metadata:
      labels:
        app: batch-job
    spec:
      restartPolicy: OnFailure
      containers:
      - name: main
        image: knrt10/batch-job
```

Jobs are part of the `batch` API group and `v1 API` version. The YAML defines a resource of type Job that will run the `knrt10/batch-job` image, which invokes a process that runs for exactly 120 seconds and then exits. The image is already been pushed on dockerhub by me.

In a pod’s specification, you can specify what Kubernetes should do when the processes running in the container finish. This is done through the `restartPolicy` pod spec property, which defaults to `Always`. Job pods can’t use the default policy, because they’re not meant to run indefinitely. Therefore, you need to explicitly set the restart policy to either `OnFailure` or `Never`. This setting is what prevents the container from being restarted when it finishes (not the fact that the pod is being managed by a Job resource).

#### Seeing a Job run a pod

After you create this Job with the `kubectl create` command, you should see it start up
a pod immediately:

`kubectl get jobs`

```bash
NAME      DESIRED   SUCCESSFUL  AGE
batch-job 1         0           2s
```

## Todo

- [ ] Write more about pods
- [ ] Write about yaml files
- [ ] Write about ingress routing
- [ ] Write about volumes
- [ ] Write about config maps and secrets
- [ ] Write more on updating running pods
- [ ] Write about StatefulSets
- [ ] More on securing pods and containers
- [ ] Implement && write about GCP 
