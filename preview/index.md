# 

Preview
03:05
Code for the course
00:28
Support for Apple M1 users
00:30
Preview
09:34
Preview
02:49
Extra note for Linux Users
00:18
If you already have Docker installed...
01:41
Preview
07:16
Preview
03:34
Preview
06:42
Preview
02:46
Attention Apple M1 Users!
00:59
Preview
12:44
Preview
09:13
Writing a Pod
05:06
Running a Pod
10:54
Important note for Docker Desktop and Driver Users
00:52
Services
07:31
NodePort and ClusterIP
12:09
Pod Selection with Labels
15:02
Exercise: Deploy ActiveMQ as a Pod and Service
10:04
ReplicaSets
10:44
Writing a ReplicaSet
10:05
Applying a ReplicaSet to Kubernetes
10:54
Deployments Overview
12:08
Managing Rollouts
12:24
Networking Overview in Kubernetes
08:18
Namespaces - kube-system
09:34
Note for M1 Architectures
00:04
Accessing MySQL from a Pod
07:15
Cygwin extra - fixing the terminal with winpty
04:52
Service Discovery
07:27
Fully Qualified Domain Names (FQDN)
03:27
WARNING - possible resource problems!
00:50
An Introduction to Microservices
15:18
Introduction to Microservices Part 2
10:40
Deploying the Queue
12:38
Deploying the Position Simulator
07:56
Inspecting Pod Logs
05:40
Deploying the Position Tracker
11:07
Deploying the API Gateway
04:49
Deploying the Webapp
06:40
Persistence
12:00
Upgrading to a Mongo Pod
13:48
Mongo Service
06:22
Expanding the Minikube VM
02:50
Volume Mounts
09:26
Volumes
14:25
PersistentVolumeClaims
16:26
StorageClasses and Binding
09:24
Warning
00:34
Getting started with AWS
10:58
Managing a Cluster in the Cloud
09:12
EKS vs Kops - Which to Choose?
09:39
Pricing Differences - EKS vs Kops (prices correct mid 2020)
08:18
Choose Your Own Adventure!
00:24
This Section is for Kops!
00:10
Introducing Kops - Kubernetes Operations
10:15
Installing the Kops Environment - 2021 Update
18:39
Configuring your first cluster
20:04
Running the Cluster
14:03
This section is for EKS
00:07
Getting started with EKS
13:12
Install eksctl and AWS CLI
06:05
Configure the AWS credentials
13:24
Install kubectl
04:28
Start the cluster
04:29
This section is for both EKS and Kops
00:15
Provisioning SSD drives with a StorageClass
12:51
Warning - problems with AWS LoadBalancers
00:46
Note for Kops users
00:44
Deploying the Fleetman Workload to Kubernetes
13:17
Setting up a real Domain Name
04:02
Surviving Node Failure
10:09
Replicating Pods in Kubernetes
11:03
Deleting the Cluster
10:28
Preview
05:34
How to delete your EKS cluster
07:06
One last cluster deletion step
01:01
Preview
00:31
Introducing the ELK / ElasticStack
15:39
Installing the Stack to Kubernetes
16:06
Kibana - first look
09:01
Setting Filters and Refreshes
05:01
Preview
05:14
Kibana Dashboards
15:25
Monitoring a Cluster (2020 update)
05:31
Installing the kube-prometheus-stack
15:16
Use the "Classic UI" in the next video
00:07
Using the Prometheus UI
17:19
Introducing Grafana
21:52
(optional) How to Use NodePorts on a Cluster
17:29
Introducing Alerts - 2020 Update
11:46
Preparing a Slack Channel
10:15
Configuring the AlertManager
15:17
Troubleshoot the alertmanager.yaml config
16:40
Dealing with Firing Alerts
16:32
The AlertManager UI and how to Silence Alerts
09:24
How to handle the Watchdog
14:31
Using PagerDuty
17:11
Case Study
00:21
Case Study: Troubleshooting a "Delinquent" node
13:02
What happens if the Master Node crashes? (Kops clusters only!)
10:34
Preview
02:40
Code / files for this section
00:06
Memory requests
20:40
CPU Requests
07:05
Memory and CPU Limits
14:49
Enabling the Metrics Server
14:25
Viewing Metrics on the Dashboard
16:42
Tuning Java Spring Boot Applications, Heap restriction
22:52
Setting reasonable Requests
07:42
Update: you will need to modify the yaml file in the next video
00:26
Introducing Replication and Autoscaling
30:59
Testing Autoscaling
07:29
Demo: why readiness probes are needed
12:01
Applying Liveness and Readiness Probes
08:56
Understanding the scheduler
15:37
QoS labels
04:58
Evictions
12:03
Pod Priorities
12:40
Creating a ConfigMap
07:33
Consuming a ConfigMap as Environment Variables
05:29
Do changes to a ConfigMap get propagated?
06:37
How to consume multiple environments variables with envFrom
03:32
Mounting ConfigMaps as Volumes
09:18
Creating Secrets
08:11
Using Secrets
08:06
Where have we already used ConfigMaps and Secrets?
09:39
(extra) Using Spring Cloud Kubernetes to Hot Reload ConfigMaps
00:11
Introducing Ingress
12:07
Defining Routing Rules
15:20
Adding Routes
04:04
Authentication
15:11
Running Ingress on AWS
14:06
Testing the Ingress Rules
08:57
(Extra) setting up HTTPS with TLS termination at the load balancer
00:09
Batch Jobs
22:26
Cron Jobs
09:24
DaemonSets
06:24
StatefulSets Overview
22:21
StatefulSets for Database Replication
09:57
Demo: Scaling out a Mongo Database
21:38
Introducing CI/CD
11:12
Establishing a GitHub organization
10:44
Setting up a Basic Jenkins System
15:07
Defining a Pipeline
18:10
Update - creating a Personal Access Token from Github
01:28
Another minor update!
00:26
Running a Multibranch Pipeline
05:18
Reviewing Builds
10:20
Organization Pipelines
09:32
Continuous Deployment into a Cluster
16:17
Getting Started with Helm
09:21
How do I Install a Helm Chart
14:37
How to Find Helm Charts
10:48
Installing a Monitoring Stack with Helm
14:01
Working with Chart Values
16:14
Customising values.yaml
16:00
Avoiding Snowflake Clusters!
11:56
Using Helm Pull to Take Control of a Chart
16:51
Generating yaml with "Helm Template"
07:24
Why would you write your own Helm Charts?
10:06
Writing Go Templates for Helm
26:52
Helm Functions and Pipelines
14:19
Flow Control in a Helm Template
12:21
Named Templates
21:35
Inspecting a Professional Helm Chart
24:40
