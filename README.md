---
title: "AWS Thingy"
output: github_document
---



## Mac is my preferred environment

Accessing AWS EC2 from mac is more convenient than from Windows, because terminal is __the__ tool for SSH. All I need is the AWS key pair and the IP address of my EC2 instance. 

However, one issue I ran into is that I need to convert my .PPK (PuTTy key format) file to .PEM (Mac). So I need to install *putty* on Mac OS to do key conversion. But before I can install putty, I also need to install *port*, which is an apt-get equivalent for mac. 

## Preparation

1. Download *port* from https://www.macports.org/install.php
2. Install port
3. In terminal, navigate to key folder and then run ```puttygen your_key.ppk -O private-openssh -o your_key.pem``` to get the conversion processed
4. Make key read by owner ```chmod 400 your_key.pem```
5. Log on to my EC2 instance ```ssh -i your_key.pem ubuntu@ip_address```

## Frequently used commands on Ubuntu

* Always keep Ubuntu up to date
    * ```sudo apt-get update```
  
* Check groups and users permissions (https://www.digitalocean.com/community/tutorials/an-introduction-to-linux-permissions)
    * ```cat /etc/group```
    * ```cat /etc/passwd```

## MySQL 

There is a good walk-through from DigitalOcean (https://www.digitalocean.com/community/tutorials/a-basic-mysql-tutorial)

* Check MySQL status
    * ```sudo service mysql status```, ctrl-c to exit

* Log on MySQL
    * ```mysql -u root -p``` for now I use root and default password
    * steve:l*****7*
* Generally I use [MySQL Workbench](https://dev.mysql.com/downloads/workbench/) remotely for database management; require aws key pair for SSH authentication; also make sure EC2 security is open for MySQL port 3306

