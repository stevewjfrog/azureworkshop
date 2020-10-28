+++
title = "Configure Networking"
date =  2020-10-19T15:01:58-07:00
weight = 5
+++

We have two network models to choose from when deploying an AKS cluster. The first model is Kubenet networking, and the second is Azure Container Networking Interface (CNI) networking.

## What is Kubenet networking?

Kubenet networking is the default networking model in Kubernetes. With Kubenet networking, nodes get assigned an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes.

Network address translation (NAT) is then configured so that the pods can reach resources on the Azure virtual network. The source IP address of the traffic is translated to the node's primary IP address and then configured on the nodes. Note, that pods receive an IP address that's "hidden" behind the node IP.

## What is Azure Container Networking Interface (CNI) networking?

With Azure Container Networking Interface (CNI), the AKS cluster is connected to existing virtual network resources and configurations. In this networking model, every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be unique across your network space and calculated in advance.

Some of the features you'll use require you to deploy the AKS cluster by using the Azure Container Networking Interface networking configuration.

For a more detailed comparison, see the Learn more section at the end of this module.

Let's create the virtual network for your AKS cluster. We will use this virtual network and specify the networking model when we deploy the cluster.

First, create a virtual network and subnet. Pods deployed in your cluster will be assigned an IP from this subnet. Run the following command to create the virtual network.

```bash
az network vnet create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $VNET_NAME \
    --address-prefixes 10.0.0.0/8 \
    --subnet-name $SUBNET_NAME \
    --subnet-prefixes 10.240.0.0/16
```

Next, retrieve, and store the subnet ID in a Bash variable by running the command below.

```bash
SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNET_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
```
