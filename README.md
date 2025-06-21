## 📘 README: Install Kind and Create a 3-Node Kubernetes Cluster on Ubuntu

### 🧱 What is Kind?

**Kind (Kubernetes IN Docker)** is a lightweight tool to run Kubernetes clusters inside Docker containers. Perfect for **local development**, testing, and teaching.

---

## 🚀 Step 1: Prerequisites

Ensure docker is installed:
https://docs.docker.com/engine/install/ubuntu


Make sure your user has Docker permissions:

```bash
sudo usermod -aG docker $USER


## 📥 Step 2: Install Kind

# For AMD64 / x86_64
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-amd64
# For ARM64
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

Verify installation:

```bash
kind version
```

---

## ⚙️ Step 3: Create a 3-Node Cluster (1 Control Plane + 2 Workers)

### 1. Create a config file:

Create `kind-cluster.yaml`:

```yaml
# kind-cluster.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

### 2. Spin up the cluster:

```bash
kind create cluster --name my-cluster --config kind-cluster.yaml
```

---

## 🔍 Step 4: Verify Your Cluster

Check all nodes:

```bash
kubectl get nodes
```

Expected output:

```
NAME                 STATUS   ROLES           AGE     VERSION
my-cluster-control-plane   Ready    control-plane   Xs      vX.X.X
my-cluster-worker          Ready    <none>          Xs      vX.X.X
my-cluster-worker2         Ready    <none>          Xs      vX.X.X
```

---

## 🧼 Optional: Delete the Cluster

```bash
kind delete cluster --name my-cluster
```

---

## ✅ Useful Commands

```bash
kubectl cluster-info --context kind-my-cluster
kubectl get pods -A
docker ps  # See running Kind containers


