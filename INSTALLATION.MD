# Installation report

### Requirements  

- Environment from this [list](https://github.com/dell/csi-baremetal-operator#supported-environments)
- [go v1.16](https://go.dev/doc/install)
- [lvm2](https://www.debuntu.org/how-to-install-ubuntu-on-lvm-partitions/) packet installed on host machine
- [kubectl v1.16+](https://kubernetes.io/ru/docs/tasks/tools/install-kubectl/)
- [helm v3](https://helm.sh/docs/intro/install/)
- [docker](https://docs.docker.com/engine/install/ubuntu/)
- 30-35 GB free space at root (`df -h` to check)

## Installation
1. Be sure that you have installed all [requirements](#Requirements)
2. Clone [csi-baremetal](https://github.com/dell/csi-baremetal) repository   
`git clone https://github.com/dell/csi-baremetal.git`  
3. Clone [csi-baremetal-operator](https://github.com/dell/csi-baremetal-operator) repository  
`git clone https://github.com/dell/csi-baremetal-operator.git`
4. Create all variables at `~/.bashrc` or (and better)`/etc/profile` (for all users including root) which exports in this [guide](https://github.com/dell/csi-baremetal/blob/4a0fe85e2c0994c61d05bc664605ce6ae9713f5a/docs/CONTRIBUTING.md#build)
5. Follow this [guide](https://github.com/dell/csi-baremetal/blob/4a0fe85e2c0994c61d05bc664605ce6ae9713f5a/docs/CONTRIBUTING.md#build). Some commands need to be executed with sudo (`su -` (if not working `sudo -s`)) privileges. Be careful when executing this command  
`make load-operator-image OPERATOR_VERSION=${CSI_OPERATOR_VERSION} REGISTRY=${REGISTRY}`  
You will take an error. Here you should comment out `58` line of `Makefile.validation` and execute again
6. [Validate](https://github.com/dell/csi-baremetal/blob/4a0fe85e2c0994c61d05bc664605ce6ae9713f5a/docs/CONTRIBUTING.md#validation) your installed driver. Reduce number of replicas from `4` to `3` in `tests/app/nginx.yaml`. Original guide have a **typo**. Use this command instead of similar  
`kubectl apply -f tests/app/nginx.yaml`
7. Check all pods are Running and Ready  
`kubectl get pods`  
and all PVCs are Bound  
`kubectl get pvc`  
**_P.S._** If you have some errors when you follow this guide be sure that all variables are exported (in `root` environment too)
