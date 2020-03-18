## Why you need `kubesort`:
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
## Example:

### v0.1.0 Limitations:
1) As for now you can only sort for `kubectl get pod`.
2) You need bash in your system.(will add more ways to install in upcomming versions).

### v0.1.0:
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
