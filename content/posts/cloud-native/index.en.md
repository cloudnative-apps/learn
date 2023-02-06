---
title: "12 Factor Principles of Cloudnative Apps "
date: 2022-03-12
thumbnail: "img/placeholder.png"
# tags:
#   - "Cloud"
#   - "Cloud Native"
#   - "12 Factor App" 
#   - "Cloud App"
#   - "Cloud Migrations"
author: "Sharad"
authorLink: "https://sharadsingh.net"
categories: ["Cloud Native","Design Principles"]
  # - "Cloud Native" 
  # - "Design Principles" 
#menu: main
tags: ["Cloud", "Cloud Native","12 Factor App", "Cloud App"]
---






### 12-factor app principles

1.  **Codebase**: One codebase tracked in revision control, many deploys.
2.  **Dependencies**: Explicitly declare and isolate dependencies.
3.  **Config**: Store config in the environment.
4.  **Backing services**: Treat backing services as attached resources.
5.  **Build, release, and Run**: Strictly separate build and run stages.
6.  **Processes**: Execute the app as one or more stateless processes.
7.  **Port binding**: Export services via port binding.
8.  **Concurrency**: Scale out via the process model.
9.  **Disposability**: Maximize robustness with fast startup and graceful shutdown.
10.  **Dev/prod parity**: Keep development, staging, and production as similar as possible.
11.  **Logs**: Treat logs as event streams.
12.  **Admin processes**: Run admin/management tasks as one-off processes.



#### Codebase
* Every application should have its own codebase. Multiple codebases for multiple versions must be avoided.
* _Multiple apps sharing the same code are a violation of the twelve-factor_
> **In Microservices**, every service should have its own codebase. Having an independent codebase helps you to easy CI/CD process for your applications.
* _If you need to share you need to build a library and make it as a dependency and manage through package repository like maven, nuget_

#### Dependencies 
**Explicitly Declare and Isolate the Dependencies**
* A twelve-factor app never relies on implicit existence of system-wide packages
* Consider the dependencies from the operating system/ execution environment perspective as well.
> **Microservices**: All the application packages will be managed through package managers like sbt, maven.
> 
> * In non-containerized environments, you can go for configuration management tools like chef, ansible, etc. to install system-level dependencies.
> * For a containerized environment, you can go for dockerfile.

#### Config
 * _**Do not hardcode**  configuration values as constants in the codebase. This is a violation of 12-factor app principles._
 It advocates the strict separation between the code and configurations. The code must be the same irrespective of where the application being deployed.
  


 #### Backing Services
**Treat Backing Resources as Attached Resources** 
Database, Message Brokers, Cache, Logging, any other external systems that the app communicates is treated as Backing service.
12-factor app can automatically swap the application from one provider to another without making any further modifications to the code base. Only configuration change should be able to take care of it.
> In a **microservice ecosystem**, anything external to service is treated as attached resource. The resource can be swapped at any given point of time without impacting the service.

#### Build, Release, and Run 
**Strictly Separate Build and Run Stages**

>    * **Build stage**: transform the code into an executable bundle/ build package.
>    * **Release stage**: get the build package from the build stage and combines with the configurations of the deployment environment and make your application ready to run.
>    * **Run stage**: It is like running your app in the execution environment.
The application must have a strict separation between the build, release, and run stages. Let us understand each stage in more detail.
 **Microservices**: You can use CI/CD tools to automate the builds and deployment process. Docker images make it easy to separate the build, release, and run stages more efficiently.

#### Processes 
**Execute the App as One or More Stateless Processes**
Application should store the state in the database instead of in memory of the process. _Avoid using sticky sessions_
For storing session information, use any cache provider.
#### Port Binding
**Export Services Via Port Binding**
The twelve-factor app is completely self-contained and doesn't rely on runtime injection of a webserver into the execution environment to create a web-facing service. The web app exports HTTP as a service by binding to a port, and listening to requests coming in on that port.
#### Concurrency  
Scale Out Via the Process Model
Consider running your application as multiple processes/instances instead of running in one large system (Horizontal scaling)
> **Microservices**: By adopting the containerization, applications can be scaled horizontally as per the demands.

#### Disposability 
**Maximize the Robustness with Fast Startup and Graceful Shutdown**
* Graceful shutdowns are very important. The system must ensure the correct state. 
_When the application is shutting down or starting, an instance should not impact the application state._

> **Microservices**: By adopting the containerization into the deployment process of microservices, your application implicitly follows this principle at a maximum extent. Docker containers can be started or stopped instantly. Storing request, state, or session data in queues or other backing services ensures that a request is handled seamlessly in the event of a container crash.

#### Dev/Prod Parity 
**Keep Development, Staging, and Production as Similar as Possible**
> **Microservices**: This is an inherent feature of the Microservices that is run using the containerization techniques.
#### Logs 
**Treat Logs as Event Streams**
* Separating the log generation and processing of log's information. Logs will be written as a standard output and the execution environment takes care of capture, storage, curation, and archival of such stream should be handled by the execution environment
> **Microservices**: In Microservices, observability is the first-class citizen. Observability can be achieved through using APM tools (ELK, Newrelic, and other tools) or log aggregations tools like Splunk, logs, etc
#### Admin Processes
**Run Admin/Management Tasks as One-Off Processes**
There is a number of one-off processes as part of the application deployment like data migration, executing one-off scripts in a specific environment.
Twelve-factor principles advocates for keeping such administrative tasks as part of the application codebase in the repository. By doing so, one-off scripts follow the same process defined for your codebase.
> **Microservices**: Containerization also helps here to run the one-off processes as a task and shutdown automatically one done with the implementation.


### References:

> * https://12factor.net/
> * https://www.nginx.com/blog/microservices-reference-architecture-nginx-twelve-factor-app/
> * https://blog.scottlogic.com/2017/07/17/successful-microservices-with-12factor-app.html
> * https://dzone.com/articles/12-factor-app-principles-and-cloud-native-microser
> * https://tyk.io/blog/being-cloud-native-12-factor-app-design/