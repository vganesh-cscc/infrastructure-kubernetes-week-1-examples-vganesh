
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

cd /home/CSCC/vganesh/IdeaProjects/vganesh-cscc-week04-infra-kube-part01/2 - pods


$ **kubectl describe --help** 

Show details of a specific resource or group of resources.

**kubectl describe TYPE NAME_PREFIX**

Valid values for **TYPE** are resources like pods, deployments and many more listed below. _A brief explanation of resources follows._ 

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


**Q:** What does it mean if a namespace is going to communicate with another namespace? When does it happen? Examples??? 

What is a Kubernetes **cluster**  ? 

A Kubernetes **cluster** is a set of nodes that run containerized applications. A cluster is a bunch of machines. With minikube, it is single node and so only one machine, for example it is the CentOS VM machine created in a cloud environment. 

https://www.vmware.com/topics/glossary/content/kubernetes-cluster.html#:~:text=What%20is%20a%20Kubernetes%20cluster,and%20flexible%20than%20virtual%20machines.


https://kubernetes.io/docs/concepts/architecture/nodes/

A **node** may be a virtual or physical machine. 


$ **kubectl get nodes**

NAME       STATUS   ROLES           AGE   VERSION

**minikube**   Ready    control-plane   16h   v1.26.1


In this example think of minikube node to be the CentOS VM where minikube software was installed. 

When minikube was installed on CentOS VM, the following file is created. The name of the cluster in the config file is minikube, a single node cluster. 

**ls -ltr   ~/.kube/config**

-rw-------. 1 vganesh docker 932 Mar 25 22:10 /home/CSCC/vganesh/.kube/config

$ **grep cluster ~/.kube/config**
```aidl
clusters:
- cluster:
  name: cluster_info
  cluster: minikube
  cluster: minikube
```

At my work place, the environment variable **KUBECONFIG** points to a test configuration yaml file that was created for test purpose. 

The name of the cluster is **test011** and it has about twenty nodes, meaning twenty different machines with different ip addresses. These nodes are running on AWS cloud environment. 

C:\Users\ganesv2

**set | findstr yaml**

KUBECONFIG=C:\Users\ganesv2\.kube\config_test.yaml


$ **kubectl get nodes | wc -l**

21

C:\Users\ganesv2

**kubectl get nodes**
```aidl
NAME                                          STATUS   ROLES               AGE     VERSION
ip-10-XXX-52-KKK.us-east-2.compute.internal   Ready    worker              48d     v1.24.9
ip-10-XXX-53-YYY.us-east-2.compute.internal   Ready    worker              6d18h   v1.24.9
...

```


C:\Users\ganesv2

**findstr cluster .kube\config_test.yaml**
```aidl
clusters:
  cluster: docker-desktop
  cluster: test011
  cluster: test011-fqdn

```


**Pods** - https://kubernetes.io/docs/concepts/workloads/pods/ 

**Pods** are the smallest deployable units of computing that you can create and manage in Kubernetes. A pod is a one or more containers, with shared storage and network resources, and a specification for how to run the containers.

These are docker containers. 

https://kubernetes.io/docs/concepts/workloads/pods/ephemeral-containers/  

Pods are the fundamental building block of Kubernetes applications. Since Pods are intended to be disposable and replaceable, you cannot add a container to a Pod once it has been created. Instead, you usually delete and replace Pods in a controlled fashion using deployments.

Sometimes it's necessary to inspect the state of an existing Pod, however, for example to troubleshoot a hard-to-reproduce bug. In these cases you can run an ephemeral container in an existing Pod to inspect its state and run arbitrary commands

**Ephemeral containers** are useful for interactive troubleshooting when kubectl exec is insufficient because a container has crashed or a container image doesn't include debugging utilities.

Examples for Ephemeral containers ??




https://kubernetes.io/docs/concepts/configuration/secret/ 


A **Secret** is an object that contains a small amount of sensitive data such as a password, a token, or a key. 

Because Secrets can be created independently of the Pods that use them, there is less risk of the Secret (and its data) being exposed during the workflow of creating, viewing, and editing Pods. Kubernetes, and applications that run in your cluster, can also take additional precautions with Secrets, such as avoiding writing secret data to nonvolatile storage.

Secrets are similar to ConfigMaps but are specifically intended to hold confidential data.

How to create secrets and use it in a pod is explained here - https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/#define-container-environment-variables-using-secret-data 

$ **kubectl get secrets**

No resources found in default namespace.


C:\Users\ganesv2

**kubectl get secrets -n mac-cpp**

Thirty nine secrets are listed by the above command. 

**kubectl describe secret <SECRET-NAME>  -n mac-cpp**
```aidl
Name:         stix-properties-dev
Namespace:    mac-cpp
Labels:       <none>
Annotations:  kubernetes.io/change-cause: kubectl apply --kubeconfig=config --filename=manifests.yaml --record=true

Type:  Opaque

Data
====

environment.properties:  8921 bytes
log4j.properties:        1833 bytes
log4j2.xml:              913 bytes

```

These three files are stored as a part of the secret and are available in the classpath when the java app runs. 

Error from server (Forbidden): secrets is forbidden: User "u-5atut5g647" cannot list resource "secrets" in API group "" in the namespace "default"

I can go to vault site inside Nationwide network and see the secrets accessible to me and my team members. 

A Kubernetes **service** is a logical abstraction for a deployed group of pods in a cluster (which all perform the same function). Since pods are ephemeral, a service enables a group of pods, which provide specific functions (web services, image processing, etc.) to be assigned a name and unique IP address (clusterIP).


