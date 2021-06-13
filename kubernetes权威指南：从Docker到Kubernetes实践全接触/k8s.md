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


