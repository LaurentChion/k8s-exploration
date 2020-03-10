# k8s-exploration
Some notes about [Kubernetes](https://kubernetes.io/) and more:
- [Minikube](https://minikube.sigs.k8s.io/)
- [Helm](https://helm.sh/)


## Definition

[Minikube](https://minikube.sigs.k8s.io/): It's an easy installation of k8s using a VM.

[Helm](https://helm.sh/): It's a "package manager" for k8s.

## Setup:
- install [k8s (minikube)](https://minikube.sigs.k8s.io/docs/start/linux/)
- install [kubectl](https://kubernetes.io/fr/docs/tasks/tools/install-kubectl/)
- install [helm](https://helm.sh/docs/intro/install/)

- [Private repository configuration](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)

Example:
```
    kubectl create secret generic <repo-name> \
    --from-file=.dockerconfigjson=<path/to/.docker/config.json> \
    --type=kubernetes.io/dockerconfigjson
```

Editing global configuration: `kubectl edit serviceaccounts default`

- Adding secret
```yml
imagePullSecrets:
    # How to manage same secret name for different user ?
  - name: your-secret
```

- [multicluster management](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/) with kubectl


## Tools
- [K8s-dashboard](https://github.com/kubernetes/dashboard)
- [Cheatsheet](https://kubernetes.io/fr/docs/reference/kubectl/cheatsheet/)
- ZSH plugins:
    - [K8s](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/kubectl/kubectl.plugin.zsh)
    - [Helm](https://github.com/ohmyzsh/ohmyzsh/blob/master/plugins/helm/helm.plugin.zsh)


## Manual command line

Example:
- Deploy a container from docker image:
```sh
#kaf file.yml
kubectl apply -f file.yml
```
- Expose a deployment using a **service**:
```sh
kubectl expose deployment hello-node --type=LoadBalancer --port=8080
```