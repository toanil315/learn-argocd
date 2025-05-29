# 📦 Create a Cluster with 1 Master and 2 Workers

## Create a configuration file kind-cluster.yaml:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

## Then create the cluster:

```bash
kind create cluster --name dev-cluster --config kind-cluster.yml
```

This will create:
1 control-plane (master) node
2 worker nodes
All nodes run as Docker containers on your macOS system.

## ✅ Verify Cluster

```bash
kubectl cluster-info --context kind-dev-cluster
kubectl get nodes
```

```bash
NAME STATUS ROLES AGE VERSION
dev-cluster-control-plane Ready control-plane Xs v1.29.X
dev-cluster-worker Ready <none> Xs v1.29.X
dev-cluster-worker2 Ready <none> Xs v1.29.X
```

## 🔄 Cleanup

```bash
kind delete cluster --name dev-cluster
```
