+++
title = "Azure CLI"
date =  2020-10-19T15:02:42-07:00
weight = 5
+++

Open the Azure Cloud Shell and sign in with your account. Select the Bash version of Azure Cloud Shell.

{{% button href="https://shell.azure.com" %}}Azure Cloud Shell{{% /button %}}

Create the bash variables for the values that we will be using throughout the workshop.

```bash
REGION_NAME=westus
RESOURCE_GROUP=jfrog-aks-workshop
SUBNET_NAME=aks-subnet
VNET_NAME=aks-vnet
```

At any point, echo can be used to show the value of a variable.


![azure_cli](/images/azure_cli.png)
