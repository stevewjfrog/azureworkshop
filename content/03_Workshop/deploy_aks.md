+++
title = "Deploy an AKS cluster"
date =  2020-10-19T15:01:57-07:00
weight = 5
+++

Determine the latest non-preview version of Kubernetes for the region in which you have created your resource group and store it as a Bash variable.

```bash
VERSION=$(az aks get-versions \
    --location $REGION_NAME \
    --query 'orchestrators[?!isPreview] | [-1].orchestratorVersion' \
    --output tsv)
```

create a unique AKS cluster name and save it as a Bash variable.

```bash
AKS_CLUSTER_NAME=jfrog-aks-workshop-$RANDOM
```

Create the AKS cluster. This may take a few minutes to deploy.

```bash
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER_NAME \
--vm-set-type VirtualMachineScaleSets \
--node-count 2 \
--load-balancer-sku standard \
--location $REGION_NAME \
--kubernetes-version $VERSION \
--network-plugin azure \
--vnet-subnet-id $SUBNET_ID \
--service-cidr 10.2.0.0/24 \
--dns-service-ip 10.2.0.10 \
--docker-bridge-address 172.17.0.1/16 \
--generate-ssh-keys
```
