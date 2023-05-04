## Kubernetes Installation Guide

### [Before you begin](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#before-you-begin)

- A compatible Linux host.
- 2 GB or more of RAM per machine.
- 2 CPUs or more.
- Full network connectivity between all machines in the cluster (public or private network is fine).
- Unique hostname, MAC address, and product_uuid for every node. See here for more details.
- Certain ports are open on your machines. See [here](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#check-required-ports) for more details.
- Swap disabled. You **MUST** disable swap in order for the kubelet to work properly.
  - For example, `sudo swapoff -a` will disable swapping temporarily. To make this change persistent across reboots, make sure swap is disabled in config files like /etc/fstab, systemd.swap, depending how it was configured on your system.
- Installing a container runtime
  - To run containers in Pods, Kubernetes uses a container runtime.
  - By default, Kubernetes uses the Container Runtime Interface (CRI) to interface with your chosen container runtime.
  - ## related issue #4581 [Kubeadm unknown service runtime.](https://github.com/containerd/containerd/issues/4581)
    - `kubeadm init` shows error below
    ```
    [preflight] Running pre-flight checks
      error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR CRI]: container runtime is not running: output: ...
    ```

## [安裝 kubeadm、kubelet、kubectl 工具](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#installing-kubeadm-kubelet-and-kubectl)

- `kubeadm` : the command to bootstrap the cluster.
- `kubelet` : the component that runs on all of the machines in your cluster and does things like starting pods and containers.
- `kubectl` : the command line util to talk to your cluster.

## [Creating a cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

```
kubeadm init
```

## 安裝 Minikube (Optional)

- [安裝 minikube](https://minikube.sigs.k8s.io/docs/start/)
- Minikube 是由 Google 發布的一個輕量級工具。讓開發者可以在本機上輕易架設一個 Kubernetes Cluster，快速上手 Kubernetes 的指令與環境
- [移除 minikube](https://stackoverflow.com/questions/66016567/how-to-uninstall-minikube-from-ubuntu-i-get-an-unable-to-load-cached-images-e)

```
sudo dpkg --purge minikube
```

## Docker

- [install docker](https://docs.docker.com/desktop/install/debian/)
- [如果 docker daemon 未啟動](https://docs.docker.com/config/daemon/start/)

  ```
  sudo systemctl start docker
  ```

## 在 minikube 啟動時遇到 docker permission denied

- 官方文件中提及 docker daemon always runs as root
- 在安裝 docker 時就已創立了一個 group 叫 docker, 所以將 mis 加入 docker group

  ```
  sudo usermod -aG docker mis
  ```

- 加入後以群組是 docker 的 mis 再次登入

  ```
  newgrp docker
  ```

## pull from docker hub

- login docker first

  ```
  docker login
  ```

- create secret form config.json
- .docker/config.json usually locate at home directory

  ```
  kubectl create secret docker-registry <your secret name> --from-file=.dockerconfigjson=/path/to/.docker/config.json
  ```

## Deployment

- json or yaml formats are accepted

  ```
  kubectl apply -f path/to/filename.json | filename.yaml
  ```

## [kubectl commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-)

<table>
<tr><td>Deployment相關指令</td><td>指令功能</td></tr>
<tr><td>kubectl get deployments</td><td>取得目前Kubernetes中的deployments的資訊</td></tr>
</table>

## update image

- Update existing container image(s) of resources.
- pod (po), replicationcontroller (rc), deployment (deploy), daemonset (ds), statefulset (sts), cronjob (cj), replicaset
  (rs)
- example below is updating your image by deployment
  ```
  kubectl set image deploy/<your depolyment name> <your container name>=<your new image tag>
  ```
- check rollout status
  ```
  kubectl rollout status deployment/<your depolyment name>
  ```
