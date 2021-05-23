## What is this KUBESORT?

This a Bash Script that will help you forget the kubectl's default, difficult to remember, sorting feature by making it simpler.<br>
`kubectl` has its own `--sort-by=json-path` feature for sorting but **kubesort** will makes the sorting easier.

## Why you need KUBESORT?

1) It's simple
2) Helps you sort the results from `kubectl` in an easy way.
3) You don't have to type the long command `kubectl --sort-by=.status.containerStatuses[0].restartcount get po` to sort the pod by their `RESTART` count, just type `kubesort po restarts` that's it.


## 2 Step Installation:
Linux
Since kubesort is written in Bash, KUBESORT is exoected to run on any POSIX environment that has Bash installed.

1) Download the kubesort scripts:<br>
   `sudo git clone https://github.com/aathith/kubesort /usr/local/bin/kubesort`
2) Make the script executable:<br>
   `chmod +x /usr/local/bin/kubesort`

   
## Usage:
```
SYNTAX: kubesort option1 option2 option3
AVAILABLE OPTIONS:
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
## Samples

<details><summary>Sorting Pod</summary>
<p>



```
root@k8-master-01:~/kubesort# kubesort po restarts kube-system
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

root@k8-master-01:~/kubesort# kubesort po restart kubernetes-dashboard
NAME                                         READY   STATUS    RESTARTS   AGE
dashboard-metrics-scraper-6c554969c6-8x2fc   1/1     Running   0          40d
kubernetes-dashboard-56c5f95c6b-8c89b        1/1     Running   3          40d

root@k8-master-01:~/kubesort# kubesort po age all
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

root@k8-master-01:~/kubesort# kubesort po name dev
NAME                         READY   STATUS    RESTARTS   AGE
hello-app-5f9d7479bd-5mzmc   1/1     Running   0          2d6h
hello-app-5f9d7479bd-db9s2   1/1     Running   0          2d6h
hello-app-5f9d7479bd-kc4kr   1/1     Running   0          2d6h
```
</p>
</details>
<details><summary>Sorting Deployments</summary>
<p>

```
root@k8-master-01:~# kubesort deployment name
NAME              READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS        IMAGES                                      SELECTOR
alert-checker     1/1     1            1           155d   alert-checker     aathith/testing:alert-checker               app=alert-checker
prom-trail        1/1     1            1           113d   prom-trail        aathith/testing:prometheus-url-annotation   app=prom-trail
prometheus        1/1     1            1           115d   prometheus        prom/prometheus                             app=prometheus-server

root@k8-master-01:~# kubesort deployment name all
NAMESPACE              NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS                              IMAGES                                                      SELECTOR
default                alert-checker                           1/1     1            1           155d   alert-checker                           aathith/testing:alert-checker                               app=alert-checker
kube-system            coredns                                 2/2     2            2           169d   coredns                                 k8s.gcr.io/coredns:1.6.5                                    k8s-app=kube-dns
kubernetes-dashboard   dashboard-metrics-scraper               1/1     1            1           57d    dashboard-metrics-scraper               kubernetesui/metrics-scraper:v1.0.1                         k8s-app=dashboard-metrics-scraper
kube-system            digitalocean-cloud-controller-manager   1/1     1            1           168d   digitalocean-cloud-controller-manager   digitalocean/digitalocean-cloud-controller-manager:v0.1.6   app=digitalocean-cloud-controller-manager
kubernetes-dashboard   kubernetes-dashboard                    1/1     1            1           57d    kubernetes-dashboard                    kubernetesui/dashboard:v2.0.0-beta5                         k8s-app=kubernetes-dashboard
kube-system            metrics-server                          1/1     1            1           151d   metrics-server                          k8s.gcr.io/metrics-server-amd64:v0.3.6                      k8s-app=metrics-server
nginx-ingress          nginx-ingress                           1/1     1            1           57d    nginx-ingress                           nginx/nginx-ingress:1.6.3                                   app=nginx-ingress
default                prom-trail                              1/1     1            1           113d   prom-trail                              aathith/testing:prometheus-url-annotation                   app=prom-trail
default                prometheus                              1/1     1            1           115d   prometheus                              prom/prometheus                                             app=prometheus-server

root@k8-master-01:~# kubesort deployment containers all
NAMESPACE              NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS                              IMAGES                                                      SELECTOR
default                alert-checker                           1/1     1            1           155d   alert-checker                           aathith/testing:alert-checker                               app=alert-checker
kube-system            coredns                                 2/2     2            2           169d   coredns                                 k8s.gcr.io/coredns:1.6.5                                    k8s-app=kube-dns
kubernetes-dashboard   dashboard-metrics-scraper               1/1     1            1           57d    dashboard-metrics-scraper               kubernetesui/metrics-scraper:v1.0.1                         k8s-app=dashboard-metrics-scraper
kube-system            digitalocean-cloud-controller-manager   1/1     1            1           168d   digitalocean-cloud-controller-manager   digitalocean/digitalocean-cloud-controller-manager:v0.1.6   app=digitalocean-cloud-controller-manager
kubernetes-dashboard   kubernetes-dashboard                    1/1     1            1           57d    kubernetes-dashboard                    kubernetesui/dashboard:v2.0.0-beta5                         k8s-app=kubernetes-dashboard
kube-system            metrics-server                          1/1     1            1           151d   metrics-server                          k8s.gcr.io/metrics-server-amd64:v0.3.6                      k8s-app=metrics-server
nginx-ingress          nginx-ingress                           1/1     1            1           57d    nginx-ingress                           nginx/nginx-ingress:1.6.3                                   app=nginx-ingress
default                prom-trail                              1/1     1            1           113d   prom-trail                              aathith/testing:prometheus-url-annotation                   app=prom-trail
default                prometheus                              1/1     1            1           115d   prometheus                              prom/prometheus                                             app=prometheus-server

