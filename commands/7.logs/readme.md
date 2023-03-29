
### `kubectl logs`
`kubectl logs` outputs `stdout` and `stderr` logs from a pod. If more than one container exists use the `-c` flag with the container name.

**Command**
```
kubectl logs <NAME>
kubectl logs <NAME> -c <container-name>
```

**Examples**
```
$ kubectl logs basic-pod
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Configuration complete; ready for start up

```

## Ganesh notes 

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh/commands/7.logs

$ **kubectl get pods -A**
```aidl
NAMESPACE     NAME                               READY   STATUS    RESTARTS      AGE
default       my-nginx-85996f8dbd-4qdhj          1/1     Running   0             9h
default       my-nginx-85996f8dbd-cfnj8          1/1     Running   0             9h
default       my-nginx-85996f8dbd-j4t7d          1/1     Running   0             9h
default       vganesh                            1/1     Running   0             9h
kube-system   coredns-787d4945fb-5xxqm           1/1     Running   0             22h
kube-system   etcd-minikube                      1/1     Running   0             22h
kube-system   kube-apiserver-minikube            1/1     Running   0             22h
kube-system   kube-controller-manager-minikube   1/1     Running   0             22h
kube-system   kube-proxy-gf6vm                   1/1     Running   0             22h
kube-system   kube-scheduler-minikube            1/1     Running   0             22h
kube-system   storage-provisioner                1/1     Running   5 (10h ago)   22h
```


$ **kubectl help logs**
-c Print the logs of this container

$ **kubectl logs my-nginx-85996f8dbd-j4t7d**

No logs available for this my-nginx pod
Use "kubectl options" for a list of global command-line options (applies to all commands).



$ **kubectl get pods**
```aidl
NAME        READY   STATUS    RESTARTS   AGE
pod-nginx   1/1     Running   0          44h
```


$ **kubectl logs pod-nginx**
```aidl
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2023/03/27 02:57:44 [notice] 1#1: using the "epoll" event method
2023/03/27 02:57:44 [notice] 1#1: nginx/1.22.1
2023/03/27 02:57:44 [notice] 1#1: built by gcc 11.2.1 20220219 (Alpine 11.2.1_git20220219)
2023/03/27 02:57:44 [notice] 1#1: OS: Linux 3.10.0-1160.81.1.el7.x86_64
2023/03/27 02:57:44 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2023/03/27 02:57:44 [notice] 1#1: start worker processes
2023/03/27 02:57:44 [notice] 1#1: start worker process 30
2023/03/27 02:57:44 [notice] 1#1: start worker process 31
```

$ **kubectl logs vganesh**
```aidl
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2023/03/26 15:30:36 [notice] 1#1: using the "epoll" event method
2023/03/26 15:30:36 [notice] 1#1: nginx/1.22.1
2023/03/26 15:30:36 [notice] 1#1: built by gcc 11.2.1 20220219 (Alpine 11.2.1_git20220219)
2023/03/26 15:30:36 [notice] 1#1: OS: Linux 3.10.0-1160.81.1.el7.x86_64
2023/03/26 15:30:36 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2023/03/26 15:30:36 [notice] 1#1: start worker processes
2023/03/26 15:30:36 [notice] 1#1: start worker process 30
2023/03/26 15:30:36 [notice] 1#1: start worker process 31

```


$ **minikube dashboard --url**



From http://127.0.0.1:45088/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/


