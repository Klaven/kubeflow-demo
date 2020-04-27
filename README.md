# kubeflow-demo
Just a handful of demo deployment tools designed to be used on top of SUSE CaaSP deployments

## Requirements:
A running kubernetes cluster. while this *should* work on any cluster. it has not been tested on any other cluster then a SUSE CaaSP cluster. If you test it on another cluster please let me know how it goes!

### Usage

Pre-requirements:
1. CaaSP Kubernetes Cluster with attached dynamic (and default) storage
 - quick and dirty local storage (Not a supported solution ever), this gives local-path the `suse.caasp.psp.privileged` and is not recommended for production.
`kubectl apply -f https://raw.githubusercontent.com/Klaven/kubeflow-demo/master/local-path.yaml`
`kubectl patch storageclass local-path -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'`
2.  SYS_PTRACE is needed for pns && NET_RAW and NET_ADMIN enabled for notebook creation. at this time


Install:
follow the steps 1 & 2 from https://www.kubeflow.org/docs/started/k8s/kfctl-k8s-istio/
export CONFIG_URL=" https://raw.githubusercontent.com/SUSE/manifests/v1.0-branch-caasp/kfdef/kfctl_caasp.yaml"
continue following https://www.kubeflow.org/docs/started/k8s/kfctl-k8s-istio/#set-up-and-deploy-kubeflow
 - if you would like to make further edits to your deployment before deployment follow https://www.kubeflow.org/docs/started/k8s/kfctl-k8s-istio/#alternatively-set-up-your-configuration-for-later-deployment


GPUs: 
GPUs can be used with OCI hooks.

Exposing:
Istio is used. If you are in a environment that provides load balances one should be created for you and should expose the service though that. If you are on baremetal/KVM installation, you can use this file to expose it via the node port though this is hacky as it assume DNS is not set up.

kubectl apply -f https://raw.githubusercontent.com/Klaven/kubeflow-demo/master/istio-kubeflow-node-port.yaml
