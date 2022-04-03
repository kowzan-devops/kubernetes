# Kubernetes basics
## _Container orchestration tools_

![orchestration-tools.png](https://i.ibb.co/JRSbqQX/orchestration-tools.png)

### Example commands:

> kubectl scale --replicas=10 my-web-server
> 
> kubectl run --replicas=10 my-web-server
> 
> kubectl rolling-update my-web-server --image=web-server:2
> 
> kubectl rolling-update my-web-server --rolback 

![k8s-worker-nodes.png](https://i.ibb.co/VQ1LcZq/k8s-worker-nodes.png)

### Cluster overview

Kubernetes Cluster is composed of Master node and Worker nodes.
Kubernetes uses Docker Host to host application, in the form of Docker containers

Node is phisical machine. 

Master node:
- manage the Cluster - has Control Plane component => makes orchestration of containers on worker nodes
- has information about members of the cluster, how nodes are monitored, where to direct workload when node fails

![k8s-master-worker-nodes-cluster.png](https://i.ibb.co/K70QMSF/k8s-master-worker-nodes-cluster.png)

