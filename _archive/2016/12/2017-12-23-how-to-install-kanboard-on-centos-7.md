---
title: How to install kanboard on CentOS 7
date: 2017-12-23
updated: 2017-03-25
type: post
tags: CentOS
---

Kanban like a life style. This method for efficiently time management.

## Update the system, Install epel-release and PHP7.1
```
yum update -y
yum install -y wget epel-release
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm
yum install -y yum-utils
yum-config-manager --enable remi-php71
yum install -y php
```

## Install PHP extensions
After PHP installation, you will have Apache httpd server. We don't need to download again.

In this *how to*, I'll use SQLite. For performance, you can use OpCache. If I wanted to use plugins system, I have to install zip extension.

```
yum install -y \
    php-gd \
    php-mbstring \
    php-openssl \
    php-json \
    php-hash \
    php-ctype \
    php-session \
    php-filter \
    php-xml \
    php-dom \
    php-opcache \
    php-pdo_sqlite
```

## Download Kanboard zip

```
yum install -y unzip
cd /var/www/html
wget https://github.com/kanboard/kanboard/archive/v1.1.1.zip
```

You can unzip to /var/www/html folder.

`unzip v1.1.1.zip`

But, don't forget to delete the zip

`rm -rf v1.1.1.zip`

If you run this line you don't get any error, after what I write.

`mv kanboard-1.1.1/ kanboard/`

## Set some settings

### SELinux settings
`chcon -R -t httpd_sys_content_rw_t /var/www/html/kanboard/data`

`setsebol -P httpd_can_network_connect=1`

### Owner settings
`chown -R apache:apache /var/www/html/kanboard/data`

You don't need to edit php.ini for `short_open_tag = On`

### Firewall settings
`firewall-cmd --add-service=http --permanent`

`firewall-cmd --list-services | grep http`

If you saw http, you can start httpd

### Start the service
Start command will start the service

`systemctl start httpd.service`

Enable command for boot start.

`systemctl enable httpd.service`

And now, you can access from your browser

If you don't know your ip addres, you can run it then you will find it.

`ip addres | grep inet`
