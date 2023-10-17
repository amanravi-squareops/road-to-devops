
<img width="1000" height="200" alt="image" src="https://github.com/amanravi-squareops/road-to-devops/assets/146931382/e0da4167-eb23-451b-bed4-3702eb72a4bf">


# Module 6 - Setting up infrastructure for a 2-tier web application using Wordpress and the MySQL database in single instance
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

## 2. Deploy a networking stack

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

Create a routing table for our subnet for determine which way to forward traffic.

![image](https://github.com/amanravi-squareops/road-to-devops/assets/146931382/136bfea2-91b5-4ac4-acaa-3090ce7b4619)

#### Create Internet gateway
Internet gateway allows for internet traffic to actually enter into a VPC.

![image](https://github.com/amanravi-squareops/road-to-devops/assets/146931382/045901b1-a4de-4cf5-bc8c-72f1ce723fd4)

Now attach Internet gateway to our vpc . 

## Now it's time to launch the EC2 instance and attach your VPC to that.

![image](https://github.com/amanravi-squareops/road-to-devops/assets/146931382/39763814-d1c5-47b6-85cd-fa70e55f504d)

Here i am using Redhat image , instance type t2.micro and creating key value pair for secure login .

Now edit your network configuration and attach your vpc and enable Auto-assign public IP.

![image](https://github.com/amanravi-squareops/road-to-devops/assets/146931382/dbaf2dc1-3960-43cf-bf47-dc9146074d41)

Create your security group and add inbound security group rules (ssh for remote access and http for webapp), and launch your instance and do ssh.

### SSH for installation PHP , Wordpress and MySql database

#### Open a terminal and run this command:
      # sudo apt-get update
      
### Install Apache
Run this command to install the apache package on ubuntu:

      # sudo apt-get install apache2
### Start your Apache webserver

      # systemctl start apache2
### Verify Apache Installation 
   - open a web browser and type in the address bar http://server_ip_address
   - check the  status of your apache webserver

### Install MySql 
     # apt-get install mysql-server

### To start your MySQL, run this command:
    # systemctl start mysql

### Change the authentication method
    # ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YOUR_STRONG_PASSWORD';

### After executing the ALTER USER command, run the following command:
    # mysql> FLUSH PRIVILEGES;
### Installing PHP
    # sudo apt install php libapache2-mod-php php-mysql

###  Install WordPress On Ubuntu
    # sudo wget -c http://wordpress.org/latest.tar.gz
    # sudo tar -xzvf latest.tar.gz
### Then move the WordPress files
    # sudo mv wordpress/* /var/www/

### Now set appropriate permissions , It should be owned by the Apache2 user and group called www-data.
    # sudo chown -R www-data:www-data /var/www/wordpress
    # sudo chmod -R 775 /var/www/wordpress

###  Create WordPress Database On MySQL
    mysql> CREATE DATABASE dbname;
    mysql> CREATE USER 'username'@'%' IDENTIFIED WITH mysql_native_password BY 'db_password';
    mysql> GRANT ALL ON dbname.* TO 'username'@'%';
    mysql> FLUSH PRIVILEGES;
    mysql> EXIT;

###  open the wp-config.php configuration file for editing
  
![data](https://github.com/amanravi-squareops/road-to-devops/assets/146931382/b9e27f72-237c-4f61-90d6-979dca21e0be)

    # sudo systemctl restart apache2
    # sudo systemctl restart mysql
    
### Open your web browser, then enter your
    http://ip_address


