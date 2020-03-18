# Why you need `kubesort`:
`kubesort` helps you sort the results from `kubectl get` in an easy way.

You don't have to type `kubectl --sort-by=.status.containerStatuses[0].restartcount get po` to sort the pod by their STATUS, just type `kubesort status` that's it.

`kubectl` has its own `--sort-by=json-path` feature for sorting but `kubesort` will make the sorting more easy.
## Installation:
Linux
Since kubectx/kubens are written in Bash, you should be able to install them to any POSIX environment that has Bash installed.

1) Download the kubesort scripts:<br>
   `sudo git clone https://github.com/aathith/kubesort /path/kubesort`
2) Make the script executable:<br>
   `chmod +x /path/kubesort`
3) Create symlinks to kubesort:<br>
   `sudo ln -s /path/kubesort /usr/local/bin/kubesort`
   
## Usage:
```
  kubesort sortby namespace_name
 
          sortby: name      # kubectl --sort-by=.metadata.name get po
                  status    # kubectl --sort-by=.status.phase get po
                  restarts  # kubectl --sort-by=.status.containerStatuses[0].restartcount get po
                  age       # kubectl --sort-by=.status.startTime get po
                  ip        # kubectl --sort-by=.status.podIP get po
                  node      # kubectl --sort-by=.spec.nodeName get po
                  help      # List available commands
  namespace_name: all              # kubectl --sort-by=option get po --all-namespaces
                  namespace_name   # kubectl --sort-by=option get po -n namespace_name
```
## Samples:
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
### v0.1.0 Limitations:
1) As for now you can only sort for `kubectl get pod`.
2) You need bash in your system.(will add more ways to install in upcomming versions).

### v0.1.0 Release notes:
1) Sort by name, status, restarts, age, ip and node for pod.
2) Sort across Namespaces for pod.
### v0.2.0 roadmap:
1) Sort for resource Deployments, services, namespaces will be included.
2) Bash auto-completion will be included.
3) more install options.

### Tried and Tested:
In k8: v1.15<br>
   kubectl: v1.15<br>
   ubuntu: 18.04<br>
   bash: v4.4<br>
