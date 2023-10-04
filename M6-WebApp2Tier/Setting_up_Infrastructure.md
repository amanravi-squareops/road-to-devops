# Module 6 - Setting up infrastructure for a 2-tier web application using Wordpress and the MySQL database
While configuring this setup, there are multiple steps involved.
# Table of content:
- [2-Tier Highly Available WordPress Deployment](#2-tier-highly-available-wordpress-deployment)
  - [1. Create an AWS Account](#1-create-an-aws-account)
  - [2. Deploy a networking stack](#2-deploy-a-networking-stack)
  - [3. Create an Instance](#3-create-an-instance)
  - [4. SSH into your Instance](#4-ssh-into-your-instance)
  - [5. Install the Apache Web Server to run PHP](#5-install-the-apache-web-server-to-run-php)
  - [6. Install PHP to run WordPress](#6-install-php-to-run-wordpress)
  - [7. Install MySQL for adding database](#7-install-mysql-for-adding-database)
  - [8. Install WordPress](#8-install-wordpress)
  - [9. Map IP Address and Domain Name](#9-map-ip-address-and-domain-name)
    - [Other Method: To change your WordPress site URL with the wp-cli](#other-method-to-change-your-wordpress-site-url-with-the-wp-cli)
   
## 1. Create an AWS Account
First, you need to create an account on AWS, where you have to set up your 2-tier web application..

## Deploy a networking stack

Here, we need to configure our network as per our requirements. I am going to create a logically isolated network environment with the help of VPC.
#### VPC-There are multiple steps involved , while creating vpc-
- Give you vpc name
- Select IPv4 CIDR block
- Give your CIDR block size (CIDR block size must be between /16 and /28.)
![image](https://github.com/amanravi-squareops/road-to-devops/assets/146931382/da64bd94-f13b-488a-9ca4-2fd2d5b42f96)

After creating the VPC successfully, the next step is creating a subnet. Creating multiple subnets allows us to create logical network divisions between resources. Here, I am going to create two subnets named: - 
  - PublicSubnet1CIDR with 10.10.1.0/24 CIDR
  - PublicSubnet1CIDR with 10.10.2.0/24 CIDR

#### Select your VPC (we have created vpc in previous step )
- First subnet
  
  <img width="412" alt="image" src="https://github.com/amanravi-squareops/road-to-devops/assets/146931382/df792bbc-3f06-4eca-950a-34345e96b1f9">

- Second subnet
    
    ![image](https://github.com/amanravi-squareops/road-to-devops/assets/146931382/a85fc438-2fb7-4c00-bf1b-01854d5951a1)

#### Create your routing table 

Create a routing table for our subnet so that our instance will get public access from the internet gateway .



