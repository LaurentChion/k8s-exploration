# k8s-exploration
Some notes about [Kubernetes](https://kubernetes.io/) and more:
- [Minikube](https://minikube.sigs.k8s.io/)
- [Helm](https://helm.sh/)


## Techno definitions:

[Terraform](https://www.terraform.io/): Infrastructure as Code to provision and manage any cloud, infrastructure, or service.

[Minikube](https://minikube.sigs.k8s.io/): It's an easy installation of k8s using a VM.

[Rancher Kubernetes Engine](https://rancher.com/an-introduction-to-rke/): Easy way to deploy k8s infrasturcture

[Helm](https://helm.sh/): It's a "package manager" for k8s.

## Setup:
- install a k8s cluster with [kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/) (recommended) or [minikube](https://minikube.sigs.k8s.io/docs/start/linux/)
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

## Additional resources:
- [Terraform-rke plugin](https://github.com/rancher/terraform-provider-rke)
- [Tuto RKE/Terraform](https://medium.com/@brotandgames/deploy-a-kubernetes-cluster-using-terraform-and-rke-provider-68112463e49d)