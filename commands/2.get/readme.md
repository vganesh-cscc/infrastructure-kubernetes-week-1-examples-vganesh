

### `kubectl get`
`kubectl get` Lists one or more objects of a certain type.

**Command**
```
kubectl get <TYPE>
kubectl get <TYPE> <NAME>
kubectl get <TYPE> <NAME> <args>
```

**Examples**
```
$ kubectl get namespaces
NAME              STATUS   AGE
default           Active   132m
dev               Active   118s
kube-node-lease   Active   132m
kube-public       Active   132m
kube-system       Active   132m

$ kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
basic-pod   1/1     Running   0          87s

$ kubectl get pod basic-pod
NAME        READY   STATUS    RESTARTS   AGE
basic-pod   1/1     Running   0          107s

$ kubectl get pod basic-pod -o wide
NAME        READY   STATUS    RESTARTS   AGE    IP           NODE       NOMINATED NODE   READINESS GATES
basic-pod   1/1     Running   0          2m4s   172.18.0.4   minikube   <none>           <none>

```

## Ganesh notes 
cd 

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/2.get

$ cat basic-pod.yml
apiVersion: v1
kind: Pod
metadata:
name: vganesh
spec:
containers:
- name: nginx
  image: nginx:stable-alpine
  ports:
    - containerPort: 80/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/2.get

pod/vganesh created

$ kubectl get namespaces

NAME              STATUS   AGE
default           Active   12h
kube-node-lease   Active   12h
kube-public       Active   12h
kube-system       Active   12h

$ kubectl get pods

NAME      READY   STATUS    RESTARTS   AGE
vganesh   1/1     Running   0          5m58s

$ kubectl get pod vganesh

NAME      READY   STATUS    RESTARTS   AGE
vganesh   1/1     Running   0          6m11s
/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/2.get

$ kubectl get pod vganesh -o wide

NAME      READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
vganesh   1/1     Running   0          6m29s   10.244.0.4   minikube   <none>           <none>



