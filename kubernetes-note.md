## 安裝 kubectl 工具

- [安裝 kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management)
- The Kubernetes command-line tool, [kubectl](https://kubernetes.io/docs/reference/kubectl/kubectl/), allows you to run commands against Kubernetes clusters. You can use kubectl to deploy applications, inspect and manage cluster resources, and view logs.

## 安裝 Minikube

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

## Deployments

### list all deployments

```
kubectl get deployments --all-namespaces
```

### delete the deployment

- 如果 namespaces 是 default 不用加-n NAMESPACE

  ```
  kubectl delete -n NAMESPACE deployment DEPLOYMENT
  ```

## Pods

### create pod

- create pod by file, json or yaml formats are accepted

  ```
  kubectl create -f path/to/filename.json | filename.yaml
  ```

### pod detail

- show pod detail

  ```
  kubectl describe pod <pod name>
  ```

- show pods and labels

  ```
  kubectl get pods --show-labels
  ```

### pull from docker hub

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

### create deployment

- json or yaml formats are accepted

  ```
  kubectl apply -f path/to/filename.json | filename.yaml
  ```

### deployments commands

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
