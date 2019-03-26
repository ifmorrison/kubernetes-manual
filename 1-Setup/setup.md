# Setup
<!-- TOC -->

- [Setup](#setup)
- [1. Installing prerequisites](#1-installing-prerequisites)
    - [1.1. aws cli](#11-aws-cli)
    - [1.2. kubectl](#12-kubectl)
    - [1.3. aws-iam-authenticator](#13-aws-iam-authenticator)
- [2. Creating a cluster](#2-creating-a-cluster)
    - [2.1. AWS Getting Started method](#21-aws-getting-started-method)
    - [2.2. Terraform method](#22-terraform-method)
    - [2.3. eksctl method](#23-eksctl-method)
- [3. Authenticating to the cluster](#3-authenticating-to-the-cluster)
    - [3.1. AWS Getting Started or eksctl methods](#31-aws-getting-started-or-eksctl-methods)
    - [3.2. Terraform:](#32-terraform)
- [4. Allow worker nodes to connect to the cluster](#4-allow-worker-nodes-to-connect-to-the-cluster)
    - [4.1. AWS Getting Started](#41-aws-getting-started)
    - [4.2. Terraform](#42-terraform)
    - [4.3. eksctl](#43-eksctl)
- [5. Finish](#5-finish)

<!-- /TOC -->

# 1. Installing prerequisites  

To create an EKS cluster you will need to have the following:

- aws cli installed and configured
- kubectl
- aws-iam-authenticator

## 1.1. aws cli 

Instructions for installing the aws cli can be found here:  
[Installing the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)  

After installing the aws cli you can configure it by running the following command:    
 `aws configure`  

Note: Configuring the AWS cli will require your IAM authentication token.  

You can test the aws cli has been configured successfully with this command:  
`aws sts get-caller-identity`   

## 1.2. kubectl 

Instructions for installing kubectl can be found at the following link:  
[Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)  

Note: You do not have to configure kubectl at this stage, just installing it is enough.  

## 1.3. aws-iam-authenticator  

Instructions for installing aws-iam-authenticator can be found at the following link:  

[Installing aws-iam-authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)  


# 2. Creating a cluster  

There are several options for creating an EKS cluster.
You can choose any method from below:

## 2.1. AWS Getting Started method  

The AWS Getting Started method can be found here:  
[Getting Started with Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)  

This method consists of deploying two CloudFormation stacks. The first stack creates a VPC, and the second stack creates the cluster and the worker nodes. The defaults for the stacks are find, although you may want to alter the instance type and autoscale settings.  

## 2.2. Terraform method

The AWS terraform provider provides resources for managing EKS clusters.  
This tutorial contains example terraform templates in this section:  
[Example terraform templates can be found here]
Your aws provider information will be taken from your local aws cli setup

## 2.3. eksctl method

eksctl is a cli utility for deploying and managing eks clusters  
Installation and usage instructions for this utility can be found here:  
[https://github.com/weaveworks/eksctl](eksctl github)
[https://aws.amazon.com/blogs/opensource/eksctl-eks-cluster-one-command/](Amazon EKS Cluster with One Command)


# 3. Authenticating to the cluster

Authentication secrets are stored in $HOME/.kube/config  

## 3.1. AWS Getting Started or eksctl methods  

The aws cli will update the local authentication secrets with this command:  
`aws eks update-kubeconfig --name clustername`  
Test your connection to the cluster:    
`kubectl cluster-info`  

## 3.2. Terraform: 

Authentication details are available as a terraform output.  

Update kubeconfig:
`terraform output kubeconfig > $HOME/.kube/config`  
Test your connection to the cluster:  
`kubectl cluster-info`


# 4. Allow worker nodes to connect to the cluster

The new cluster must be provided its IAM role details so that worker nodes can join the cluster.
Until this is done no worker nodes will be available, so no containers can be run.

## 4.1. AWS Getting Started 
This step is fully documented in the AWS Getting Started guide

## 4.2. Terraform

First export the configmap  
`terraform output configmap > configmap.yml`  
Then apply it to the cluster  
`kubectl apply -f ./configmap.yml`  

## 4.3. eksctl

eksctl applies the configuration automatically, so nothing further is necessary

# 5. Finish

Your worker nodes should be visible now. 

See status of nodes:
`kubectl get nodes`