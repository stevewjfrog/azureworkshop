+++
title = "Resource Group"
date =  2020-10-19T15:01:59-07:00
weight = 5
+++

Create a new resource group with the name jfrog-aks-workshop. Deploy all resources created in these exercises in this resource group. A single resource group makes it easier to clean up the resources after you finish the module.

```bash
az group create \
    --name $RESOURCE_GROUP \
    --location $REGION_NAME
```
