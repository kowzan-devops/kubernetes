# Kubernetes basics
## _Container orchestration tools_

![orchestration-tools.png](https://i.ibb.co/JRSbqQX/orchestration-tools.png)

![k8s-worker-nodes.png](https://i.ibb.co/VQ1LcZq/k8s-worker-nodes.png)

### Cluster overview

Kubernetes Cluster is composed of Master node and Worker nodes.
Kubernetes uses Docker Host to host application, in the form of Docker containers

Node is phisical machine. 

Master node:
- manage the Cluster - has Control Plane component => makes orchestration of containers on Worker nodes
- has information about members of the cluster, how nodes are monitored, where to direct workload when node fails

![k8s-master-worker-nodes-cluster.png](https://i.ibb.co/K70QMSF/k8s-master-worker-nodes-cluster.png)

API Server - frontend for Kubernetes (user's CLI commands, devices)

etcd
- distributed key-value store, which stores all data used to manage the cluster, like how many nodes, how many masters,
- implementing logs within the cluster, to ensure there are no conflicts between the masters

Scheduler
- responsible for distributing work or containters across multiple Nodes
- looks for newly created containers and assigns them to Nodes

Controller(s)
- are orchestration's brain, responsible for noticing and responding when nodes, containers or endpoints goes down
- bring up new containers

Container runtime
- underlying software that is used to run containers - here it is Docker

Kubelet
- agent that runs on each node
- responsible to check if containers are running on the nodes as expected

### kubectl Example commands:

      kubectl cluster-info
      kubectl run hello-minikube


> kubectl scale --replicas=10 my-web-server
> 
> kubectl run --replicas=10 my-web-server
> 
> kubectl rolling-update my-web-server --image=web-server:2
> 
> kubectl rolling-update my-web-server --rolback 

