# Create AKS Cluster

## Architecture Diagram

![AKS Cluster](https://learn.microsoft.com/en-us/azure/aks/media/concepts-clusters-workloads/control-plane-and-nodes.png)

## Azure Virtual Machines

![AKS Cluster - Azure Virtual Machines](https://learn.microsoft.com/en-us/azure/aks/media/concepts-clusters-workloads/aks-node-resource-interactions.png)

## AKS Cluster - Namespaces

![AKS Cluster - Azure Virtual Machines](https://learn.microsoft.com/en-us/azure/aks/media/concepts-clusters-workloads/namespaces.png)

---

### Creating AKS Cluster

- **Project Details**
  - **Subscription:** Free Trial
  - **Resource Group:** Create New Resource Group: aks-resource-group
  - **Kubernetes Cluster Name:** aks-cluster-mnm
  - **Region:** (US) Central US
  - **Kubernetes Version:** Latest stable version
  - **Node Count:** 1
- **Authentication**
  - Authentication method: System-assigned managed identity
- **Networking**
  - **Network Configuration:** Advanced
  - **Network Policy:** Azure

---

### Configure kubectl to connect to AKS Cluster using Azure Cloud Shell

```shell
az aks get-credentials --resource-group aks-resource-group --name aks-cluster-mnm

alias k=kubectl

k get nodes -o wide
k get all -A
```

---

### Deploy Nginx Web Server - Deployment and Service

```shell
k create ns testing-nginx

k create deploy test-nginx --image=nginx --replicas=3 -n testing-nginx
k describe deploy test-nginx -n testing-nginx

k expose deploy test-nginx --port=80 --type=LoadBalancer -n testing-nginx
k describe svc test-nginx -n testing-nginx

k get all -n testing-nginx
```
