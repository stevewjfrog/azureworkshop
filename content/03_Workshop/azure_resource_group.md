+++
title = "Resource Group"
date =  2020-10-19T15:01:59-07:00
weight = 5
+++

Create a new Azure Resource Group for this workshop.

```bash
az group create \
    --name $RESOURCE_GROUP \
    --location $REGION_NAME
```

This resource group will be the container for all of the resources we will need for the workshop.