root@k8-master-01:~# kubesort deployment age kube-system
NAME                                    READY   UP-TO-DATE   AVAILABLE   AGE    CONTAINERS                              IMAGES                                                      SELECTOR
coredns                                 2/2     2            2           169d   coredns                                 k8s.gcr.io/coredns:1.6.5                                    k8s-app=kube-dns
digitalocean-cloud-controller-manager   1/1     1            1           168d   digitalocean-cloud-controller-manager   digitalocean/digitalocean-cloud-controller-manager:v0.1.6   app=digitalocean-cloud-controller-manager
metrics-server                          1/1     1            1           151d   metrics-server                          k8s.gcr.io/metrics-server-amd64:v0.3.6                      k8s-app=metrics-server

```
</p>
</details>
<details><summary>Sorting Service</summary>
<p>

```
root@k8-master-01:~# kubesort svc type
NAME              TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                         AGE    SELECTOR
kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP                         169d   <none>
alert-checker     NodePort    10.110.87.73     <none>        8080:31080/TCP                  155d   app=alert-checker
prom-trail        NodePort    10.97.208.221    <none>        8080:32445/TCP,1234:32446/TCP   115d   app=prom-trail
prometheus        NodePort    10.98.222.241    <none>        9090:31976/TCP                  117d   app=prometheus-server

root@k8-master-01:~# kubesort svc age kube-system
NAME             TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                  AGE    SELECTOR
kube-dns         ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP,9153/TCP   169d   k8s-app=kube-dns
tiller-deploy    ClusterIP   10.108.104.169   <none>        44134/TCP                165d   app=helm,name=tiller
metrics-server   ClusterIP   10.98.220.21     <none>        443/TCP                  162d   k8s-app=metrics-server
kubelet          ClusterIP   None             <none>        10250/TCP                117d   <none>
   
root@k8-master-01:~# kubesort svc clusterip all
NAMESPACE              NAME                        TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                         AGE    SELECTOR  
default                kubernetes                  ClusterIP   10.96.0.1        <none>        443/TCP                         169d   <none>
kube-system            kube-dns                    ClusterIP   10.96.0.10       <none>        53/UDP,53/TCP,9153/TCP          169d   k8s-app=kube-dns
default                prom-trail                  NodePort    10.97.208.221    <none>        8080:32445/TCP,1234:32446/TCP   115d   app=prom-trail
kubernetes-dashboard   kubernetes-dashboard        NodePort    10.98.9.79       <none>        443:30402/TCP                   57d    k8s-app=kubernetes-dashboard
kube-system            metrics-server              ClusterIP   10.98.220.21     <none>        443/TCP                         162d   k8s-app=metrics-server
default                prometheus                  NodePort    10.98.222.241    <none>        9090:31976/TCP                  117d   app=prometheus-server
kube-system            tiller-deploy               ClusterIP   10.108.104.169   <none>        44134/TCP                       165d   app=helm,name=tiller
kubernetes-dashboard   dashboard-metrics-scraper   ClusterIP   10.108.179.217   <none>        8000/TCP                        57d    k8s-app=dashboard-metrics-scraper
default                alert-checker               NodePort    10.110.87.73     <none>        8080:31080/TCP                  155d   app=alert-checker
nginx-ingress          nginx-ingress               NodePort    10.110.160.112   <none>        80:31372/TCP,443:31289/TCP      57d    app=nginx-ingress
kube-system            kubelet                     ClusterIP   None             <none>        10250/TCP                       117d   <none>
```
</p>
</details>

### v0.3.0 Limitations:
 You need Bash in your system.(will add more ways to install in future versions).

### v0.3.0 Release notes:
  Typing to sort kubectl output is reduced furter with the addion of option to run KUBESORT with PIPE so that you don't have to remember seperate syntax for kubesort<br>
  eg.:`kubesort get po age | kubesort` will get Pods sorted by their age.

### Roadmap:
1) Sort for resource pv, pvc, replicasets, replication controllers, ingress resources, nodes, namespaces will be included.
2) Bash auto-completion will be included.
3) making this into Kubectl plugin.
4) more install options.
5) Video instruction on how to use KUBESORT.


### Tried and Tested in:
   k8s: v1.18.1<br>
   kubectl: v1.18.1<br>
   ubuntu: 18.04<br>
   bash: v4.4<br>


## Contribution are welcomed here.
#### What can you contribute?
1) Reduce the no. of lines of the code.
2) Add things to matchup with the Roadmap.
#### Who can contribute?
ANY ONE WITH INTEREST.


## *** If KUBESORT interests you Do Give this Project a Star ***
