# Setup

## Installing prerequisites

Before creating an Amazon EKS cluster, make sure your environment is set up correctly.
You should have the following

- aws cli installed and configured
- kubectl
- aws-iam-authenticator

**aws cli**

Instructions for installing the aws cli can be found here:
[Installing the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

After installing the aws cli you will need to configure it using the command 'aws configure'
This will require your IAM authentication token, which you can find in the aws portal

You can test your user authentication with the command 'aws sts get-caller-identity'

**kubectl**

Instructions for installing kubectl can be found at the following link:
[Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

Note: You do not have to configure kubectl at this stage, just installing it is enough.

**aws-iam-authenticator**

Instructions for installing aws-iam-authenticator can be found at the following link:

[Installing aws-iam-authenticator](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html)

## Creating a cluster

There are several ways a cluster can be created:

**AWS Getting Started method**

The AWS Getting Started method can be found here:
[Getting Started with Amazon EKS](https://docs.aws.amazon.com/eks/latest/userguide/getting-started.html)

This method consists of deploying two CloudFormation stacks. The first stack creates a VPC, and the second stack creates the cluster and the worker nodes. The defaults for the stacks are find, although you may want to alter the instance type and autoscale settings.

**Terraform** 

The AWS terraform provider provides resources for managing EKS clusters.
An example of using terraform to create an EKS cluster can be found here:
[eks-terraform](1-Setup/eks-terraform/)

**eksctl**

eksctl is a cli utility for managing eks clusters
Installation and usage instructions for this utility can be found here:
(eksctl github)[https://github.com/weaveworks/eksctl]

