# Kubernetes basics
## _Container orchestration tools_

![orchestration-tools.png](https://i.ibb.co/JRSbqQX/orchestration-tools.png)

![k8s-worker-nodes.png](https://i.ibb.co/VQ1LcZq/k8s-worker-nodes.png)

### Cluster overview

Kubernetes Cluster
- Group of physical or virtual servers wherein  Kubernetes is installed 
- Cluster is composed of Master node and Worker nodes.

Kubernetes uses Docker Host to host application, in the form of Docker containers

Master node (Master):
- Physical or virtual server that controls the Kubernetes cluster - has Control Plane component
- makes orchestration of containers on Worker nodes
- has information about members of the cluster, how nodes are monitored, where to direct workload when node fails

Worker node (Worker):
- Physical or virtual servers where workloads run in a given container technology 

![k8s-master-worker-nodes-cluster.png](https://i.ibb.co/K70QMSF/k8s-master-worker-nodes-cluster.png)

API Server
- frontend for Kubernetes (user's CLI commands, devices)

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

Pods
- Group of containers and volumes which share the  same network namespace 

Labels
- User defined Key:Value pair associated to Pods  

Master
- Control plane components which provide access  point for admins to manage cluster workloads 

Service
- An abstraction which serves as a proxy for a group of Pods performing a “service”

### kubectl Example commands:

   kubectl cluster-info
   kubectl get nodes
   kubectl run hello-minikube
   kubectl run --replicas=10 my-web-app --image=my-web-app

> kubectl scale --replicas=10 my-web-server
> 
> kubectl rolling-update my-web-server --image=web-server:2
> 
> kubectl rolling-update my-web-server --rolback 


# List of Kubernetes objects

Kubernetes enables you to control and orchestrate various types of objects, either by their full name or their “shortname”.  These objects include:

### Workloads

- Container
- CronJob / cronjobs / cj
- DaemonSet / daemonsets / ds
- Deployment / deployments / deploy
- Job / jobs
- Pod / pods / po
- ReplicaSet / replicasets / rs
- ReplicationController / replicationcontrollers / rc
- StatefulSet / statefulsets / sts

### Services

- Endpoints / endpoints / ep
- EndpointSlice / endpointslices
- Ingress / ingresses / ing
- IngressClass / ingressclasses
- Service / services / svc

### Config & Storage

- ConfigMap / configmaps / cm
- CSIDriver / csidrivers
- CSINode / csinodes
- Secret / secrets
- PersistentVolumeClaim / persistentvolumeclaims / pvc
- StorageClass / storageclasses / sc
- CSIStorageCapacity
- Volume
- VolumeAttachment / volumeattachments

### Clusters

- APIService / apiservices
- Binding / bindings
- CertificateSigningRequest / certificatesigningrequests / csr
- ClusterRole / clusterroles
- ClusterRoleBinding / clusterrolebindings
- ComponentStatus / componentstatuses/cs
- FlowSchema / flowschemas
- Lease / leases
- LocalSubjectAccessReview / localsubjectaccessreviews
- Namespace / namespaces/ns
- NetworkPolicy / networkpolicies / netpol
- Node / nodes / no
- PersistentVolume / persistentvolumes / pv
- PriorityLevelConfiguration / prioritylevelconfigurations
- ResourceQuota / resourcequotas / quota
- Role / roles
- RoleBinding / rolebindings
- RuntimeClass / runtimeclasses
- SelfSubjectAccessReview / selfsubjectaccessreviews
- SelfSubjectRulesReview / selfsubjectrulesreviews
- ServiceAccount / serviceaccounts / sa
- StorageVersion
- SubjectAccessReview / subjectaccessreviews
- TokenRequest
- TokenReview / tokenreviews

### Metadata

- ControllerRevision / controllerrevisions
- CustomResourceDefinition / customresourcedefinitions / crd,crds
- Event / events / ev
- LimitRange / limitranges / limits
- HorizontalPodAutoscaler / horizontalpodautoscalers / hpa
- MutatingWebhookConfiguration / mutatingwebhookconfigurations
- ValidatingWebhookConfiguration / validatingwebhookconfigurations
- PodTemplate / podtemplates
- PodDisruptionBudget / poddisruptionbudgets / pdb
- PriorityClass / priorityclasses / pc
- PodSecurityPolicy / podsecuritypolicies / psp
