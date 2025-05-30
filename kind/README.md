# Create the K8s cluster

## Create
### Create the K8s cluster with kind

```console
❯ source .envrc

❯ cd kind

❯ kind create cluster --config config.yaml
Creating cluster "cloudnative-netbox-poc" ...
 ✓ Ensuring node image (kindest/node:v1.33.1) 🖼
 ✓ Preparing nodes 📦 📦 📦 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
 ✓ Joining worker nodes 🚜
Set kubectl context to "kind-cloudnative-netbox-poc"
You can now use your cluster with:

kubectl cluster-info --context kind-cloudnative-netbox-poc

Have a nice day! 👋
```

### Check the K8s cluster is created and ready

```console
❯ export KUBECONFIG=$(mktemp) && kind get kubeconfig --name cloudnative-netbox-poc > "$KUBECONFIG"

❯ kubectl get nodes
NAME                                   STATUS   ROLES           AGE     VERSION
cloudnative-netbox-poc-control-plane   Ready    control-plane   4m52s   v1.33.1
cloudnative-netbox-poc-worker          Ready    <none>          4m39s   v1.33.1
cloudnative-netbox-poc-worker2         Ready    <none>          4m39s   v1.33.1
cloudnative-netbox-poc-worker3         Ready    <none>          4m39s   v1.33.1
```

## Delete
### Delete the k8s cluster with kind

```console
❯ kind delete cluster --name cloudnative-netbox-poc
Deleting cluster "cloudnative-netbox-poc" ...
Deleted nodes: ["cloudnative-netbox-poc-worker3" "cloudnative-netbox-poc-control-plane" "cloudnative-netbox-poc-worker2" "cloudnative-netbox-poc-worker"]
```
