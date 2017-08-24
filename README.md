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

* Connecting to MySQL using R

```r
library(DBI)
conn <- dbConnect(
    drv = RMySQL::MySQL(),
    dbname = "mysql",
    group = "destination",
    host = "192.168.0.1",
    port = 3306,
    username = "xxx",
    password = "xxxx")
```

```
## Error in .local(drv, ...): Failed to connect to database: Error: Can't connect to MySQL server on '192.168.0.1' (57)
```

```r
rs <- dbSendQuery(conn, "SELECT * FROM user;")
```

```
## Error in dbSendQuery(conn, "SELECT * FROM user;"): object 'conn' not found
```

```r
dbFetch(rs)
```

```
## Error in dbFetch(rs): object 'rs' not found
```

## Ubuntu Misc

* Run program as root ```R -i```

* check system RAM ```cat /proc/meminfo``` or ```free -m```

* check disk space ```df -h```

* check system status ```htop``` need ```sudo apt-get install htop```

* 
