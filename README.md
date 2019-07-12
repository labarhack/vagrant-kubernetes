# Vagrant Nomad cluster
[![Open Source Helpers](https://www.codetriage.com/labarhack/vagrant-kubernetes/badges/users.svg)](https://www.codetriage.com/labarhack/vagrant-kubernetes)

Start Kubernetes cluster with single master.

## Prerequisites

* VirtualBox Version 6.0
* Vagrant 2.2.5
* Ansible 2.8.1

## Setup

```
export KUBE_NODE_COUNT=1 # default: 1
```
## Build vagrant box

See [README](packer/README.md) to build box with packer.
```
export BOX_NAME='labarhack/kubernetes_20190712.0'
```

## Start vagrant

```
vagrant up
vagrant status
```

## Test

```
vagrant ssh kube_master_1
kubectl get nodes
```
