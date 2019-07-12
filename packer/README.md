# Build Kubernetes Box

## Quick start

```
export BOX_VERSION=`date +%Y%m%d.0`
export BOX_NAME="labarhack/kubernetes_${BOX_VERSION}"
packer build -var-file=bionic64.json ubuntu.json
vagrant box add output-vagrant/package.box --name $BOX_NAME
```
