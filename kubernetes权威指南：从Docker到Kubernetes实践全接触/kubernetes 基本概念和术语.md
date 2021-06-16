# kubernetes 基本概念和术语

## k8s指令  

kubectl create -f mysql-rc.yaml  
kubectl create -f mysql-svc.yaml  
kubectl create -f myweb-rc.yaml  
kubectl create -f myweb-svc.yaml  

kubectl get rc  
kubectl get pods  
kubectl get svc  
kubectl get service  
kubectl get nodes  
> 查看集群中多少个node  

kubectl get delplyments  
> 查看Deployment信息

kubectl describe node<node_name>
> 查看某个node详细信息  

kubectl scale rc redis-slave --replicas=3
> 修改rc的副本数量，实现pod动态缩放

kubectl get rs
> 查看对应Replica Set

kubectl get pods
> 查看创建的pod

kubectl describe deployments
> 查看Deployment控制的pod的水平扩展过程

kubectl get endpoints

kubectl get svc tomcat-service -o yaml
> 查看yaml文件

kubectl get namespace  
kubectl get pods --namespace=development

## 配置文件说明

![avatar](./img/replicationController.png)
![avatar](./img/service.png)

## k8s组件  

### master  

+ Kubernetes API Server(kube-apiserver)

> 提供HTTP Rest接口的关键服务进程，集群控制入口

+ Kubernetes Controller Manager(kube-controller-manager)

> 资源对象自动化控制中心

+ Kubernetes Scheduler(kube-scheduler)

> 负责资源调度（Pod调度）的进程

+ etcd Server

> 所有资源对象持久化保存在etcd中

### Node  

+ kubelet  

> 负责Pod对应容器创建，启停，和master合作实现集群管理

+ kube-proxy

> 实现 Kubernetes Service通信与负载均衡机制的组件

+ Docker Engine (docker)

> docker 引擎，负责本机容器创建和管理

### Pod  

+ 每个Pod都有一个特殊的被称为“根容器”的Pause容器，还包含一个或者多个紧密相关的用户业务容器  

+ endpoint (Pod ip + container port)

### Label

### Replication Controller  

### Deployment  

### Horizontal Pod Autoscaler(HPA)  

### Service

![avatar](./img/1_4_8_service.png)
> node ip  
集群中每个几点的物理网卡的IP地址，真实存在的物理网络，外部通信  
pod ip  
每个pod的ip地址，虚拟的二层网络，用于内部pod相互访问  
cluster ip  
虚拟的IP，仅用于service这个对象，无法被ping，只能结合port组成一个通信端口，用于kubernetes 集群内部地址。

![avatar](./img/service_proxy.png)
> 多个kubernetes负载均衡可以使用Load balancer 或者 HAProxy Nginx实现。

### Volume  

> Volume 是pod中能够被多个容器访问的目录，定义在pod上，被一个Pod里的多个容器挂在到具体文件目录下，生命周期与pod相同，和容器生命周期不相关。  

+ emptyDir  
+ hostPath
+ gcePersistentDisk
+ awsElasticBlockStore
+ NFS
+ 其他 (flocker,glusterfs,rbd,gitRepo,secret)

### Persistent Volume

+ PV只能是网络存储，不属于Node，但是可以访问
+ PV不定义在pod上，独立于pod  
+ PV 目前只有几种类型： GCE Persistent Disks、 NFS、 RBD、 iSCSCI、 AWS ElasticBlockStore、 GlusterFS  

> PV 的状态

+ Available：空闲状态。
+ Bound：已经绑定到某个PVC上。
+ Released：对应的PVC已经删除，资源还没有被集群收回。
+ Failed：PV自动回收失败。

### Namespace(命名空间)  

namespace 实现多租户的资源隔离，结合kubernetes的资源配额管理，限定不同的租户能占用的资源，cpu使用量，内存使用量  

### Annotation  

Annotation与Label 类似，也使用 key/ value 键值对的形式进行定义。 不同的是Label具有严格的命名规则，它定义的是 Kubernetes 对象的元数据（ Metadata）， 并且用于Label Selector。 而Annotation则是用户任意定义 的“ 附加” 信息， 以便于外部工具进行查找， 很多时候，Kubernetes的模块自身会通过Annotation 的方式标记资源对象的一些特殊信息。
