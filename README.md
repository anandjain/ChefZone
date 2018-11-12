---
author:
- Denny Zhang
classoption: 8pt
email: 'denny@dennyzhang.com'
export_exclude_tags: exclude noexport
header-includes:
- '\usepackage[margin=0.6in]{geometry}'
- '\usepackage[english]{babel}'
- '\usepackage{lastpage}'
- '\usepackage{fancyhdr}'
- '\pagestyle{fancy}'
- '\fancyhf{}'
- '\rhead{Updated: \today}'
- '\rfoot{\thepage\ of \pageref{LastPage}}'
- '\lfoot{\href{https://github.com/dennyzhang/cheatsheet-kubernetes-A4}{GitHub: https://github.com/dennyzhang/cheatsheet-kubernetes-A4}}'
- '\lhead{\href{https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-A4}{Blog URL: https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-A4}}'
priorities: A D C
startup: overview customtime noalign logdone showall
tags: 'noexport(n)'
---

\usepackage[margin=0.6in]{geometry}

\usepackage[english]{babel}

\usepackage{lastpage}

\usepackage{fancyhdr}

\pagestyle{fancy}

\fancyhf{}

\rhead{Updated: \today}

\rfoot{\thepage\ of \pageref{LastPage}}

\lfoot{\href{https://github.com/dennyzhang/cheatsheet-kubernetes-A4}{GitHub: https://github.com/dennyzhang/cheatsheet-kubernetes-A4}}

\lhead{\href{https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-A4}{Blog URL: https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-A4}}

Kubernets CheatSheet[]{.tag data-tag-name="Kubernetes"} {#kubernets-cheatsheet type="kubernetes" export_file_name="cheatsheet-kubernetes-A4.pdf"}
=======================================================

<a href="https://github.com/dennyzhang/cheatsheet-kubernetes-A4"><img align="right" width="200" height="183" src="https://www.dennyzhang.com/wp-content/uploads/denny/watermark/github.png" /></a>
<div id="the whole thing" style="overflow: hidden;">
<div style="float: left; padding: 5px"> <a href="https://www.linkedin.com/in/dennyzhang001"><img src="https://www.dennyzhang.com/wp-content/uploads/sns/linkedin.png" alt="linkedin" /></a></div>
<div style="float: left; padding: 5px"><a href="https://github.com/dennyzhang"><img src="https://www.dennyzhang.com/wp-content/uploads/sns/github.png" alt="github" /></a></div>
<div style="float: left; padding: 5px"><a href="https://www.dennyzhang.com/slack" target="_blank" rel="nofollow"><img src="https://slack.dennyzhang.com/badge.svg" alt="slack"/></a></div>
</div>

<br/><br/>
<a href="http://makeapullrequest.com" target="_blank" rel="nofollow"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome"/></a>

-   PDF Link:
    [cheatsheet-kubernetes-A4.pdf](https://github.com/dennyzhang/cheatsheet-kubernetes-A4/blob/master/cheatsheet-kubernetes-A4.pdf)
-   Blog URL:
    <https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-A4>
-   Category:
    [kubernetes](https://cheatsheet.dennyzhang.com/category/kubernetes/)

File me
[Issues](https://github.com/dennyzhang/cheatsheet-kubernetes-A4/issues)
or star [this
repo](https://github.com/DennyZhang/cheatsheet-kubernetes-A4).

See more CheatSheets from Denny:
[\#denny-cheatsheets](https://github.com/topics/denny-cheatsheets)

-   Check kubernetes cheatsheet:
    <https://cheatsheet.dennyzhang.com/cheatsheet-minikube-A4>
-   Yaml Templates:
    <https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml>

### Common Commands

  Name                                        Command
  ------------------------------------------- --------------------------------------------------------------------------
  List everything                             `kubectl get all --all-namespaces`
  Validate yaml file with dry run             `kubectl create --dry-run --validate -f pod-dummy.yaml`
  Start a temporary pod for testing           `kubectl run --rm -i -t --image=alpine test-$RANDOM -- sh`
  Run wget test temporarily                   `kubectl run --rm mytest --image=busybox -it`
  Run curl test temporarily                   `kubectl run --rm mytest --image=yauritux/busybox-curl -it`
  Get system conf via configmap               `kubectl -n kube-system get cm kubeadm-config -o yaml`
  Explain resource                            `kubectl explain pods`, `kubectl explain svc`
  Get all services                            `kubectl get service --all-namespaces`
  Get services sorted by name                 kubectl get services --sort-by=.metadata.name
  Get pods sorted by restart count            kubectl get pods --sort-by='.status.containerStatuses\[0\].restartCount'
  Query healthcheck endpoint                  `curl -L http://127.0.0.1:10250/healthz`
  Open a bash terminal in a pod               `kubectl exec -it storage sh`
  Check pod environment variables             `kubectl exec redis-master-ft9ex env`
  Enabling shell autocompletion for kubectl   `echo "source <(kubectl completion bash)" >> ~/.bashrc`, then reconnect
  In mac desktop, use minikube dockerd        `eval $(minikube docker-env)`, No need to docker push any more

Components & Services
---------------------

-   Services on Master Nodes

  Name                                                                                                          Summary
  ------------------------------------------------------------------------------------------------------------- --------------------------------------------------------------------------------------------------------
  [kube-apiserver](https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-apiserver)                     exposes the Kubernetes API from master nodes
  [etcd](https://coreos.com/etcd/)                                                                              reliable data store for all k8s cluster data
  [kube-scheduler](https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-scheduler)                     schedule pods to run on selected nodes
  [kube-controller-manager](https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-controller-manager)   node controller, replication controller, endpoints controller, and service account & token controllers

-   Services on Worker Nodes

  Name                                                                                Summary
  ----------------------------------------------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------
  [kubelet](https://github.com/kubernetes/kubernetes/tree/master/cmd/kubelet)         makes sure that containers are running in a pod
  [kube-proxy](https://github.com/kubernetes/kubernetes/tree/master/cmd/kube-proxy)   perform connection forwarding
  Container Runtime                                                                   Kubernetes supported runtimes: Docker, rkt, runc and any [OCI runtime-spec](https://github.com/opencontainers/runtime-spec) implementation.

-   Addons: pods and services that implement cluster features

  Name                            Summary
  ------------------------------- ---------------------------------------------------------------------------
  DNS                             serves DNS records for Kubernetes services
  Web UI                          a general purpose, web-based UI for Kubernetes clusters
  Container Resource Monitoring   collect, store and serve container metrics
  Cluster-level Logging           save container logs to a central log store with search/browsing interface

-   Tools

  Name                                                                           Summary
  ------------------------------------------------------------------------------ -----------------------------------------------------------------------------------------
  [kubectl](https://github.com/kubernetes/kubernetes/tree/master/cmd/kubectl)    the command line util to talk to k8s cluster
  [kubeadm](https://github.com/kubernetes/kubernetes/tree/master/cmd/kubeadm)    the command to bootstrap the cluster
  [kubefed](https://kubernetes.io/docs/reference/setup-tools/kubefed/kubefed/)   the command line to control a Kubernetes Cluster Federation
  Kubernetes Components                                                          [link: Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)

Check Performance
-----------------

  Name                                           Command
  ---------------------------------------------- ------------------------------------------------------
  Get node resource usage                        `kubectl top node`
  Get pod resource usage                         `kubectl top pod`
  Get resource usage for a given pod             `kubectl top <podname> --containers`
  List resource utilization for all containers   `kubectl top pod --all-namespaces --containers=true`

Resources Deletion
------------------

  Name                                 Command
  ------------------------------------ --------------------------------------------------------------
  Delete pod                           `kubectl delete pod hello-node-95913-n63qs -n $my-namespace`
  Delete pods by labels                `kubectl delete pod -l env=test`
  Delete deployments by labels         `kubectl delete deployment -l app=wordpress`
  Delete persist volumes by labels     `kubectl delete pvc -l app=wordpress`
  Delete statefulset only (not pods)   `kubectl delete sts <stateful_set_name> --cascade=false`

Pod
---

  Name                           Command
  ------------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------
  List all pods                  `kubectl get pods`
  List pods for all namespace    `kubectl get pods -all-namespaces`
  List all critical pods         `kubectl get -n kube-system pods -a`
  List pods with more info       `kubectl get pod -o wide`, `kubectl get pod -o yaml`
  Get pod info                   `kubectl describe pod srv-mysql-server`
  List all pods with labels      `kubectl get pods --show-labels`
  Get Pod initContainer status   `kubectl get pod --template '{{.status.initContainerStatuses}}' <pod-name>`
  kubectl run command            kubectl exec -it -n "\$ns" "\$podname" -- sh -c "echo \$msg &gt;&gt;/dev/err.log"
  Get pod by selector            podname=\$(kubectl get pods -n \$namespace --selector="app=syslog" -o jsonpath='{.items\[\*\].metadata.name}')
  List pods with docker images   kubectl get pods -o=jsonpath='{range .items\[\*\]}{.metadata.name}:{.spec.containers\[0\].name}{"\t"}{.spec.containers\[0\].image}{"\n"}{end}'
  Kubernetes Yaml Examples       [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

Label & Annontation
-------------------

  Name                               Command
  ---------------------------------- -----------------------------------------------------------------------
  Filter pods by label               `kubectl get pods -l owner=denny`
  Manually add label to a pod        `kubectl label pods dummy-input owner=denny`
  Remove label                       `kubectl label pods dummy-input owner-`
  Manually add annonation to a pod   `kubectl annotate pods dummy-input my-url=https://www.dennyzhang.com`

Deployment & Scale
------------------

[link: Pausing and Resuming a
Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#pausing-and-resuming-a-deployment)

  Name                           Command
  ------------------------------ -------------------------------------------------------------------------------------------------
  Scale out                      `kubectl scale --replicas=3 deployment/nginx-app`
  online rolling upgrade         `kubectl rollout app-v1 app-v2 --image=img:v2`
  Roll backup                    `kubectl rollout app-v1 app-v2 --rollback`
  List rollout                   `kubectl get rs`
  Check update status            `kubectl rollout status deployment/nginx-app`
  Check update history           `kubectl rollout history deployment/nginx-app`
  Pause/Resume                   `kubectl rollout pause deployment/nginx-deployment`, `resume`
  Rollback to previous version   `kubectl rollout undo deployment/nginx-deployment`
  Kubernetes Yaml Examples       [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

Quota & Limits
--------------

  Name                       Command
  -------------------------- -------------------------------------------------------------------------------------------------
  List Resource Quota        `kubectl get resourcequota`
  List Limit Range           `kubectl get limitrange`
  Kubernetes Yaml Examples   [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

Service
-------

  Name                       Command
  -------------------------- -------------------------------------------------------------------------------------------------
  List all services          `kubectl get services`
  List service endpoints     `kubectl get endpoints`
  Get service detail         `kubectl get service nginx-service -o yaml`
  Get service cluster ip     kubectl get service nginx-service -o go-template='{{.spec.clusterIP}}'
  Get service cluster port   kubectl get service nginx-service -o go-template='{{(index .spec.ports 0).port}}'
  Kubernetes Yaml Examples   [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

StatefulSet
-----------

  Name                                 Command
  ------------------------------------ -------------------------------------------------------------------------------------------------
  List statefulset                     `kubectl get sts`
  Scale statefulset                    `kubectl scale sts <stateful_set_name> --replicas=5`
  Delete statefulset only (not pods)   `kubectl delete sts <stateful_set_name> --cascade=false`
  Kubernetes Yaml Examples             [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

Volumes & Volume Claims
-----------------------

  Name                        Command
  --------------------------- -------------------------------------------------------------------------------------------------
  Check the mounted volumes   `kubectl exec storage ls /data`
  Check persist volume        `kubectl describe pv pv0001`
  List storage class          `kubectl get storageclass`
  Kubernetes Yaml Examples    [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

Security
--------

  Name                       Command
  -------------------------- -------------------------------------------------------------------------------------------------
  List certificates          `kubectl get csr`
  Kubernetes Yaml Examples   [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

Resources
---------

  Name                            Command
  ------------------------------- ----------------------------------------------------------------------------------
  Customize resource definition   `kubectl set resources deployment nginx -c=nginx --limits=cpu=200m,memory=512Mi`

Other Components
----------------

### Log files

  Name                             Command
  -------------------------------- -----------------------------------------
  API Server.log= in master node   `/var.log=/kube-apiserver.log`
  Scheduler.log= in master node    `/var.log=/kube-scheduler.log`
  Controller.log= in master node   `/var.log=/kube-controller-manager.log`
  Kubelet.log= in worker node      `/var.log=/kubelet.log`
  Kube Proxy.log= in worker node   `/var.log=/kubelet-proxy.log`

### Events & Metrics

  Name              Command
  ----------------- ---------------------------------------
  View all events   `kubectl get events --all-namespaces`

### Namespace & Security

  Name                          Command
  ----------------------------- -------------------------------------------------------------------------------------------------
  List authenticated contexts   `kubectl config get-contexts`
  List contexts                 `kubectl config get-contexts`
  Switch context                `kubectl config use-context <cluster-name>`
  List all namespaces defined   `kubectl get namespaces`
  kubectl config file           `~/.kube/config`
  Kubernetes Yaml Examples      [link: kubernetes yaml templates](https://cheatsheet.dennyzhang.com/cheatsheet-kubernetes-yaml)

### Network

  Name                                Command
  ----------------------------------- ----------------------------------------------------------
  Temporarily add a port-forwarding   `kubectl port-forward redis-izl09 6379`
  Add port-forwaring for deployment   `kubectl port-forward deployment/redis-master 6379:6379`
  Add port-forwaring for replicaset   `kubectl port-forward rs/redis-master 6379:6379`
  Add port-forwaring for service      `kubectl port-forward svc/redis-master 6379:6379`
  Get network policy                  `kubectl get NetworkPolicy`

Basic
-----

### Key Concepts

  Name   Summary
  ------ -----------------------------------
  CNCF   Cloud Native Computing Foundation
  CRI    Container Runtime Interface
  CNI    Container Network Interface
  CSI    Container Storage Interface

### Kubernets Critical Files

  Name                        Comment
  --------------------------- ---------------------------------------------------------
  Config folder               `/etc/kubernetes/`
  Certificate files           `/etc/kubernetes/pki/`
  Credentials to API server   `/etc/kubernetes/kubelet.conf`
  Superuser credentials       `/etc/kubernetes/admin.conf`
  Kubernets working dir       `/var/lib/kubelet/`
  Docker working dir          `/var/lib/docker/`
  Etcd working dir            `/var/lib/etcd/`
  Network cni                 `/etc/cni/net.d/`
  Docker container log        `/var/log/containers/`
  Log files                   `/var/log/pods/`
  Env                         `export KUBECONFIG=/etc/kubernetes/admin.conf`
  Env                         `/etc/systemd/system/kubelet.service.d/10-kubeadm.conf`

<a href="https://www.dennyzhang.com"><img align="right" width="185" height="37" src="https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/dns_small.png"></a>

### Check status

  Name                                 Summary
  ------------------------------------ --------------------------------------------
  List everything                      `kubectl get all --all-namespaces`
  Get cluster info                     `kubectl cluster-info`
  Get configuration                    `kubectl config view`
  Get kubectl version                  `kubectl version`
  Get component status                 `kubectl get componentstatus`
  Similar to `docker ps`               `kubectl get nodes`
  Similar to `docker inspect`          `kubectl describe pod nginx-app-413181-cn`
  Similar to `docker logs`             `kubectl logs`
  Similar to `docker exec`             `kubectl exec`
  Get services for current namespace   `kubectl get svc`
  Get node status                      `kubectl describe node $node_name`

### Kubernetes Developer Resources

  Name              Summary
  ----------------- --------------------------------------------------------------------------------------------------------------------
  API Conventions   [link: API Conventions](https://github.com/kubernetes/community/blob/master/contributors/devel/api-conventions.md)

Minikube
--------

  Name                                                  Command
  ----------------------------------------------------- ----------------------------------------------------------------------------------------------------
  Get minikube version                                  `minikube version`, [link: all minikube releases](https://github.com/kubernetes/minikube/releases)
  Start minikube with a specific k8s version            `minikube start --kubernetes-version v1.10.0`
  Start minikube env with a bigger machine flavor       `minikube start --memory 5120 --cpus=4`
  Gets all available Kubernetes versions for minikube   `minikube get-k8s-versions`
  Mount host OS's folder to minikube VM                 `minikube mount /host-mount-path:/vm-mount-path`
  Check minikube config in your host OS desktop         `~/.minikube/machines/minikube/config.json`
  folder of k8s.io/minikube-hostpath provisioner        `/tmp/hostpath-provisioner`, `/tmp/hostpath_pv`
  Critical minikube folder                              `/var/lib/localkube`, `/var/lib/docker`, `/data`
  minikube docker-env                                   `eval $(minikube docker-env)`
  Get minikube log                                      `minikube logs`
  Get dashboard                                         `minikube dashboard`
  SSH to minikube vm                                    `minikube ssh`
  Get ip                                                `minikube ip`
  Get cluster info                                      `kubectl cluster-info`
  List addons                                           `minikube addons list`
  Get service info                                      `minikube service $srv_name`

Misc scripts
------------

-   Tail pod log by label

``` {.bash}
namespace="mynamespace"
mylabel="app=mylabel"
kubectl get pod -l "$mylabel" -n "$namespace" | tail -n1 \
    | awk -F' ' '{print $1}' | xargs -I{} \
      kubectl logs -n "$namespace" -f {}
```

-   Get node hardware resource utilization

``` {.bash}
kubectl get nodes --no-headers \
     | awk '{print $1}' | xargs -I {} \
     sh -c 'echo {}; kubectl describe node {} | grep Allocated -A 5'

kubectl get nodes --no-headers | awk '{print $1}' | xargs -I {} \
    sh -c 'echo {}; kubectl describe node {} | grep Allocated -A 5 \
     | grep -ve Event -ve Allocated -ve percent -ve -- ; echo'
```

-   Apply the configuration in manifest.yaml and delete all the other
    configmaps that are not in the file.

``` {.example}
kaubectl apply --prune -f manifest.yaml --all --prune-whitelist=core/v1/ConfigMap
```

More Resources
--------------

License: Code is licensed under [MIT
License](https://www.dennyzhang.com/wp-content/mit_license.txt).

<https://kubernetes.io/docs/reference/kubectl/cheatsheet/>

<https://github.com/kubecamp/kubernetes_in_2_days>

<https://marc.xn--wckerlin-0za.ch/computer/kubernetes-on-ubuntu-16-04>

<https://codefresh.io/kubernetes-guides/kubernetes-cheat-sheet/>

<a href="https://www.dennyzhang.com"><img align="right" width="201" height="268" src="https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/denny_201706.png"></a>

<a href="https://www.dennyzhang.com"><img align="right" src="https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/dns_small.png"></a>
