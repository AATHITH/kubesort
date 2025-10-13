# 🔍 KubeSort - Dynamic Kubernetes Resource Sorter

[![Version](https://img.shields.io/badge/version-v1.0.0-blue.svg)](https://github.com/AATHITH/kubesort/releases)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Shell](https://img.shields.io/badge/shell-bash-yellow.svg)](https://www.gnu.org/software/bash/)

## 🎯 What is KubeSort?

KubeSort is a powerful Bash script that transforms kubectl's complex `--sort-by=json-path` syntax into simple, intuitive commands. No more memorizing JSONPath expressions - just use plain English field names to sort your Kubernetes resources!

## ⭐ Why Choose KubeSort?

✅ **Beginner-Friendly** - Simple syntax that anyone can learn  
✅ **Comprehensive** - Supports 14+ Kubernetes resource types  
✅ **Modern** - Uses standard kubectl flag conventions (`-n`, `-A`)  
✅ **Dynamic** - Automatically discovers available sort fields  
✅ **Fast** - Direct kubectl integration with no overhead  

**Before KubeSort:**
```bash
kubectl --sort-by=.status.containerStatuses[0].restartCount get pods -n kube-system -o wide
```

**With KubeSort:**
```bash
kubesort kubectl get pods restarts -n kube-system
```


## 🚀 Quick Installation

### Prerequisites
- Kubernetes cluster with `kubectl` configured
- Bash shell (any POSIX-compliant environment)

### Install Options

#### Option 1: Direct Download (Recommended)
```bash
# Download kubesort to your local bin directory
curl -o /usr/local/bin/kubesort https://raw.githubusercontent.com/AATHITH/kubesort/main/kubesort
chmod +x /usr/local/bin/kubesort
```

#### Option 2: Git Clone
```bash
# Clone and install
git clone https://github.com/AATHITH/kubesort.git
sudo cp kubesort/kubesort /usr/local/bin/
sudo chmod +x /usr/local/bin/kubesort
```

#### Option 3: Local Installation
```bash
# Install to user's local bin (add ~/.local/bin to PATH)
mkdir -p ~/.local/bin
curl -o ~/.local/bin/kubesort https://raw.githubusercontent.com/AATHITH/kubesort/main/kubesort
chmod +x ~/.local/bin/kubesort
```

## 📖 Usage

### Syntax
```bash
kubesort kubectl get <resource_type> <sort_field> [-n namespace|-A|--all-namespaces]
```

### 🎯 Namespace Options
- **Specific namespace:** `-n <namespace>` (e.g., `-n kube-system`)
- **All namespaces:** `-A` or `--all-namespaces`  
- **Default:** Uses current context's default namespace

### 📋 Supported Resources & Sort Fields

<details>
<summary><b>📦 Pods (po/pod/pods)</b></summary>

**Sort Fields:** `name`, `status`, `restarts`, `age`, `ip`, `node`, `ready`

```bash
kubesort kubectl get pods name -n kube-system
kubesort kubectl get po restarts -A
kubesort kubectl get pods age
```
</details>

<details>
<summary><b>🚀 Deployments (deploy/deployment/deployments)</b></summary>

**Sort Fields:** `name`, `ready`, `uptodate`, `available`, `age`, `containers`, `images`

```bash
kubesort kubectl get deployments name -A
kubesort kubectl get deploy age -n default
```
</details>

<details>
<summary><b>🔗 Services (svc/service/services)</b></summary>

**Sort Fields:** `name`, `type`, `clusterip`, `externalip`, `port`, `age`

```bash
kubesort kubectl get services type -A
kubesort kubectl get svc port -n nginx-ingress
```
</details>

<details>
<summary><b>🖥️ Nodes (node/nodes)</b></summary>

**Sort Fields:** `name`, `status`, `roles`, `age`, `version`, `internal-ip`, `external-ip`

```bash
kubesort kubectl get nodes age
kubesort kubectl get nodes status
```
</details>

<details>
<summary><b>💾 Persistent Volumes (pv/persistentvolume/persistentvolumes)</b></summary>

**Sort Fields:** `name`, `capacity`, `accessmodes`, `reclaimpolicy`, `status`, `claim`, `storageclass`, `age`

```bash
kubesort kubectl get pv capacity
kubesort kubectl get pv status
```
</details>

<details>
<summary><b>📝 Persistent Volume Claims (pvc/persistentvolumeclaim/persistentvolumeclaims)</b></summary>

**Sort Fields:** `name`, `status`, `volume`, `capacity`, `accessmodes`, `storageclass`, `age`

```bash
kubesort kubectl get pvc capacity -n default
kubesort kubectl get pvc status -A
```
</details>

<details>
<summary><b>🔄 ReplicaSets (rs/replicaset/replicasets)</b></summary>

**Sort Fields:** `name`, `desired`, `current`, `ready`, `age`

```bash
kubesort kubectl get rs ready -A
kubesort kubectl get replicasets age
```
</details>

<details>
<summary><b>⚙️ Other Resources</b></summary>

**DaemonSets (ds/daemonset/daemonsets)**  
Fields: `name`, `desired`, `current`, `ready`, `uptodate`, `available`, `age`

**StatefulSets (sts/statefulset/statefulsets)**  
Fields: `name`, `ready`, `age`

**ConfigMaps (cm/configmap/configmaps)**  
Fields: `name`, `data`, `age`

**Secrets (secret/secrets)**  
Fields: `name`, `type`, `data`, `age`

**Ingress (ing/ingress/ingresses)**  
Fields: `name`, `class`, `hosts`, `address`, `ports`, `age`

**Namespaces (ns/namespace/namespaces)**  
Fields: `name`, `status`, `age`

**ReplicationControllers (rc/replicationcontroller/replicationcontrollers)**  
Fields: `name`, `desired`, `current`, `ready`, `age`
</details>
## 🌟 Quick Examples

### Basic Sorting
```bash
# Sort pods by name in default namespace
kubesort kubectl get pods name

# Sort nodes by age (cluster-wide resource)
kubesort kubectl get nodes age

# Sort services by type across all namespaces
kubesort kubectl get services type -A
```

### Advanced Examples
```bash
# Monitor pod restarts across all namespaces
kubesort kubectl get pods restarts -A

# Check deployment readiness in specific namespace
kubesort kubectl get deployments ready -n production

# Review PVC capacity usage
kubesort kubectl get pvc capacity -A

# Sort nodes by Kubernetes version
kubesort kubectl get nodes version

# Check ingress resources by class
kubesort kubectl get ingress class -A
```

### 💡 Pro Tips
```bash
# Get help with available resources and fields
kubesort kubectl get help

# Sort by age to see oldest resources first
kubesort kubectl get pods age -n kube-system

# Use -A for cluster-wide view
kubesort kubectl get secrets type -A

# Combine with other kubectl flags
kubesort kubectl get pods ready -n monitoring | grep -v Running
```

### Sample Output
```bash
$ kubesort kubectl get pods restarts -n kube-system
🚀 Executing: kubectl get pod --sort-by=.status.containerStatuses[0].restartCount -n kube-system -o wide
─────────────────────────────────────────────────────────────
NAME                     READY   STATUS    RESTARTS   AGE   IP             NODE
coredns-558bd4d5db-k8z9x  1/1     Running   0          45d   10.244.0.2     worker-1
kube-proxy-abc123         1/1     Running   1          45d   192.168.1.10   worker-1
calico-node-def456        1/1     Running   2          45d   192.168.1.10   worker-1
```


## 🚧 Roadmap

### ✅ Completed in v1.0.0
- [x] Support for PV, PVC, ReplicaSets, ReplicationControllers, Nodes, Namespaces
- [x] Modern kubectl flag conventions (`-n`, `-A`)
- [x] Dynamic resource and field discovery
- [x] Comprehensive error handling
- [x] 14+ Kubernetes resource types supported

### 🔮 Future Enhancements
- [ ] Shell completion (bash/zsh/fish)
- [ ] JSON/YAML output format options
- [ ] Custom JSONPath expressions
- [ ] Multi-column sorting
- [ ] Filtering capabilities
- [ ] Configuration file support
- [ ] Package manager installations (brew, apt, yum)

## 🧪 Compatibility

**Tested Environments:**
- **Kubernetes:** v1.24+ (EKS, GKE, AKS, self-managed)
- **kubectl:** v1.24+
- **Bash:** v4.0+ (Linux, macOS, WSL)
- **Platforms:** Linux, macOS, Windows (WSL/Git Bash)

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### 🔧 Code Contributions
- **Bug fixes** - Find and fix issues
- **New resources** - Add support for CRDs and newer K8s resources  
- **Performance** - Optimize script performance
- **Features** - Implement roadmap items

### 📝 Documentation
- **Examples** - Add real-world usage examples
- **Tutorials** - Create guides for specific use cases
- **Translations** - Help with internationalization

### 🧪 Testing
- **Platform testing** - Test on different OS/K8s versions
- **Edge cases** - Find and report unusual scenarios
- **Performance testing** - Test with large clusters

### How to Contribute
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📬 Support & Community

- 🐛 **Bug Reports:** [GitHub Issues](https://github.com/AATHITH/kubesort/issues)
- 💡 **Feature Requests:** [GitHub Discussions](https://github.com/AATHITH/kubesort/discussions)
- 📖 **Documentation:** [Wiki](https://github.com/AATHITH/kubesort/wiki)
- 📰 **Release Notes:** [Releases](https://github.com/AATHITH/kubesort/releases)

## ⭐ Show Your Support

If KubeSort helps you manage Kubernetes resources more efficiently, please give it a star! ⭐

Your support helps us continue improving the project and shows that the community finds it valuable.

---

<div align="center">
  
**Made with ❤️ for the Kubernetes community**

[⭐ Star on GitHub](https://github.com/AATHITH/kubesort) • 
[🐛 Report Bug](https://github.com/AATHITH/kubesort/issues) • 
[💡 Request Feature](https://github.com/AATHITH/kubesort/discussions)

</div>
