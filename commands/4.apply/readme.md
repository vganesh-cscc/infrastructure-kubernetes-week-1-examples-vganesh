
### `kubectl apply`

`kubectl apply` is like `kubectl create`. It will create the resource if it does not exist of update the resource if it is already created.

It is similar to `kubectl create` and takes a `-f` path to the manifest or reads in the config from the cli's stdin.

**Command**
```
kubectl apply -f <path>
```

**Notes**

When objects are created in kubernetes we learned that its state/config is stored within kubernetes. When you update a resource, it will store the previous version of it in an `annotation`.

`kubectl apply` behavior ff the object was not created initially with `apply` will act as a diff between the two. If you use apply on an object created via `create` you will get warning.

```
kubectl apply -f manifests/basic-pod.yaml 
Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply
pod/basic-pod configured
```

[kubectl apply documentation](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#kubectl-apply)


**Examples**
```
$ kubectl apply -f manifests/basic-pod.yaml 
pod/basic-pod created
```

## Ganesh notes 

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/4.apply

$ **kubectl get pods**

No resources found in default namespace.

$ **cat basic-pod.yml**

apiVersion: v1
kind: Pod
metadata:
name: **vganesh**
spec:
containers:
- name: nginx
  image: nginx:stable-alpine
  ports:
    - containerPort: 80
      

$ **kubectl apply -f basic-pod.yml**

pod/vganesh created

apply command reference https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#kubectl-apply



$ **kubectl get deployment**
No resources found in default namespace.


$ **kubectl apply -f https://k8s.io/examples/application/nginx/nginx-deployment.yaml**

deployment.apps/my-nginx created

$ **kubectl get deployments**

NAME       READY   UP-TO-DATE   AVAILABLE   AGE

**my-nginx**   3/3     3            3           17s

$ **kubectl describe  deployment my-nginx**

Name:                   my-nginx
Namespace:              default
CreationTimestamp:      Sun, 26 Mar 2023 11:43:48 -0400
Labels:                 <none>
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=nginx
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
Labels:  app=nginx
Containers:
nginx:
Image:        nginx:1.14.2
Port:         80/TCP
Host Port:    0/TCP
Environment:  <none>
Mounts:       <none>
Volumes:        <none>
Conditions:
Type           Status  Reason
  ----           ------  ------
Available      True    MinimumReplicasAvailable
Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   my-nginx-85996f8dbd (3/3 replicas created)
Events:
Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
Normal  ScalingReplicaSet  40s   deployment-controller  Scaled up replica set my-nginx-85996f8dbd to 3



