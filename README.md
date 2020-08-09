# Testing Hashicorp Vault

## Requirements:
- Ubuntu 20.04
- virtualbox
- kubectl
- minikube
- helm
- vault

## Install Virtualbox
```
$ sudo apt -y install virtualbox
```
## Install kubectl
```
$ curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"
$ chmod +x ./kubectl
$ sudo mv kubectl /usr/local/bin/
```

##  Install minikube
```
$ curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64   && chmod +x minikube
$ sudo mv minikube /usr/local/bin/
$ minikube version
minikube version: v1.12.2
commit: be7c19d391302656d27f1f213657d925c4e1cfc2-dirty
```

## Start minikube
```
$ minikube start --driver=virtualbox
😄  minikube v1.12.2 on Ubuntu 20.04
✨  Using the virtualbox driver based on user configuration
💿  Downloading VM boot image ...
    > minikube-v1.12.2.iso.sha256: 65 B / 65 B [-------------] 100.00% ? p/s 0s
    > minikube-v1.12.2.iso: 173.73 MiB / 173.73 MiB [] 100.00% 57.44 MiB p/s 3s
👍  Starting control plane node minikube in cluster minikube
💾  Downloading Kubernetes v1.18.3 preload ...
    > preloaded-images-k8s-v5-v1.18.3-docker-overlay2-amd64.tar.lz4: 510.91 MiB
🔥  Creating virtualbox VM (CPUs=2, Memory=5900MB, Disk=20000MB) ...
🐳  Preparing Kubernetes v1.18.3 on Docker 19.03.12 ...
🔎  Verifying Kubernetes components...
🌟  Enabled addons: default-storageclass, storage-provisioner
🏄  Done! kubectl is now configured to use "minikube"
👉  You can use kubectl inside minikube. For more information, visit https://minikube.sigs.k8s.io/docs/handbook/kubectl/
💡  For best results, install kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/
```
```
$ minikube kubectl config get-clusters
NAME
minikube
```

## Install Helm
```
$ curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
$ sudo apt-get install apt-transport-https --yes
$ echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
$ sudo apt-get update
$ sudo apt-get install helm
```
```
$ helm version
version.BuildInfo{Version:"v3.2.4", GitCommit:"0ad800ef43d3b826f31a5ad8dfbb4fe05d143688", GitTreeState:"clean", GoVersion:"go1.13.12"}
```

## Install Vault
Add repository:
```
$ helm repo add hashicorp https://helm.releases.hashicorp.com
"hashicorp" has been added to your repositories
```
```
$ helm install vault hashicorp/vault
NAME: vault
LAST DEPLOYED: Fri Aug  7 12:59:31 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Thank you for installing HashiCorp Vault!

Now that you have deployed Vault, you should look over the docs on using
Vault with Kubernetes available here:

https://www.vaultproject.io/docs/


Your release is named vault. To learn more about the release, try:

  $ helm status vault
  $ helm get all vault
```
```
$ kubectl get pods
NAME                                    READY   STATUS    RESTARTS   AGE
vault-0                                 0/1     Running   0          3m16s
vault-agent-injector-7d8b64b8d4-89lj8   1/1     Running   0          3m16s
```

