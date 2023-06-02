# Kubernetes Autoscaler

## What's inside

[Cluster Autoscaler](https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler) - a component that automatically adjusts the size of a Kubernetes
Cluster so that all pods have a place to run and there are no unneeded nodes. Supports several public cloud providers. Version 1.0 (GA) was released with kubernetes 1.8.

## Build the docker image for Hasty/Inference Engine purposes

This is an example for releasing and building the autoscaler for kubenetes v1.22.


### Preparing the release with vgpu support
```
git checkout cluster-autoscaler-release-1.22
git checkout -b cluster-autoscaler-release-1.22-vgpu-support
git commit -m 'Supporting vgpu'
# Merge the resulting PR
git pull origin master
git tag cluster-autoscaler-1.22.2-vgpu-support
git push -u origin cluster-autoscaler-1.22.2-vgpu-support
# Do the official release via github
```

### Building and pushing the container
```
TAG=v1.22.2-vgpu-patched REGISTRY=hastyai make clean build make-image
docker tag hastyai/cluster-autoscaler-amd64:v1.22.2-vgpu-patched hastyai/cluster-autoscaler:v1.22.2-vgpu-patched
docker push hastyai/cluster-autoscaler:v1.22.2-vgpu-patched
```

