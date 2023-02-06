---
weight: 1
title: "Docker and Kubernets"
date: 2020-03-06T21:29:01+08:00
lastmod: 2020-03-06T21:29:01+08:00
draft: false
author: "Sharad"
authorLink: "https://sharadsingh.net"
description: "Docker, kubernets ,AKS, EKS, ECS etc"
# resources:
# - name: "featured-image"
#   src: "featured-image.webp"
# - name: "featured-image-preview"
#   src: "featured-image-preview.webp"

tags: ["docker", "kubernets","container", "microservice"]
categories: ["documentation"]

lightgallery: true

toc:
  auto: false
---


## Docker

### Install Docker
#### Install Docker: Windows
Use the following URL and download the installation file:
https://hub.docker.com/editions/community/docker-ce-desktop-windows

#### Install Docker: Linux
Use the following URL and download the installation file:
https://hub.docker.com/editions/community/docker-ce-desktop-windows

#### Install Docker: Mac
Use the following URL and download the installation file:
https://hub.docker.com/editions/community/docker-ce-desktop-windows

##### Commands

  $ docker version // docker version
  

## Kubernetes
### Install KubeCtl

Reference: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html


#### Primary scalar types

* Create Cluster
```
eksctl create cluster --name=eksdemo1 --region=us-east-1 --zones=us-east-1a,us-east-1b --without-nodegroup 
```

* Get List of clusters
```
eksctl get cluster 
```  


#### Step-02: Create & Associate IAM OIDC Provider for our EKS Cluster
To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create & associate OIDC identity provider.
To do so using eksctl we can use the below command.
Use latest eksctl version (as on today the latest version is 0.21.0)

**Template**
```
eksctl utils associate-iam-oidc-provider \
    --region region-code \
    --cluster <cluter-name> \
    --approve
```

 Replace with region & cluster name
 ```
eksctl utils associate-iam-oidc-provider   --region us-east-1   --cluster eksdemo1   --approve
```


###### Step-03: Create EC2 Keypair
Create a new EC2 Keypair with name as kube-demo
This keypair we will use it when creating the EKS NodeGroup.
This will help us to login to the EKS Worker Nodes using Terminal.
Step-04: Create Node Group with additional Add-Ons in Public Subnets
These add-ons will create the respective IAM policies for us automatically within our Node Group role.
# Create Public Node Group   
eksctl create nodegroup --cluster=eksdemo1 \
                       --region=us-east-1 \
                       --name=eksdemo1-ng-public1 \
                       --node-type=t3.medium \
                       --nodes=2 \
                       --nodes-min=2 \
                       --nodes-max=4 \
                       --node-volume-size=20 \
                       --ssh-access \
                       --ssh-public-key=kube-demo \
                       --managed \
                       --asg-access \
                       --external-dns-access \
                       --full-ecr-access \
                       --appmesh-access \
                       --alb-ingress-access 


 eksctl create nodegroup --cluster=eksdemo1    --region=us-east-1  --name=eksdemo1-ng-public1                       --node-type=t3.medium  --nodes=2  --nodes-min=2 --nodes-max=4 --node-volume-size=20 --ssh-access                        --ssh-public-key=ekc-ecs-demo-2022 --managed --asg-access --external-dns-access --full-ecr-access                       --appmesh-access --alb-ingress-access 

Step-05: Verify Cluster & Nodes

# List EKS clusters
eksctl get cluster

# List NodeGroups in a cluster
eksctl get nodegroup --cluster=<clusterName>

# List Nodes in current kubernetes cluster
kubectl get nodes -o wide

# Our kubectl context should be automatically changed to new cluster
kubectl config view --minify


## AKS (Azure Kubernetes Service)





1. Create a resource group
```bash
az group create --name devopresources --location westeurope    
```     
2. Create ACR (Azure container repository)        
```bash
az acr create --resource-group devopresources --name devopsshoppingacr --sku Basic
```
3. Enable admin access on the ACR repor        

        


```bash
az acr update --resource-group devopresources --n devopsshoppingacr --admin-enabled true
```



## 1 Requirements
eyteyhdhgh
Thanks to the simplicity of Hugo, [Hugo](https://gohugo.io/) is the only dependency of this theme.

Just install latest version of [:(far fa-file-archive fa-fw): Hugo (> 0.84.0)](https://gohugo.io/getting-started/installing/) for your OS (**Windows**, **Linux**, **macOS**).

{{< admonition note "Why not support earlier versions of Hugo?" >}}
Since [Markdown Render Hooks](https://gohugo.io/getting-started/configuration-markup#markdown-render-hooks) was introduced in the [Hugo Christmas Edition](https://gohugo.io/news/0.62.0-relnotes/) and some of image resources are using webp which was introduced in [0.84.0](https://github.com/gohugoio/hugo/releases/tag/v0.84.0), this theme only supports Hugo versions above **0.84.0**.
{{< /admonition >}}

{{< admonition tip "Hugo extended version is recommended" >}}
Since some features of this theme need to processes :(fab fa-sass fa-fw): SCSS to :(fab fa-css3 fa-fw): CSS, it is recommended to use Hugo **extended** version for better experience.
{{< /admonition >}}

## 2 Installation

The following steps are here to help you initialize your new website. If you don’t know Hugo at all, we strongly suggest you learn more about it by following this [great documentation for beginners](https://gohugo.io/getting-started/quick-start/).

### 2.1 Create Your Project

Hugo provides a `new` command to create a new website:

```bash
hugo new site my_website
cd my_website
```

testigggg