# WordPress application will achieve high availability by developing a multi-instance infrastructure.

### Creating a multi-instance architecture in AWS for Wordpress application with
    - High availability
    - Security
    - Monitoring

### for installation of wordpress , php and create  mysql replication cluster , refer my repository Readme file.

Now create EFSand select same vpc where your instance is running.

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

### After editing , make sure before reboot, run this command .
    # sudo mount -a
Now upload your photo on wordpress and paste image url in the browser and refresh and check image present in the browser or not.

