---
title: "Azure"
date: 2022-03-09
thumbnail: "img/placeholder.png"
menu:
  main:
    name: Azure
    weight: 10
tags:
  - "Cloud"
  - "Azure"
  - "Exam" 
  - "AZ-104" 

categories:
  - "Azure" 
  - "Cloud" 
menu: main
---


### Azure Core Concepts

#### IAAS
#### PAAS
#### FAAS

### Azure Compute
Azure compute is an on-demand computing services for running cloud based applications.
<!--more-->

* Azure Virtual Machines
* Azure Container Instances
* Azure App Service
* Azure Functions (or serverless computing)



#### Azure Virtual Machines (VMs)

Virtual Machines are virtual computer systems. They include 
* Virtual processor 
* Memory
* Storage
* Networking resources
VMs host an opertaing system, and we can install and run softwares on the VMs just like a physical computer.
VMs provide IaaS (infrastructure as a service).

#### Storage
 * OS Disk
 * Data Disk
 * Temporary Disk (instance)
 * Unmanaged vs managed
 #### Operating System
 * Windows
 * Linux
 #### Connections to VMs
 * RDP
 * SSH

 



### Region
------
OS
Type (OS Only)
Tier (Standered)
Category ( General Purpose | Compute Optimized)
Instance Series
Instance
Number of VM



#### Virtual machine scale sets
 Virtual machine scale sets are like image  of an operating system




### Eventhub

* Configure resource group and location.
```
az configure --defaults group=[sandbox Resource Group] location=westus2
```
* Create Eventhub namespace
```
az eventhubs namespace create --name $NS_NAME
```
* Fetch authorization key and connectionstring
```
az eventhubs namespace authorization-rule keys list \
    --name RootManageSharedAccessKey \
    --namespace-name $NS_NAME
```


* Create Eventhub
```
az eventhubs eventhub create --name $HUB_NAME --namespace-name $NS_NAME
```
* Show eventhub
```
az eventhubs eventhub show --namespace-name $NS_NAME --name $HUB_NAME
```
Connecting to eventhub
** To Publishing Message**
Following eventhub details are required for sending event to eventhub:

1. Event hub namespace name
2. Event hub name
3. Shared access policy name
4. Primary shared access key


** Receive messages from an Event Hub**

Following eventhub details are required:

1. Event hub namespace name
2. Event hub name
3. Shared access policy name
4. Primary shared access key
5. Storage account name
6. Storage account connection string
7. Storage account container name



```
az storage account create --name $STORAGE_NAME --sku Standard_RAGRS --encryption-service blob
```
Retrieve the storage account key.
```
az storage account keys list --account-name $STORAGE_NAME
```
Retrieve the connection string for an Azure Storage account.
```
az storage account show-connection-string -n $STORAGE_NAME
```
Creates a new container in a storage account.
```
az storage container create --name messages --connection-string "<connection string here>"
```