
## 🧑‍🏫 **What is Kind (Kubernetes in Docker)?**

**Kind** is a tool for running **local Kubernetes clusters using Docker containers as nodes**. It is:

* Lightweight
* Easy to install
* Ideal for CI, testing, or local development
* Great for training students or setting up tutorials

---

## ✅ **What You Need**

Before you start:

### 🔧 Prerequisites:

* Docker installed and running ✅
* Go (optional, only for source builds)
* Ubuntu (WSL or native)
* `kubectl` installed
* Internet connection

---

## 📦 Step 1: Install Kind

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.22.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

✅ Check installation:

```bash
kind version
```

---

## 🚀 Step 2: Create a Cluster

```bash
kind create cluster --name dev-cluster
```

📌 This creates a 1-node Kubernetes cluster **inside a Docker container**.

Check with:

```bash
kubectl get nodes
```

---

## 🧠 Step 3: 

When you run `kind create cluster`:

* Docker starts a container that runs `kubelet`, `kubeadm`, and other components.
* A kubeconfig is generated and placed in `~/.kube/config` to point `kubectl` to this cluster.
* Kind uses a custom Docker network for the cluster.

---

## 🧪 Step 4: Deploy an App

```bash
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --port=80 --type=NodePort
kubectl get service nginx
```

To access the app:

```bash
kubectl port-forward svc/nginx 9090:80
```

Visit: `http://localhost:9090`

---

## 🔁 Step 5: Delete the Cluster

```bash
kind delete cluster --name dev-cluster
```

---

## 🧰 Optional: Create Multi-Node Cluster

Create a config file:

**`cluster.yaml`**

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: mini-cluster
nodes:
  - role: control-plane
  - role: worker
  - role: worker
```

Create the cluster:

```bash
kind create cluster --name multi-node --config cluster.yaml
```

Check:

```bash
kubectl get nodes
```

---

## 🧩 Common Commands Cheat Sheet

| Task                   | Command                                  |
| ---------------------- | ---------------------------------------- |
| Create cluster         | `kind create cluster --name dev`         |
| Delete cluster         | `kind delete cluster --name dev`         |
| List nodes             | `kubectl get nodes`                      |
| Port forward a service | `kubectl port-forward svc/myapp 8080:80` |
| View Docker containers | `docker ps`                              |
| Multi-node config      | Use `--config` with a YAML file          |


