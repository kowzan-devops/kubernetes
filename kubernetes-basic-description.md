# Kubernetes basics
## _Container orchestration tools_

![orchestration-tools.png](https://i.ibb.co/JRSbqQX/orchestration-tools.png)

![k8s-worker-nodes.png](https://i.ibb.co/VQ1LcZq/k8s-worker-nodes.png)

### Cluster overview

**Kubernetes Cluster**
- Group of physical or virtual servers wherein  Kubernetes is installed 
- Cluster is composed of Master node and Worker nodes.

Kubernetes uses Docker Host to host application, in the form of Docker containers

**Master node (Master):**
- Physical or virtual server that controls the Kubernetes cluster - has Control Plane component
- makes orchestration of containers on Worker nodes
- has information about members of the cluster, how nodes are monitored, where to direct workload when node fails

**Worker node (Worker):**
- Physical or virtual servers where workloads run in a given container technology 

![k8s-master-worker-nodes-cluster.png](https://i.ibb.co/K70QMSF/k8s-master-worker-nodes-cluster.png)

**API Server**
- frontend for Kubernetes (user's CLI commands, devices)

**etcd**
- distributed key-value store, which stores all data used to manage the cluster, like how many nodes, how many masters,
- implementing logs within the cluster, to ensure there are no conflicts between the masters

**Scheduler**
- responsible for distributing work or containters across multiple Nodes
- looks for newly created containers and assigns them to Nodes

**Controller(s)**
- are orchestration's brain, responsible for noticing and responding when nodes, containers or endpoints goes down
- bring up new containers

**Container runtime**
- underlying software that is used to run containers - here it is Docker

**Kubelet**
- agent that runs on each node (service that communicates with the master)
- responsible to check if containers are running on the nodes as expected

**kube-proxy = proxy for connecting to the cluster network**

### kubectl Example commands:

      kubectl cluster-info
      kubectl config view # view cluster and client configuration
      kubectl api-resources
      kubectl get nodes
      kubectl explain pods # explain = manual
      kubectl run hello-minikube
      kubectl attach mywebserver -c mynginx -i # connect to a running container
      kubectl exec mywebserver -- /home/user/myscript.sh # run a command in a single container pod
      kubectl run --replicas=10 my-web-app --image=my-web-app
      kubectl get pods --field-selector status.phase=Running
      kubectl get pods --field-selector=status.phase!=Running,spec.restartPolicy=Always

      #selects all Statefulsets and Services that are not in the default namespace
      kubectl get statefulsets,services --all-namespaces --field-selector metadata.namespace!=default 

      # Scale a resource
      kubectl scale --replicas=3 deployment.apps/my-web-server
      kubectl scale --replicas=3 -f my-manifest.yaml

      kubectl rolling-update my-web-server --image=web-server:2
      kubectl rolling-update my-web-server --rolback

      # Create a resource
      kubectl run <pod-name> --image=<image-name> --restart=Never -o yaml --dry-run > pod.yaml
      kubectl create -f ./my-manifest.yaml
      kubectl create deployment my-manifest --image=nginx

      # Delete a resource
      kubectl delete -f ./my-manifest.yaml
      kubectl delete deployment my-manifest


# List of Kubernetes objects

Kubernetes enables you to control and orchestrate various types of objects, either by their full name or their “shortname”.  These objects include:

### Workloads

- Container
> software package ready-to-run an application: the code and any runtime environment, settings and libraries
- CronJob / cronjobs / cj
> object that creates Jobs on a repeating schedule
- DaemonSet / daemonsets / ds
> A DaemonSet ensures that all (or some) Nodes run a copy of a Pod.  
> As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected.  
> Deleting a DaemonSet will clean up the Pods it created.
- Deployment / deployments / deploy
> object that manages a replicated application
> making sure to automatically replace any instances that fail or become unresponsive
- Job / jobs
> supervise a set of pods that run to complete process, that runs for a certain time, like calculation or a backup operation.
- Pod / pods / po
> The smallest object within the Kubernetes ecosystem  
> pod = container or containers + storage resources + unique IP + local options  
> Labels - User defined Key:Value pair associated to Pods  
- ReplicaSet / replicasets / rs
> object that ensures there is always a stable set of running pods for a specific workload
> if a pod is evicted or fails, creates more pods to compensate for the loss
- ReplicationController / replicationcontrollers / rc
> ensures that a specified number of pod replicas are running at any one time (up and running)
- StatefulSet / statefulsets / sts
> Like a Deployment, a StatefulSet manages Pods that are based on an identical container spec. Unlike a Deployment, a StatefulSet maintains a sticky identity for each of their Pods. These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling.
> What is a statefulset application?  
> Stateful applications save data to persistent disk storage for use by the server, by clients, and by other applications  
> An example of a stateful application is a database or key-value store to which data is saved and retrieved by other applications  
> Using StatefulSets  
> StatefulSets are valuable for applications that require one or more of the following.  
      Stable, unique network identifiers.
      Stable, persistent storage.
      Ordered, graceful deployment and scaling.
      Ordered, automated rolling updates.

### Services

- Endpoints / endpoints / ep
- EndpointSlice / endpointslices
- Ingress / ingresses / ing
- IngressClass / ingressclasses
- Service / services / svc
> An abstraction which serves as a proxy for a group of Pods, performing a “service”, it means that service makes sure that network traffic can be directed to the pods for the workload.
### Config & Storage

- ConfigMap / configmaps / cm
- CSIDriver / csidrivers
- CSINode / csinodes
- Secret / secrets
> Secrets let you store and manage sensitive information such as passwords, OAuth tokens, and ssh keys
- PersistentVolumeClaim / persistentvolumeclaims / pvc
- StorageClass / storageclasses / sc
- CSIStorageCapacity
- Volume
> sometimes-shared, persistent storage
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
> virtual cluster on top of an underlying physical cluster
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

#### Service(s)
An abstraction which serves as a proxy for a group of Pods, performing a “service”, it means that service makes sure that network traffic can be directed to the pods for the workload. Types of services:

- ClusterIP is the default ServiceType, ClusterIP services have a cluster-internal IP address, so they can only be reached by other cluster components.  
- NodePort enables you to create a service that’s available from outside the cluster by exposing the service on the same port for every node. For example, the same service might be available on host1.example.com:32768, host2.example.com:32768, and host3.example.com:32768.
- LoadBalancer requires coordination with your cloud provider’s load balancer, which automatically routes requests to the service. For this reason, not all distributions of Kubernetes will support LoadBalancer services. 
- ExternalName is the most complex ServiceType, coordinating the service with your DNS server.

Create a service that directs requests on port 80 to container port 8000 (simple LoadBalancer)
- kubectl expose deployment nginx --port=80 --target-port=8000 --type=LoadBalancer
- so if I write in Firefox IP_ADDRESS of POD (default 80) website will appear
#### Port forwarding:

kubectl port-forward podname PORT:TARGET_PORT
- port: the port receiving the request (on my PC)
- targetPort: the container's port receiving the request

#### Draining

> There may be scenarios where a faulty node has been identified and will need maintenance or to be decommissioned - what would be the safest way to evict all workloads to another node before removing the faulty node from service?  
> The drain command safely evicts all of your pods by terminating them gracefully, while only leaving node-critical workloads such as networking and logging components:  
> kubectl drain <node-name> --delete-local-data --ignore-daemonsets