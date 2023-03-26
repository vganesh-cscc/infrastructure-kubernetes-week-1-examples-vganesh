
### `kubectl delete`
`kubectl delete` this command deletes the object.

**Command**
```
kubectl delete <TYPE> <NAME>
```

**Examples**
```
$ kubectl delete pod basic-pod
pod "basic-pod" deleted
```

## Ganesh notes 

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/3.delete

$ **kubectl get pods**

NAME      READY   STATUS    RESTARTS   AGE

vganesh   1/1     Running   0          9m10s

$ **kubectl delete  pod vganesh**

pod "vganesh" deleted


$ **kubectl get pods**

No resources found in default namespace.

