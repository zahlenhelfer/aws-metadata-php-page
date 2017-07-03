# Overview #
Queries metadata address on AWS EC2 instances to help see what machine you hit behind an Elastic Load Balancer (ELB)

### Demo Screenshot ###
![Demo screenshot of page](http://www.alphamusk.com/img/demo_aws_metadata.jpg)

## Installation on EC2 Instance ##
Paste into bootstrapping
    #!/bin/sh

### Reconfigure ssh keys (Optional)
    /bin/rm -v /etc/ssh/ssh_host_*
    dpkg-reconfigure openssh-server

### Install applications
    apt-get install -y apache2 php5 awscli git

### GIT code on Ubuntu
    cd /var/www/html && git clone http://github.com/alphamusk/aws-metadata-php-page 

### Cron job to git source every 30 mins
    ##### m h  dom mon dow   command
    job="*/30 * * * *  cd /var/www/html && git pull http://github.com/alphamusk/aws-metadata-php-page.git > /dev/null 2>&1"
    (crontab -u ${USER} -l; echo "${job}" ) | crontab -u ${USER} -
    crontab -l
