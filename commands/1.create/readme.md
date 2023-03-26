### `kubectl create`
`kubectl create` creates an object from the cli or with a path to a manifest using the `-f` or  `--filename` flag that can point to either a manifest file, or a directory that has multiple

**Command**
```
kubectl create <TYPE> <args>
kubectl create -f <path>
```

**Examples**
```
$ kubectl create namespace dev
namespace/dev created

kubectl create -f manifests/basic-pod.yaml 
pod/basic-pod created
```

### Ganesh notes 

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh
$ **minikube start**

$ **minikube status**

minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/1.create
$ **ls**

basic-pod.yml  readme.md

$ **kubectl create -f basic-pod.yml**

pod/basic-pod created

$ **kubectl get pods --all-namespaces**

NAMESPACE     NAME                               READY   STATUS    RESTARTS   AGE
default       basic-pod                          1/1     Running   0          28s
kube-system   coredns-787d4945fb-5xxqm           1/1     Running   0          22m
kube-system   etcd-minikube                      1/1     Running   0          22m
kube-system   kube-apiserver-minikube            1/1     Running   0          22m
kube-system   kube-controller-manager-minikube   1/1     Running   0          22m
kube-system   kube-proxy-gf6vm                   1/1     Running   0          22m
kube-system   kube-scheduler-minikube            1/1     Running   0          22m
kube-system   storage-provisioner                1/1     Running   0          22m



$ **kubectl describe pod basic-pod**

Name:             basic-pod
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Sat, 25 Mar 2023 22:32:26 -0400
Labels:           <none>
Annotations:      <none>
Status:           Running
IP:               10.244.0.3
IPs:
IP:  10.244.0.3
Containers:
nginx:
Container ID:   docker://15ba81a958d588de0958408d9cc7ff248f7ffe9b08ccd696bf8b699111f8489f
Image:          nginx:stable-alpine
Image ID:       docker-pullable://nginx@sha256:a9e4fce28ad7cc7de45772686a22dbeaeeb54758b16f25bf8f64ce33f3bff636
Port:           80/TCP
Host Port:      0/TCP
State:          Running
Started:      Sat, 25 Mar 2023 22:32:30 -0400
Ready:          True
Restart Count:  0
Environment:    <none>
Mounts:
/var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-bnvwp (ro)
Conditions:
Type              Status
Initialized       True
Ready             True
ContainersReady   True
PodScheduled      True
Volumes:
kube-api-access-bnvwp:
Type:                    Projected (a volume that contains injected data from multiple sources)
TokenExpirationSeconds:  3607
ConfigMapName:           kube-root-ca.crt
ConfigMapOptional:       <nil>
DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:

Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------

Normal  Scheduled  70s   default-scheduler  Successfully assigned default/basic-pod to minikube
Normal  Pulling    69s   kubelet            Pulling image "nginx:stable-alpine"
Normal  Pulled     67s   kubelet            Successfully pulled image "nginx:stable-alpine" in 1.860339838s (1.860352352s including waiting)
Normal  Created    67s   kubelet            Created container nginx
Normal  Started    66s   kubelet            Started container nginx

$ **kubectl delete pod basic-pod**

pod "basic-pod" deleted

$ **kubectl describe pod basic-pod**

Error from server (NotFound): pods "basic-pod" not found



