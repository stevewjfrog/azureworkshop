+++
title = "AKS Cluster Connectivity"
date =  2020-10-19T15:01:56-07:00
weight = 5
+++

kubectl is the main Kubernetes command-line client you use to interact with your cluster and is available in Cloud Shell. A cluster context is required to allow kubectl to connect to a cluster. The context contains the cluster's address, a user, and a namespace. Use the az aks get-credentials command to configure your instance of kubectl.

Retrieve the cluster credentials by running the command below.

```bash
az aks get-credentials \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_CLUSTER_NAME
```

Let's take a look at what was deployed by listing all the nodes in your cluster. Use the kubectl get nodes command to list all the nodes.

```bash
kubectl get nodes
```

You'll see a list of your cluster's nodes. Here's an example.

```bash
NAME                                STATUS   ROLES   AGE  VERSION
aks-nodepool1-29333311-vmss000000   Ready    agent   2m36s   v1.17.9
aks-nodepool1-29333311-vmss000001   Ready    agent   2m34s   v1.17.9
```
