## Introduction
Helm is a package manager like npm for javascript  or apt/yum in linux.
* Package Manager: It is a tool that automates the process of installing, upgrading, configuring, and removing programs for computer's operating system.

Before we talk about what is helm? Will go back in time when we were not having any package manager (apt & yum or npm for javascript programming langauge). During those days we used to download the binaries compile and install. So, for example to download apache or nginx every organization had their own methods or steps to install package.

https://medium.com/@manoj.bhagwat60/understanding-helm-charts-26f2db983d96

## What is Helm?
* Pre-requisite:
    - Good Understanding of Kubernetes
    
Helm is a tool for kubernetes that helps you install and manage application.
* Chart: 
   - The format that helm uses to package application is called Chart.

* Architecture:

    - It has client(run on your computer) and server(tiller)

* Client: (Helm CLi)
    - Runs on your computer
    - Generates kubernetes YAML template
    - Send request to Tiller
* Server: (Tiller)
    - Runs in kubernetes cluster
    - Manage release and adds to helm history so that you can rollback

* Files Structure
    - my-chart/
        - Chart.yaml: store metadata and version information
        - values-yaml: Store default configuration value
        - requirements.yaml: Dependency 
        - charts/ : template directory
            - _helper: function definition

* Create Release 
    - Deployment
    - Services
    - Pods
    - and more

## Example
* Node.js + MongoDB web app - package them into same chart so that we can manage them at the same time
based on yaml


## Why in Sofy

Helm is a popular open source package manager for kubernetes cluster.
Helps in packaged hcl products and onboard it on sofy which user can deploy in their environment.





