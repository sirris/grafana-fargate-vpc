# Setting up grafana with a postgres backend, securely and scalable on AWS

***Goal of this projects:*** secure, scripted deployment of grafana on AWS, with little operational worries.

Choices made:
- whole setup described in cloudformation (infrastructure as code)
- use of VPC to not expose database directly to the Internet
- postgres RDS
- setup bastion host to enable secure access over ssh into VPC
- grafana via docker (official grafana/grafana image), aws fargate to manage the running container(s)
- use https to connect to grafana, terminated to aws ALB

This setup is largely inspired/borrowed from the AWS startup scripts. Find the original scripts at https://github.com/aws-samples/startup-kit-templates


## Prerequisites.
Before using these scripts, be sure to:
- AWS account
- An IAM user with the privileges to deploy cloudformation stacks
- (optional) aws cli installed and properly configured
- a key pair to access the bastion
- an tls/ssl certificate for the domain you want to use, managed by aws certificate manager.


## Deploying the infrastructure
Deploying this entire infrastructure can be done either via the cli or via the aws console (web based). If you deploy via the cli, you'll need to provide a number of parameters for each stack. When you use the aws console, you'll be presented with a form to full those out.

You'll deploy the scripts from 01_vpc.cfn.yml all the way to 04_fargate_grafana.cfn.yml

It's ok to accept all the defaults, you'll have to specify the name of the VPC and DB stack here and there.
