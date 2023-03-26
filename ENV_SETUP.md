# Infrastructure Automation Kubernetes Pre-lab

## Introduction: 

In this lab, you will install and start to use Minikube - a which acts like a local Kubernetes.  

## Objective

For this lab, you will install the required tools needed to continue with the kubernetes course.



## Instructions:


The steps below are from these install information links

* [minikube][install-minikube]
* [kubectl][install-kubectl]
---
## install minikube 

1- download the binary

 ```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && chmod +x minikube
```

2- make minikube executable
```
sudo mkdir -p /usr/local/bin/
sudo install minikube /usr/local/bin/
```

## install kubectl
---
1- download
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

2- make executable

```
sudo mv ./kubectl /usr/local/bin/kubectl
chmod +x /usr/local/bin/kubectl

```
3- verify
```
kubectl version --client
```

4- Validate output - should be

output should be similar to:
```
Client Version: version.Info{Major:"1", Minor:"18", GitVersion:"v1.18.4", GitCommit:"c96aede7b5205121079932896c4ad89bb93260af", GitTreeState:"clean", BuildDate:"2020-06-17T11:41:22Z", GoVersion:"go1.13.9", Compiler:"gc", Platform:"linux/amd64"}
```

**Optionally** install [command completion][install-completion] for working with `kubectl`

---

## verify minikube installation

0- run the following start your minikube:
```
minikube start
```

1- run the following to get the status

```
minikube status
```

2- run the following to stop minikube
```
minikube stop
```

3-  finally delete the minikube instance with:
```
minikube delete
```

4- run the following restart your minikube:
```
minikube start
```





## Submitting Your Work

Nothing to submit

[minikube]: https://github.com/kubernetes/minikube
[install-kubectl]: https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl
[install-minikube]: https://kubernetes.io/docs/tasks/tools/install-minikube/
[install-completion]: https://kubernetes.io/docs/tasks/tools/install-kubectl/#enabling-shell-autocompletion

## Ganesh notes. 

```agsl
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
&& chmod +x minikube

sudo mkdir -p /usr/local/bin/

sudo install minikube /usr/local/bin/

curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl





```
ls -ltr /usr/local/bin/kubectl
-rwxr-xr-x. 1 vganesh docker 48037888 Mar 20 18:51 /usr/local/bin/kubectl


kubectl version --client

$ kubectl version --short
Flag --short has been deprecated, and will be removed in the future. The --short output will become the default.
Client Version: v1.26.3
Kustomize Version: v4.5.7
Server Version: v1.26.1

https://kubernetes.io/docs/tutorials/hello-minikube/


minikube dashboard --url
...
Verifying proxy health ...
http://127.0.0.1:44772/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/

From another terminal 

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh
$ minikube start

😄  minikube v1.29.0 on Centos 7.9.2009

✨  Using the docker driver based on existing profile

👍  Starting control plane node minikube in cluster minikube

🚜  Pulling base image ...

🏃  Updating the running docker "minikube" container ...

🐳  Preparing Kubernetes v1.26.1 on Docker 20.10.23 ...

🔎  Verifying Kubernetes components...

▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5

❗  Executing "docker container inspect minikube --format={{.State.Status}}" took an unusually long time: 3.626301816s

💡  Restarting the docker service may improve performance.

▪ Using image docker.io/kubernetesui/metrics-scraper:v1.0.8

▪ Using image docker.io/kubernetesui/dashboard:v2.7.0

💡  Some dashboard features require the metrics-server addon. To enable all features please run:

        minikube addons enable metrics-server   


🌟  Enabled addons: storage-provisioner, default-storageclass, dashboard

🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh
$ 

$ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured



/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh
$ minikube stop

✋  Stopping node "minikube"  ...

🛑  Powering off "minikube" via SSH ...

🛑  1 node stopped.

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh

$ minikube delete

🔥  Deleting "minikube" in docker ...

🔥  Deleting container "minikube" ...

🔥  Removing /home/CSCC/vganesh/.minikube/machines/minikube ...

💀  Removed all traces of the "minikube" cluster.

/home/CSCC/vganesh/IdeaProjects/infrastructure-kubernetes-week-1-examples-vganesh
$ 


