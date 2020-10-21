+++
title = "Configure Networking"
date =  2020-10-19T15:01:58-07:00
weight = 5
+++

Create a virtual network. What is the purpsoe of the network resource.

```bash
az network vnet create \
    --resource-group $RESOURCE_GROUP \
    --location $REGION_NAME \
    --name $VNET_NAME \
    --address-prefixes 10.0.0.0/8 \
    --subnet-name $SUBNET_NAME \
    --subnet-prefixes 10.240.0.0/16
```

What did we configure.

Store the subnet ID as a Bash variable.

```bash
SUBNET_ID=$(az network vnet subnet show \
    --resource-group $RESOURCE_GROUP \
    --vnet-name $VNET_NAME \
    --name $SUBNET_NAME \
    --query id -o tsv)
```
