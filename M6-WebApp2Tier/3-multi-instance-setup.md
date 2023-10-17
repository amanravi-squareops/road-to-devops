# WordPress application will achieve high availability by developing a multi-instance infrastructure.

### Creating a multi-instance architecture in AWS for Wordpress application with
    - High availability
    - Security
    - Monitoring

### For installation of WordPress, PHP, and MySQL replication clusters, refer to my repository.

### Now, I am going to create a target group for the load balancer. It is used to route requests to one or more registered targets.

<img width="815" alt="image" src="https://github.com/amanravi-squareops/road-to-devops/assets/146931382/b1d62bcd-7d8b-4ce4-b581-1a3efa6a28e8">

#### Target group health status should be Success

### Now, go to the load balancer and create an ALB for the WordPress application.

<img width="812" alt="image" src="https://github.com/amanravi-squareops/road-to-devops/assets/146931382/e83f17ca-9ce8-4641-bc06-28d9a825c86c">

#### Open the DNS link provided by ALB, upload your image, and check that your image is visible on the browser after consecutive refreshes.

Your image is stored in local WordPress storage; now we have to attach EFS to all WordPress applications.

#### Create an EFS and select the same VPC where your instance is running.

<img width="404" alt="image" src="https://github.com/amanravi-squareops/road-to-devops/assets/146931382/aac93b4b-74cb-4241-8edc-5dad5d543e36">

### SSH to your vm and run following command:
    # mount -t efs fs-0d436907e5d279e5a <mount-ip>
### Check efs is mount successfully or not.
    # df -h
### Now , we need to mount efs permanently
#### you need to install helper agent for mounting efs
    # sudo apt-get update
    # sudo apt-get -y install wget

### Run this Shell Scripting code

    if echo $(python3 -V 2>&1) | grep -e "Python 3.6"; then
    sudo wget https://bootstrap.pypa.io/pip/3.6/get-pip.py -O /tmp/get-pip.py
    elif echo $(python3 -V 2>&1) | grep -e "Python 3.5"; then
        sudo wget https://bootstrap.pypa.io/pip/3.5/get-pip.py -O /tmp/get-pip.py
    elif echo $(python3 -V 2>&1) | grep -e "Python 3.4"; then
        sudo wget https://bootstrap.pypa.io/pip/3.4/get-pip.py -O /tmp/get-pip.py
    else
        sudo apt-get -y install python3-distutils
        sudo wget https://bootstrap.pypa.io/get-pip.py -O /tmp/get-pip.py
    fi
### Install botocore
    sudo python3 /tmp/get-pip.py
    sudo pip3 install botocore

You can refer this doc too - https://docs.aws.amazon.com/efs/latest/ug/installing-amazon-efs-utils.html#installing-other-distro

### Permanent Mount-
    # vim /etc/fstab
    # <dns>:/ /<mount-point>/ nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport,_netdev 0 0

### After editing the fstab file, make sure, before rebooting, to run this command.
    # sudo mount -a

Now upload your photo on WordPress, paste the image URL in the browser, and refresh and image is present in the browser or not after consecutive refreshes.