$ **kubectl get services**
```aidl
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   17h

```


**TODO**: Find ways to do services related CRUD activities. 

At my work place. 

C:\Users\ganesv2

**kubectl get services -n mac-cpp**

There are seventeen services listed. 

**kubectl describe service <SERVICE-NAME> -n mac-cpp**


I can login to rancher web site inside Nationwide and see the services https://<rancher-dashboard-url>/c/c-v5zwm/explorer/service 

When I look at Service: dev-stix-consumer-search , an app I am working on, it has following items. 

1. Pods - more than one pod can appear here, since a service is a collection of related pods. 
2. Ports - 
3. Selectors - has key and value. app.kubernetes.io/name  == gangplank , What is gangplank? 
4. Conditions 
5. Related resources - 

A Kubernetes **Deployment** tells Kubernetes how to create or modify instances of the pods that hold a containerized application.

https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

A Deployment provides declarative updates for Pods and **ReplicaSets**. 

A ReplicaSet's purpose is to maintain a stable set of replica Pods running at any given time. As such, it is often used to guarantee the availability of a specified number of identical Pods

$ **kubectl get deployments**

NAME       READY   UP-TO-DATE   AVAILABLE   AGE

**my-nginx**   3/3     3            3           4h29m


Create the Deployment by running the following command:

kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml



$ **kubectl get rs**
```aidl
NAME                  DESIRED   CURRENT   READY   AGE
my-nginx-85996f8dbd   3         3         3       4h32m
```

$ **kubectl get rs -n mac-cpp | wc -l**

142


/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/6.describe

There are three nginx pods running. 

$ **kubectl get pods**
```aidl
NAME                        READY   STATUS    RESTARTS   AGE
my-nginx-85996f8dbd-4qdhj   1/1     Running   0          4h38m
my-nginx-85996f8dbd-cfnj8   1/1     Running   0          4h38m
my-nginx-85996f8dbd-j4t7d   1/1     Running   0          4h38m
vganesh                     1/1     Running   0          4h51m
```


There is one nginx replica set available. Maybe this rs will be used if one the pod crashes? 

$ **kubectl get rs**
```aidl
NAME                  DESIRED   CURRENT   READY   AGE
my-nginx-85996f8dbd   3         3         3       4h38m
```

https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/

**CronJob** is meant for performing regular scheduled actions such as backups, report generation, and so on.
There are no differences between cronjob and a job. Cronsjobs are jobs scheduled to run regularly at a specified interval.

**kubectl get cronjobs -n mac-cpp**
```aidl
NAME                   SCHEDULE       SUSPEND   ACTIVE   LAST SCHEDULE   AGE
dev-piixe-reporting    13 22 31 2 *   True      0        <none>          5d22h
test-piixe-reporting   13 22 31 2 *   True      0        <none>          5d22h
```

**TODO:** Get crud commands cronjob related, as well how to see the cronjob log files? Can you see the cronjob log file five minutes after the cronjon has completed? Is that possible? 

A **CronJob** creates Jobs on a repeating schedule. CronJob is meant for performing regular scheduled actions such as backups, report generation, and so on. One CronJob object is like one line of a crontab (cron table) file on a Unix system. It runs a job periodically on a given schedule, written in Cron format.

**Jobs** are useful when you want to run a one-time task, or when you want to run a task multiple times until it succeeds, with a specified number of retries. 

Use Jobs and CronJobs to control and manage Kubernetes pods and containers.

https://opensource.com/article/20/11/kubernetes-jobs-cronjobs

The **Ingress** concept lets you map traffic to different backends based on rules you define via the Kubernetes API. An API object that manages external access to the services in a cluster, typically HTTP. Ingress may provide load balancing, SSL termination and name-based virtual hosting.



ganesv2@NW258455 MINGW64 ~

$ **kubectl get ing -n mac-cpp | wc -l**

17



**kubectl get ing -n mac-cpp | findstr dev-stix**

dev-stix-consumer-search

**kubectl describe ing <NAME-ING>  -n mac-cpp**


The output of the above command says if I go to a host listed in the command output, that host is mapped to consumer search app pod. 


/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/6.describe

$ **kubectl get ing**

No resources found in default namespace.

At my work place, 


**kubectl get roles -n mac-cpp**
```aidl
NAME                      CREATED AT
gangplank-fluent          2021-10-08T13:51:21Z
nginx-node-chart-fluent   2021-10-08T13:44:11Z
```


In Kubernetes, ClusterRoles and **Roles** define the actions a user can perform within a cluster or namespace, respectively. You can assign these roles to Kubernetes subjects (users, groups, or service accounts) with role bindings and cluster role bindings.


A **StorageClass** provides a way for administrators to describe the "classes" of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by the cluster administrators. Kubernetes itself is unopinionated about what classes represent.

**Persistent Volume** — low level representation of a storage volume. Persistent Volume Claim — binding between a Pod and Persistent Volume. Storage Class — allows for dynamic provisioning of Persistent Volumes.


https://medium.com/devops-mojo/kubernetes-storage-options-overview-persistent-volumes-pv-claims-pvc-and-storageclass-sc-k8s-storage-df71ca0fccc3#:~:text=Persistent%20Volume%20%E2%80%94%20low%20level%20representation,dynamic%20provisioning%20of%20Persistent%20Volumes.

1. **Persistent Volume** — low level representation of a storage volume.
2. **Persistent Volume Claim** — binding between a Pod and Persistent Volume.
3. **Storage Class** — allows for dynamic provisioning of Persistent Volumes.

