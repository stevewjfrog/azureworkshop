+++
title = "AKS Cluster Connectivity"
date =  2020-10-19T15:01:56-07:00
weight = 5
+++

Retrieve the cluster credentials.

```bash
az aks get-credentials \
    --resource-group $RESOURCE_GROUP \
    --name $AKS_CLUSTER_NAME
```

List the nodes in the AKS cluster.

```bash
kubectl get nodes
```
This should return the name and status for the 2 nodes in the AKS cluaster you created.

![azure_nodes_1](/images/azure_nodes_1.png)
