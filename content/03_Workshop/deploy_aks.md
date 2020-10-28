+++
title = "Deploy an AKS cluster"
date =  2020-10-19T15:01:57-07:00
weight = 5
+++

With the new virtual network in place, you can go ahead and create your new cluster. There are two values you need to know before running the ```az aks create``` command. The first is the version of the latest, non-preview, Kubernetes version available in your selected region, and the second is a unique name for your cluster.

To get the latest, non-preview, Kubernetes version you use the ```az aks get-versions``` command. Store the value that returns from the command in a Bash variable named ```VERSION```. Run the command below the retrieve and store the version number.

```bash
VERSION=$(az aks get-versions \
    --location $REGION_NAME \
    --query 'orchestrators[?!isPreview] | [-1].orchestratorVersion' \
    --output tsv)
```

The AKS cluster name must be unique. Run the following command to create a Bash variable that holds a unique name.

```bash
AKS_CLUSTER_NAME=jfrog-aks-workshop-$RANDOM
```
Run the following command to output the value stored in ```$AKS_CLUSTER_NAME```. Note this for later use. You'll need it to reconfigure the variable in the future, if necessary.

```bash
echo $AKS_CLUSTER_NAME
```

Run the following ```az aks create``` command to create the AKS cluster running the latest Kubernetes version. This command can take a few minutes to complete.

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

Let's review the variables in the previous command:

* ```$AKS_CLUSTER_NAME``` specifies the name of the AKS cluster.
* ```$VERSION``` is the latest Kubernetes version you retrieved earlier.
* ```$SUBNET_ID``` is the ID of the subnet created on the virtual network to be configured with AKS.

Note the following deployment configuration:

* ```--vm-set-type```: We're specifying that the cluster is created by using virtual machine scale sets. The virtual machine scale sets enable you to switch on the cluster autoscaler when needed.

* ```--node-count```: We're specifying that the cluster is created with two nodes. The default node count is three nodes. However, if you're running this exercise using a free trial account, cluster creation may fail due to quota limits if left at the default setting.

* ```--network-plugin```: We're specifying the creation of the AKS cluster by using the CNI plug-in.

* ```--service-cidr```: This address range is the set of virtual IPs that Kubernetes assigns to internal services in your cluster. The range must not be within the virtual network IP address range of your cluster. It should be different from the subnet created for the pods.

* ```--dns-service-ip```: The IP address is for the cluster's DNS service. This address must be within the Kubernetes service address range. Don't use the first IP address in the address range, such as 0.1. The first address in the subnet range is used for the kubernetes.default.svc.cluster.local address.

* ```--docker-bridge-address```: The Docker bridge network address represents the default docker0 bridge network address present in all Docker installations. AKS clusters or the pods themselves don't use docker0 bridge. However, you have to set this address to continue supporting scenarios such as docker build within the AKS cluster. It's required to select a classless inter-domain routing (CIDR) for the Docker bridge network address. If you don't set a CIDR, Docker chooses a subnet automatically. This subnet could conflict with other CIDRs. Choose an address space that doesn't collide with the rest of the CIDRs on your networks, which includes the cluster's service CIDR and pod CIDR.
