# kn-api-server-source

A helm chart that installs knative-eventing and deploys an ApiServerSource

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
* If using minikube on linux, start minikube with
```bash
minikube start --driver=kvm2
```

## Use the Chart

To deploy
```bash
helm install <a string with no spaces> ./kn-api-server-source
```

To remove the deployment
```bash
helm uninstall <string from the install command>
```
