# vSphere with Tanzu Quick Start Demo

## Log in to Supervisor cluster

```sh
export SC_IP=10.198.52.128
export NAMESPACE=myles
kubectl vsphere login --server=https://$SC_IP --vsphere-username administrator@vsphere.local --insecure-skip-tls-verify
```

### Set kubectl context to be the supervisor cluster

```sh
kubectl config use-context $NAMESPACE-$SC_IP
```

## Deploy TKG Service cluster if you haven't already

```sh
kubectl apply -f https://raw.githubusercontent.com/mylesagray/vsphere-with-tanzu-quick-start/master/manifests/tkc.yaml
```

## Login to TKG Service cluster

```sh
kubectl vsphere login --server=$SC_IP --tanzu-kubernetes-cluster-name tkc-1 --tanzu-kubernetes-cluster-namespace $NAMESPACE --vsphere-username administrator@vsphere.local --insecure-skip-tls-verify
```

### Use the TKG cluster context

```sh
kubectl config use-context tkc-1
```

## Deploy a workload

### Deploy Kubernetes Up and Running Demo

```sh
kubectl run --restart=Never --image=gcr.io/kuar-demo/kuard-amd64:blue kuard
```

#### Verify deployment

```sh
kubectl get pods
```

#### Access Deployment

```sh
kubectl port-forward kuard 8080:8080
```

##### Access in your browser

```sh
open http://localhost:8080
```
