## What is this KUBESORT?

This a Bash Script that will help you forget the kubectl's default, difficult to remember, sorting feature by making it simpler.<br>
`kubectl` has its own `--sort-by=json-path` feature for sorting but **kubesort** will makes the sorting easier.

## Why you need kubesort?

1) It's simple
2) Helps you sort the results from `kubectl` in an easy way.
3) You don't have to type `kubectl --sort-by=.status.containerStatuses[0].restartcount get po` to sort the pod by their `RESTART` count, just type `kubesort po restarts` that's it.


## Installation:
Linux
Since kubesort is written in Bash, you should be able to install them to any POSIX environment that has Bash installed.

1) Download the kubesort scripts:<br>
   `sudo git clone https://github.com/aathith/kubesort /path/kubesort`
2) Make the script executable:<br>
   `chmod +x /path/kubesort`
3) Create symlinks to kubesort:<br>
   `sudo ln -s /path/kubesort /usr/local/bin/kubesort`
   
## Usage:
```
SYNTAX: kubesort option1 option2 option3
AVAAIABLE OPTIONS:
        option1:
        (po/pod/pods), (deployments/deployment/deploy), (svc/service/services)

                option2(po/pod/pods):
                name, status, restarts, age, ip, node

                option2(deployments/deployment/deploy):
                name, uptodate, available, age, containers, images

                option2(svc/service/services):
                name, type, clusterIP, externalIP, ports, age

                        option3: namespace-name or all
```
<details>
<summary>Sorting Pod Samples:</summary>
<br>
```
root@k8-master-01:~/kubesort# kubesort restarts kube-system
NAME                                                     READY   STATUS    RESTARTS   AGE
etcd-k8-master-01                                        1/1     Running   0          58d
tiller-deploy-688ddc6c9-h6424                            1/1     Running   0          26d
kube-apiserver-k8-master-01                              1/1     Running   0          58d
kube-controller-manager-k8-master-01                     1/1     Running   1          58d
kube-scheduler-k8-master-01                              1/1     Running   1          58d
kube-proxy-sclt9                                         1/1     Running   2          56d
kube-flannel-ds-amd64-l579g                              1/1     Running   2          56d
kube-proxy-l592g                                         1/1     Running   7          93d
coredns-5c98db65d4-tw75g                                 1/1     Running   8          60d
kube-flannel-ds-amd64-8krvm                              1/1     Running   9          93d
metricbeat-5rcb4                                         1/1     Running   13         88d
kube-proxy-mlnrc                                         1/1     Running   13         93d
kube-flannel-ds-amd64-lbxbr                              1/1     Running   14         93d
filebeat-9hh95                                           1/1     Running   55         23d

root@k8-master-01:~/kubesort# kubesort restart kubernetes-dashboard
NAME                                         READY   STATUS    RESTARTS   AGE
dashboard-metrics-scraper-6c554969c6-8x2fc   1/1     Running   0          40d
kubernetes-dashboard-56c5f95c6b-8c89b        1/1     Running   3          40d

root@k8-master-01:~/kubesort# kubesort age all
NAMESPACE              NAME                                                     READY   STATUS    RESTARTS   AGE
kube-system            kube-proxy-l592g                                         1/1     Running   7          93d
kube-system            metricbeat-5rcb4                                         1/1     Running   13         88d
kube-system            etcd-k8-master-01                                        1/1     Running   0          58d
kube-system            coredns-5c98db65d4-tw75g                                 1/1     Running   8          60d
kubernetes-dashboard   kubernetes-dashboard-56c5f95c6b-8c89b                    1/1     Running   3          40d
kubernetes-dashboard   dashboard-metrics-scraper-6c554969c6-8x2fc               1/1     Running   0          40d
my-prometheus          prometheus-operator-5bcd9f9d5c-9kwvg                     1/1     Running   0          35d
kube-system            filebeat-7wg6k                                           1/1     Running   55         23d
default                prometheus-784586f976-fq6q8                              1/1     Running   0          9d
dev                    hello-app-5f9d7479bd-kc4kr                               1/1     Running   0          2d6h
olm                    catalog-operator-5bdf7fc7b-52qhw                         1/1     Running   0          5h21m

root@k8-master-01:~/kubesort# kubesort name dev
NAME                         READY   STATUS    RESTARTS   AGE
hello-app-5f9d7479bd-5mzmc   1/1     Running   0          2d6h
hello-app-5f9d7479bd-db9s2   1/1     Running   0          2d6h
hello-app-5f9d7479bd-kc4kr   1/1     Running   0          2d6h
```
</details>

### v0.2.0 Limitations:
 You need Bash in your system.(will add more ways to install in future versions).

### v0.2.0 Release notes:
  You can now sort Deployment(6 options) and Service(5 options) resource in addition to the Pods(5 options).
  Total of 3 resources and 16 options are now supported by KUBESORT.


### Roadmap:
1) Sort for resource pv, pvc, replicasets, replication controllers, ingress resources, nodes, namespaces will be included.
2) Bash auto-completion will be included.
3) making this into Kubectl plugin.
4) more install options.


### Tried and Tested in:
   k8s: v1.18.1<br>
   kubectl: v1.18.1<br>
   ubuntu: 18.04<br>
   bash: v4.4<br>
