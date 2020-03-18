`kubesort` helps you sort the results from `kubectl get`
## Installation:
Linux
Since kubectx/kubens are written in Bash, you should be able to install them to any POSIX environment that has Bash installed.

1) Download the kubesort scripts:<br>
   `sudo git clone https://github.com/aathith/kubernetes/kubesort /path/kubesort`
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
