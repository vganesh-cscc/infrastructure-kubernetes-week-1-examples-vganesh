
### `kubectl edit`
`kubectl edit` allows for in place modification with your text editor without having to apply. 

This command is useful for debugging, and **should not** be used in production since changes made are not tracked like `apply`.

**Command**
```
$ kubectl edit <TYPE> <NAME>
```

**Examples**
```
$ kubectl edit pod basic-pod

# Please edit the object below. Lines beginning with a '#' will be ignored,
# and an empty file will abort the edit. If an error occurs while saving this file will be
# reopened with the relevant failures.
#
apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"name":"basic-pod","namespace":"default"},"spec":{"containers":[{"image":"nginx:stable-alpine","name":"nginx","ports":[{"containerPort":80}]}]}}
  creationTimestamp: "2020-07-15T02:20:28Z"
  managedFields:
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:metadata:
        f:annotations:
          .: {}
          f:kubectl.kubernetes.io/last-applied-configuration: {}
      f:spec:
        f:containers:
          k:{"name":"nginx"}:
            .: {}
            f:image: {}
            f:imagePullPolicy: {}
            f:name: {}
            f:ports:
              .: {}
              k:{"containerPort":80,"protocol":"TCP"}:
                .: {}
                f:containerPort: {}
                f:protocol: {}
            f:resources: {}
            f:terminationMessagePath: {}
            f:terminationMessagePolicy: {}
        f:dnsPolicy: {}
        f:enableServiceLinks: {}
        f:restartPolicy: {}
        f:schedulerName: {}
        f:securityContext: {}
        f:terminationGracePeriodSeconds: {}
    manager: kubectl
    operation: Update
    time: "2020-07-15T02:20:28Z"
  - apiVersion: v1
    fieldsType: FieldsV1
    fieldsV1:
      f:status:
   
   .... omitted for brevity
```


## Ganesh notes 

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/5.edit

$ **ls -ltra**

total 4

-rw-r--r--.  1 vganesh domain users 1945 Mar 25 21:48 readme.md

drwxr-xr-x.  2 vganesh domain users   23 Mar 25 21:48 .

drwxr-xr-x. 10 vganesh domain users  127 Mar 25 21:48 ..


$ **kubectl get pods**

NAME                        READY   STATUS    RESTARTS   AGE
my-nginx-85996f8dbd-4qdhj   1/1     Running   0          18m
my-nginx-85996f8dbd-cfnj8   1/1     Running   0          18m
my-nginx-85996f8dbd-j4t7d   1/1     Running   0          18m
vganesh                     1/1     Running   0          31m

Not able to change the name of the pod from vganesh to vramesh. The command failed with an error: name was changed. 

It looks like only certain fields in that deployment are malleable??? 

$ **kubectl edit pod vganesh**

A copy of your changes has been stored to "/tmp/kubectl-edit-2662882958.yaml"
error: At least one of apiVersion, kind and **name was changed**


TODO: Find out the fields folks change in a deployment for all practical purpose, during testing ??? Maybe the port number? 



$ **kubectl get deployments**

NAME       READY   UP-TO-DATE   AVAILABLE   AGE

my-nginx   3/3     3            3           174m


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
Normal  ScalingReplicaSet  33m   deployment-controller  Scaled up replica set my-nginx-85996f8dbd to 3


TODO: Find out the fields in a pod like vganesh that can be edited during testing??? 



$ **kubectl describe pod vganesh**  

Name:             vganesh
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Sun, 26 Mar 2023 11:30:35 -0400
Labels:           <none>
Annotations:      <none>
Status:           Running
IP:               10.244.0.5
IPs:
IP:  10.244.0.5
Containers:
nginx:
Container ID:   docker://8d431a952469df6e5c1b535296df7f4bbd514a6c086f5156d9ca29db07e1aeee
Image:          nginx:stable-alpine
Image ID:       docker-pullable://nginx@sha256:a9e4fce28ad7cc7de45772686a22dbeaeeb54758b16f25bf8f64ce33f3bff636
Port:           80/TCP
Host Port:      0/TCP
State:          Running
Started:      Sun, 26 Mar 2023 11:30:36 -0400
Ready:          True
Restart Count:  0
Environment:    <none>
Mounts:
/var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-8vcgh (ro)
Conditions:
Type              Status
Initialized       True
Ready             True
ContainersReady   True
PodScheduled      True
Volumes:
kube-api-access-8vcgh:
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
Normal  Scheduled  49m   default-scheduler  Successfully assigned default/vganesh to minikube
Normal  Pulled     49m   kubelet            Container image "nginx:stable-alpine" already present on machine
Normal  Created    49m   kubelet            Created container nginx
Normal  Started    49m   kubelet            Started container nginx


