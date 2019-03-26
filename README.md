# Kubernetes Manual

This repository provides an overview and introductory tutorial for AWS Elastic Container Service for Kubernetes

<!-- TOC -->

- [Kubernetes Manual](#kubernetes-manual)
    - [What is Kubernetes?](#what-is-kubernetes)
    - [Why do I need a container orchestration platform?](#why-do-i-need-a-container-orchestration-platform)
    - [What does a Kubernetes cluster consist of?](#what-does-a-kubernetes-cluster-consist-of)
    - [What is Amazon EKS?](#what-is-amazon-eks)
    - [Getting Started](#getting-started)
        - [Setup](#setup)
        - [Deployments](#deployments)
        - [Services](#services)
        - [Ingress](#ingress)
        - [Helm](#helm)
        - [Troubleshooting](#troubleshooting)
        - [Monitoring](#monitoring)

<!-- /TOC -->

## What is Kubernetes?

Kubernetes is a container orchestration plaform originally created by Google and now maintained by the [Cloud Native Computing Foundation](https://www.cncf.io/)  
The official site for Kubernetes can be found here: [kubernetes.io](https://kubernetes.io/)

## Why do I need a container orchestration platform?

With container orchestration we can

- Create a cluster out of multiple container hosts
- Bind storage to containers
- Allow communication between containers
- Store configuration maps
- Store secrets
- Allow secure access to containers
- Set resource limits
- manage containers as a service, instead of as individuals

Kubernetes provides a standard interface to orchestrate containers.

## What does a Kubernetes cluster consist of?

For this workshop, only Master nodes, and Worker nodes will be discussed.

Master nodes are linux server instances on which run all of the critical services related to the functioning of the cluster.

Worker nodes are linux server instances with a container runtime (typically docker) on which our application containers run.

## What is Amazon EKS?

Amazon Elastic Container Service for Kubernetes (EKS) is Amazon's managed kubernetes service.

Amazon operates Kubernetes master nodes in multiple availability zones. These master nodes are not visible and cannot be accessed by the customer. The master nodes are backed by a %99.9 SLA.

Worker nodes consist of Amazon EC2 instances, with the instance type definable by the customer. Worker nodes are organised into "Node Pools", and each node pool typically has an autoscaling group associated with it.

The customer can view and is responsible for the worker nodes.

## Getting Started

This tutorial contains the following sections:  

### Setup
[Setup](1-Setup/setup.md "Setup")  
How to set up an EKS cluster and set up admin tooling

### Deployments
[Deployments](2-Deployments/deployments.md "Deployments")  
Deploying applications

### Services
[Services](3-Services/services.md "Services")  
Exposing deployments  

### Ingress
[Ingress](4-Ingress/ingress.md "Ingress")  
TLS termination and path routing  

### Helm
[Helm](5-Helm/helm.md "Helm")  
Helm: a ackage manager for Kubernetes

### Troubleshooting
[Troubleshooting](6-Troubleshooting/troubleshooting.md "Troubleshooting")  
Cluster and application troubleshooting

### Monitoring
[Monitoring](7-Monitoring/monitoring.md "Monitoring")  
Kubernetes monitoring