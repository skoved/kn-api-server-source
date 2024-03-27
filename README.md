# kn-api-server-source

A helm chart that installs knative-eventing and deploys an ApiServerSource follwing the
[Creating an ApiServerSource Object guide](https://knative.dev/docs/eventing/sources/apiserversource/getting-started/#creating-an-apiserversource-object)
from knative-eventing. The ApiServerSource is deployed in the `api-server-source` namespace by default. By default the ApiServerSource is listening for 
events in the `test` namespace.

To deploy and have ApiServerSource send clound events to a Channel use the `channel` branch of this repo.

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
  * If podman installed add the following alias to your .bashrc
  ```bash
  alias docker=podman
  ```
  * If docker installed run the following commands
  ```bash
  sudo usermod -aG docker $usermod
  ```
  ```bash
  newgrp docker
  ```
* Start minikube
```bash
minikube start --driver=kvm2
```
* Apply knative CRDs (Helm doesn't do a good job managing CRDs)
```bash
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.13.3/eventing-crds.yaml
```
```bash
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.13.3/eventing-core.yaml
```
```bash
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.13.3/in-memory-channel.yaml
```
```bash
kubectl apply -f https://github.com/knative/eventing/releases/download/knative-v1.13.3/mt-channel-broker.yaml
```

## Use the Chart

To deploy
```bash
helm install -g .
```

To see deployments from helm
```bash
helm ls
```

To remove the deployment
```bash
helm ls -q | awk '{print $1}' | xargs -I {} helm uninstall {}
```
This command assumes that the install of this chart is the first one listed by helm ls. If that is not the case change awk command to
```bash
awk '{print $<position number>}'
