# Description  
This is the Cloud Formation Template which deploys two VM-Series Firewalls in Active-Passive mode in the chosen availability zone in a given AWS region. Cross zone HA is not supported in this version of the template. Two templates will be provided. One for deployments with new VPC and new Subnets ( Greenfield ) and another one for existing VPC and existing Subnets ( Brownfield ).  

The CFT is created for the HA failover mode - Secondary IP move. To use this HA failover mode, user should use the VMseries plugin version 2.0.1

# Template Elements    

# Parameters  
Following parameters will be given as an option to the user while deploying the stack from the AWS Cloud Formation console. 
 
# VPCName  
This is the name of the VPC. If not given, a default value 'panwVPC' will be used. Only for deployments with new VPC.  

# VPCId  
This is the id of an existing VPC. Users will be provided a drop down menu with the list of VPCs already created and he/she has to choose from one. No default values will be used.  

# VPCCIDR  
This is the CIDR for the newly created VPC. If not given, a default value of '10.4.0.0/16' will be used.  
 
# MgmtSubnetPrefix  
This is the CIDR for the management subnet. It is applicable for both new and existing VPC deployments. For both greenfield and brown deployment, a user has to input the CIDR, or a default value of '10.4.1.0/24' will be used.  
 
# HA2SubnetPrefix  
This is the CIDR for the HA2 subnet. It is applicable for both new and existing VPC deployments. For both greenfield and brownfield deployment, a user has to input the CIDR, or a default value of '10.4.2.0/24' will be used.  
 
# PublicSubnetPrefix  
This is the CIDR for the public subnet. It is applicable for both new and existing VPC deployments. For both greenfield and brownfield deployment, a user has to input the CIDR, or a default value of '10.4.3.0/24' will be used.  
 
# PrivateSubnetPrefix  
This is the CIDR for the public subnet. It is applicable for both new and existing VPC deployments. For both greenfield and brownfield deployment, a user has to input the CIDR, or a default value of '10.4.4.0/24' will be used.  
 
# LambdaSubnetPrefix  
This is the CIDR for the public subnet. It is applicable for both new and existing VPC deployments. For both greenfield and brownfield deployment, a user has to input the CIDR, or a default value of '10.4.5.0/24' will be used.  

# NeedDataPlaneIntfEIPAssociation  
This parameter is to let AWS auto-assign an Elastic IP address to the secondary IP of the data plane untrust interface. Default value is 'no'  

# KeyName  
This is the EC2 key pair used for accessing the firewall instances after deployment.  

# InstanceType  
This is the list of supported EC2 Instance Types for the vm-series firewall which the user has to choose from.  

# AvailabilityZone  
This is the availability zone in which the firewall will be deployed. This is a drop down menu which lists the existing availability zones in a given region.  

# BootstrapS3BucketActive  
This is the name of the S3 bucket which has the necessary folders for bootstrapping for the active firewall. For example folders which have init-cfg.txt, bootstrap.xml, license authcode, plugin image to boot with etc.  

# BootstrapS3BucketPassive  
This is the name of the S3 bucket which has the necessary folders for bootstrapping for the passive firewall. For example  folders which have init-cfg.txt, bootstrap.xml, license authcode, plugin image to boot with, etc.  

# LambdaS3Bucket  
This is the name of the S3 bucket which has the lambda function code ‘panw-aws-ha.zip’  

# CIDRForInstanceAccess  
This is the IP which the user can input, from which firewall instances can be accessed from outside AWS.  

# PanFwAmiId  
This is the AMI id of the firewall instance to be deployed.   

User will be given a link like 'Link to Ami Id lookup table: https://www.paloaltonetworks.com/documentation/global/compatibility-matrix/vm-series-firewalls/aws-cft-amazon-machine-images-ami-list' from which he can choose the AMI which user wants to deploy
 
 
 
 
 
# How to Deploy?  
Create the necessary prerequisites to deploy the template.  
Create S3 buckets for both active and passive FWs with necessary folders ( eg: config, license, plugins)  
Create a S3 bucket for lambda and make sure to have the panw-aws-ha.zip in that S3 bucket for the parameter LambdaS3Bucket.  
In the AWS Portal, under Cloud formation pane, upload  the deployment template. Fill the required  input parameters and deploy.  
