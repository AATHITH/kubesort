## What is this KUBESORT?

This a Bash Script that will help you forget the kubectl's default, difficult to remember, sorting feature by making it simpler.<br>
`kubectl` has its own `--sort-by=json-path` feature for sorting but **kubesort** will makes the sorting easier.

## Why you need kubesort?

1) It's simple
2) Helps you sort the results from `kubectl` in an easy way.
3) You don't have to type `kubectl --sort-by=.status.containerStatuses[0].restartcount get po` to sort the pod by their STATUS, just type `kubesort po restarts` that's it.


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
<summary>## Samples:</summary>
<br>

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
