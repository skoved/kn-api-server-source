# kn-api-server-source

A helm chart that installs knative-eventing and deploys an ApiServerSource follwing the
[Creating an ApiServerSource Object guide](https://knative.dev/docs/eventing/sources/apiserversource/getting-started/#creating-an-apiserversource-object)
from knative-eventing. The ApiServerSource is deployed in the `api-server-source` namespace by default.

## Requirements

* Helm must be installed. Installation instructions for helm can be found [here](https://helm.sh/docs/intro/install/)
* Follow the instructions for verifying image signatures for knative-eventing [here](https://knative.dev/docs/install/yaml-install/eventing/install-eventing-with-yaml/#verifying-image-signatures)
* On linux make sure that you have kvm virtualization installed and running. On fedora/rhel run
```bash
sudo dnf install @virtualization
```
```bash
sudo systemctl enable --now libvirtd
```
```bash
sudo usermod -aG libvirt $USER
```
```bash
newgrp libvirt
```
* Be logged into a kubernetes cluster. If you don't have a cluster, installation instructions for minikube can be found [here](https://minikube.sigs.k8s.io/docs/start/)
* If using minikube on linux, docker or podman must be installed. On fedora/rhel run
```bash
sudo dnf install (podman|docker)
```
  * if podman installed add the following alias to your .bashrc
  ```bash
  alias docker=podman
  ```
  * if docker installed run the following commands
  ```bash
  sudo usermod -aG docker $usermod
  ```
  ```bash
  newgrp docker
  ```
* start minikube
```bash
minikube start --driver=kvm2
```

## Use the Chart

To deploy
```bash
helm install <a string with no spaces> .
```

To remove the deployment
```bash
helm uninstall <string from the install command>
```
