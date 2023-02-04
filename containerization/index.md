# Docker And Kubernetes


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
  

* Create Cluster
eksctl create cluster --name=eksdemo1 --region=us-east-1 --zones=us-east-1a,us-east-1b --without-nodegroup 

* Get List of clusters
eksctl get cluster   


#### Step-02: Create & Associate IAM OIDC Provider for our EKS Cluster
To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create & associate OIDC identity provider.
To do so using eksctl we can use the below command.
Use latest eksctl version (as on today the latest version is 0.21.0)
# Template
eksctl utils associate-iam-oidc-provider \
    --region region-code \
    --cluster <cluter-name> \
    --approve

# Replace with region & cluster name
eksctl utils associate-iam-oidc-provider   --region us-east-1   --cluster eksdemo1   --approve


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

## Install KubeCtl

Reference: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html


#### Primary scalar types

* Create Cluster
eksctl create cluster --name=eksdemo1 --region=us-east-1 --zones=us-east-1a,us-east-1b --without-nodegroup 

* Get List of clusters
eksctl get cluster   


#### Step-02: Create & Associate IAM OIDC Provider for our EKS Cluster
To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create & associate OIDC identity provider.
To do so using eksctl we can use the below command.
Use latest eksctl version (as on today the latest version is 0.21.0)
# Template
eksctl utils associate-iam-oidc-provider \
    --region region-code \
    --cluster <cluter-name> \
    --approve

# Replace with region & cluster name
eksctl utils associate-iam-oidc-provider   --region us-east-1   --cluster eksdemo1   --approve


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


### ECR (Elastic Container registory)

URL https://aws.amazon.com/ecr/pricing/

//Create repo
aws ecr create-repository --repository-name demo-repository
// Delete repo
aws ecr delete-repository --repository-name demo-repository
<!--more-->
//Tag and Push image

docker tag amazonlinux:2 852051225911.dkr.ecr.us-west-1.amazonaws.com/deploy:amazonlinux2
docker push 852051225911.dkr.ecr.us-west-1.amazonaws.com/deploy:amazonlinux2

aws ecr get-login --region us-west-1 --no-include-email

// List repo
aws ecr list-images --repository-name demo-repository

This article describes fundamental building blocks of [Systems design][gosystemdesign], and will disscuss some of the common systems.

## Install KubeCtl

Reference: https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html


#### Primary scalar types

* Create Cluster
eksctl create cluster --name=eksdemo1 --region=us-east-1 --zones=us-east-1a,us-east-1b --without-nodegroup 

* Get List of clusters
eksctl get cluster   


#### Step-02: Create & Associate IAM OIDC Provider for our EKS Cluster
To enable and use AWS IAM roles for Kubernetes service accounts on our EKS cluster, we must create & associate OIDC identity provider.
To do so using eksctl we can use the below command.
Use latest eksctl version (as on today the latest version is 0.21.0)
# Template
eksctl utils associate-iam-oidc-provider \
    --region region-code \
    --cluster <cluter-name> \
    --approve

# Replace with region & cluster name
eksctl utils associate-iam-oidc-provider   --region us-east-1   --cluster eksdemo1   --approve


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
