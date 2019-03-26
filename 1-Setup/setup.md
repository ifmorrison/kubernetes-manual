<!-- TOC -->

- [Installing prerequisites](#installing-prerequisites)
    - [aws cli](#aws-cli)
    - [kubectl](#kubectl)
    - [aws-iam-authenticator](#aws-iam-authenticator)
- [Creating a cluster](#creating-a-cluster)
    - [AWS Getting Started method](#aws-getting-started-method)
    - [Terraform method](#terraform-method)
    - [eksctl method](#eksctl-method)
- [Authenticating to the cluster](#authenticating-to-the-cluster)
    - [AWS Getting Started or eksctl methods](#aws-getting-started-or-eksctl-methods)
    - [Terraform:](#terraform)
- [Allow worker nodes to connect to the cluster](#allow-worker-nodes-to-connect-to-the-cluster)
    - [AWS Getting Started](#aws-getting-started)
    - [Terraform](#terraform)
    - [eksctl](#eksctl)
- [Finish](#finish)

<!-- /TOC -->

# Installing prerequisites  

To create an EKS cluster you will need to have the following:

- aws cli installed and configured
- kubectl
- aws-iam-authenticator

## aws cli 

Instructions for installing the aws cli can be found here:  
[Installing the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)  

After installing the aws cli you will need to configure it using the command 'aws configure  '
This will require your IAM authentication token, which you can find in the aws portal  

You can test your user authentication with the command 'aws sts get-caller-identity'   

## kubectl 

Instructions for installing kubectl can be found at the following link:  
[Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)  

Note: You do not have to configure kubectl at this stage, just installing it is enough.  

## aws-iam-authenticator  

Instructions for installing aws-iam-authenticator can be found at the following link:  

[Installing aws-iam-authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)  


# Creating a cluster  

There are several options for creating an EKS cluster.
You can choose any method from below:

## AWS Getting Started method  

The AWS Getting Started method can be found here:  
[Getting Started with Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)  

This method consists of deploying two CloudFormation stacks. The first stack creates a VPC, and the second stack creates the cluster and the worker nodes. The defaults for the stacks are find, although you may want to alter the instance type and autoscale settings.  

## Terraform method

The AWS terraform provider provides resources for managing EKS clusters.  
An example of using terraform to create an EKS cluster can be found here:  
[eks-terraform](eks-terraform/)

## eksctl method

eksctl is a cli utility for deploying and managing eks clusters  
Installation and usage instructions for this utility can be found here:  
[https://github.com/weaveworks/eksctl](eksctl github)
[https://aws.amazon.com/blogs/opensource/eksctl-eks-cluster-one-command/](Amazon EKS Cluster with One Command)


# Authenticating to the cluster

Authentication secrets are stored in $HOME/.kube/config  

## AWS Getting Started or eksctl methods  

Update your local authentication file:
`aws eks update-kubeconfig --name clustername`
Test your connection to the cluster:  
`kubectl cluster-info`

## Terraform: 

Authentication details are available as a terraform output.  

Update kubeconfig:
`terraform output kubeconfig > $HOME/.kube/config`  
Test your connection to the cluster:  
`kubectl cluster-info`


# Allow worker nodes to connect to the cluster

Finally, the new cluster must be updated its IAM role details so that worker nodes can join the cluster.
Until this is done no worker nodes will be available, so no containers can be run.

## AWS Getting Started 
This step is fully documented in the AWS Getting Started guide

## Terraform

First export the configmap  
`terraform output configmap > configmap.yml`  
Then apply it to the cluster  
`kubectl apply -f ./configmap.yml`  

## eksctl

eksctl applies the configuration automatically, so nothing further is necessary

# Finish

Your worker nodes should be visible now. 

See status of nodes:
`kubectl get nodes`