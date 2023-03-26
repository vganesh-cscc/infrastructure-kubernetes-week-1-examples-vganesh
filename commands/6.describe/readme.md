
### `kubectl describe`
`kubectl describe` lists information about the specific object.
**Command**
```
kubectl describe <TYPE>
kubectl describe <TYPE> <NAME>
```

**Examples**
```
$ kubectl describe pod basic-pod
Name:         basic-pod
Namespace:    default
Priority:     0
Node:         minikube/172.17.0.3
Start Time:   Tue, 14 Jul 2020 22:20:28 -0400
Labels:       <none>
Annotations:  Status:  Running
IP:           172.18.0.4
IPs:
  IP:  172.18.0.4
Containers:
  nginx:
    Container ID:   docker://7fb050f8ec78d7fe3994472b2f385c05b3dece96be6771b90c69592dedff6a90
    Image:          nginx:stable-alpine
    Image ID:       docker-pullable://nginx@sha256:29dc24ed982665eb88598e0129e4ec88c2049fafc63125a4a640dd67529dc6d4
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Tue, 14 Jul 2020 22:20:29 -0400
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-hj99j (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  default-token-hj99j:
    Type:        Secret (a volume populated by a Secret)
    SecretName:  default-token-hj99j
    Optional:    false
QoS Class:       BestEffort
Node-Selectors:  <none>
Tolerations:     node.kubernetes.io/not-ready:NoExecute for 300s
                 node.kubernetes.io/unreachable:NoExecute for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  7m32s  default-scheduler  Successfully assigned default/basic-pod to minikube
  Normal  Pulled     7m31s  kubelet, minikube  Container image "nginx:stable-alpine" already present on machine
  Normal  Created    7m31s  kubelet, minikube  Created container nginx
  Normal  Started    7m31s  kubelet, minikube  Started container nginx

  ```

## Ganesh notes 



$ **kubectl describe --help** 

Show details of a specific resource or group of resources.

**kubectl describe TYPE NAME_PREFIX**

Valid values for **TYPE** are resources like pods, deployments and many more listed below. 

Use "kubectl api-resources" for a complete list of supported resources.

Example resources are namespaces, nodes, pods, secrets, services, deployments, replicasets, cronjobs, jobs, ingresses, roles, storageclasses and volumeattachments to name a few. 

There are about 55 resources listed when I run the command below. 

$ **kubectl api-resources | wc -l**

56


What is a **namespace** in Kubernetes?

**Namespaces** are a way to organize clusters — they can be helpful when different teams share a Kubernetes cluster. Any number of namespaces are supported within a cluster, each logically separated from others but with the ability to communicate with each other.

https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/

Names of resources need to be unique within a namespace. 

Namespace-based scoping is applicable only for namespaced objects (e.g. Deployments, Services, etc) and not for cluster-wide objects (e.g. StorageClass, Nodes, PersistentVolumes, etc)


Q: What does it mean if a namespace is going to communicate with another namespace? When does it happen? Examples??? 



What is a Kubernetes **cluster**  ? 

A Kubernetes **cluster** is a set of nodes that run containerized applications. Cluster is a bunch of machines. 


https://www.vmware.com/topics/glossary/content/kubernetes-cluster.html#:~:text=What%20is%20a%20Kubernetes%20cluster,and%20flexible%20than%20virtual%20machines.


https://kubernetes.io/docs/concepts/architecture/nodes/

A **node** may be a virtual or physical machine. 


$ **kubectl get nodes**

NAME       STATUS   ROLES           AGE   VERSION

minikube   Ready    control-plane   16h   v1.26.1


In this example think of minikube to be the CentOS VM where minikube software was installed. 

When minikube was installed on CentOS VM, the following file is created. The name of the cluster in the config file is minikube, a single node cluster. 

**ls -ltr   ~/.kube/config**

-rw-------. 1 vganesh docker 932 Mar 25 22:10 /home/CSCC/vganesh/.kube/config

$ **grep cluster ~/.kube/config**
clusters:
- cluster:
  name: cluster_info
  cluster: minikube
  cluster: minikube



At my work place, the environment variable KUBECONFIG points to a test configuration yaml file that was created for test purpose. 

The name of the cluster is **test011** and it has about twenty nodes, meaning twenty different machines with different ip addresses. These nodes are running on AWS cloud environment. 

C:\Users\ganesv2

**set | findstr yaml**

KUBECONFIG=C:\Users\ganesv2\.kube\config_test.yaml


$ **kubectl get nodes | wc -l**
21


C:\Users\ganesv2

**findstr cluster .kube\config_test.yaml**

clusters:
  cluster: docker-desktop
  cluster: test011
  cluster: test011-fqdn

C:\Users\ganesv2

