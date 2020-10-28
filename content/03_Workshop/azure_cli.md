+++
title = "Azure CLI"
date =  2020-10-19T15:02:42-07:00
weight = 5
+++

Open the Azure Cloud Shell and sign in with your account. Select the Bash version of Azure Cloud Shell.

{{% button href="https://shell.azure.com" %}}Azure Cloud Shell{{% /button %}}

We need to create some Bash variables for the values that we will be using throughout the workshop. If you select a different value, remember it for the rest of the exercises in this workshop. Run the following commands to record these values in Bash variables.

```bash
REGION_NAME=westus
RESOURCE_GROUP=jfrog-aks-workshop
SUBNET_NAME=aks-subnet
VNET_NAME=aks-vnet
```

At any point, the ```echo``` command can be used to show the value of a variable.

```bash
echo $RESOURCE_GROUP
```

![azure_cli](/images/azure_cli.png)
