---
title: How to Deploy Symfony 3.3 on CentOS 7
date: 2017-12-16
updated: 2018-03-25
layout: post
tags: Symfony, CentOS
---

I'll show you how you can deploy your Symfony demo or production stage application in your VPS system. I'm gonna use Digital Ocean VPS and CentOS 7. This is not tutorial, this is close to my actual project deployment.

## Change your timezone

If you didn't do, you cannot read your logs. For example, you are living in Europe, but server time zone is America, you can see all log times in America times.

You can check this [link](https://en.wikipedia.org/wiki/Time_zone#List_of_UTC_offsets) for your time zone.

`timedatectl set-timezone $YOUR_TIMEZONE`

## Update all system

`yum update -y`

## Change SELinux mode Enforcing to Permissive

You have to change SELINUX=enforcing to permissive

```
[root@webserver ~]# vi /etc/selinux/config
# This file controls the state of SELinux on the system.
# SELINUX= can take one of these three values:
#     enforcing - SELinux security policy is enforced.
#     permissive - SELinux prints warnings instead of enforcing.
#     disabled - No SELinux policy is loaded.
SELINUX=enforcing
# SELINUXTYPE= can take one of three two values:
#     targeted - Targeted processes are protected,
#     minimum - Modification of targeted policy. Only selected processes are protected.
#     mls - Multi Level Security protection.
SELINUXTYPE=targeted
```

## Build the file system
```
[root@webserver ~]# mkdir -p /home/$USER_NAME/www
[root@webserver ~]# mkdir -p /home/$USER_NAME/log/$PROJECT_NAME
[root@webserver ~]# chown nginx:nginx -R /home/$USER_NAME/www /home/$USER_NAME/log
```

## Install Nginx

Nginx is not available in default CentOS repository. That's why we have to enable epel-release.

`[root@webserver ~]# yum install -y epel-release`

Now, we can download it

`[root@webserver ~]# yum install -y nginx`

If we wanted to reboot the server, Nginx cannot start after the boot. Therefore, we have to run this two lines

`[root@webserver ~]# systemctl enable nginx.service`

and

`[root@webserver ~]# systemctl start nginx.service`

## Install MySQL (or MariaDB)

Actualy, you can use MySQL either, but in default CentOS's repository you cannot find it. They have only MariaDB, but I'll show you how you can install MySQL, too.

First of all, I'll show you installation MariaDB

`[root@webserver ~]# yum install -y mariadb mariadb-server`

Than we have to do this again for MariaDB.

`[root@webserver ~]# systemctl enable mariadb.service`

`[root@webserver ~]# systemctl start mariadb.service`

### RDBMS Security

In default, all first setup MySQL/MariaDB, we run setup script. This script will ask you about your root password or allow anonymous users...

`[root@webserver ~]# mysql_secure_installation`

```
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE! PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure its, we'll need to current
password for the root user. if you've just installed MariaDB, and
you haven't set the root password yet, the password will blank,
you should just press enter here.

Enter current password for root (enter for none):

OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the
MariaDB
Root user without the proper authorization.

Set root password? [Y/n] y
New password:
Re-enter new password:
Password updated successfully!
Reloading privilege tables..
 ... Success!

By default, a MariaDB installation has an anonymous user, allowing
anyone
to log into MariaDB without having to have a user account created
for them, This is intended only for testing, and to make
installation go a bit smoother, You should remove them before
moving into a production environment.

Remove anonymous users? [Y/n] y
 ... Success!

Normally, root should only be allowed to connect from 'localhost'
this ensures that someone cannot guess at the root password from
the network.

Disallow root login remotely? [Y/n] y

By default, MariaDB comes with a database name 'test' that anyone
can access. This is also intended only for testing, and should be
remove before moving into a production environment.

Remove test database and access to it? [Y/n] y
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so
far will take effect immediately.

Reload privilege tables no? [Y/n] y
 ... Success!

Cleaning up...

All done! If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```

## Instal PHP 7.1

You must have wget if you want to use this line. If you don't have, you can download with this line

```
[root@webserver ~]# yum install -y wget
[root@webserver ~]# wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
[root@webserver ~]# rpm -Uvh remi-release-7.rpm
[root@webserver ~]# yum install -y yum-utils
[root@webserver ~]# yum-config-manager --enable remi-php71
```
You will see like this output

```
[root@webserver ~]# yum-config-manager --enable remi-php71
Loaded plugins: fastestmirror
========================= repo: remi-php71 ==========================
[remi-php71]
async = True
bandwidth = 0
base_persistdir = /var/lib/yum/repos/x86_64/7
baseurl =
cache = 0
cachedir = /var/cache/yum/x86_64/7/remi-php71
check_config_file_age = True
compare_providers_priority = 80
cost = 1000
deltarpm_metadata_percentage = 100
deltarpm_percentage =
enabled = 1
enablegroups = True
exclude =
failovermethod = priority
ftp_disable_epsv = False
gpgcadir = /var/lib/yum/repos/x86_64/7/remi-php71/gpgcadir
gpgcakey =
gpgcheck = True
gpgdir = /var/lib/yum/repos/x86_64/7/remi-php71/gpgdir
gpgkey = file:///etc/pki/rpm-gpg/RPM-GPG-KEY-remi
hdrdir = /var/cache/yum/x86_64/7/remi-php71/headers
http_caching = all
includepkgs =
ip_resolve =
keepalive = True
keepcache = False
mddownloadpolicy = sqlite
mdpolicy = group:small
mediaid =
metadata_expire = 21600
metadata_expire_filter = read-only:present
metalink =
minrate = 0
mirrorlist = http://rpms.remirepo.net/enterprise/7/php71/mirror
mirrorlist_expire = 86400
name = Remi's PHP 7.1 RPM repository for Enterprise Linux 7 - x86_64
old_base_cache_dir =
password =
persistdir = /var/lib/yum/repos/x86_64/7/remi-php71
pkgdir = /var/cache/yum/x86_64/7/remi-php71/packages
proxy = False
proxy_dict =
proxy_password =
proxy_username =
repo_gpgcheck = False
retries = 10
skip_if_unavailable = False
ssl_check_cert_permissions = True
sslcacert =
sslclientcert =
sslclientkey =
sslverify = True
throttle = 0
timeout = 30.0
ui_id = remi-php71
ui_repoid_vars = releasever,
   basearch
username =
```

First PHPs are core PHP packages, you have to download it.

`[root@webserver ~]# yum install -y php php-fpm php-common`

Than we have to start it, because Nginx can return an error

`[root@webserver ~]# systemctl enable php-fpm.service`

`[root@webserver ~]# systemctl start php-fpm.service`

And also you can find your php extensions in this chart

<!-- add table for -->

`[root@webserver ~]# vi /etc/nginx/conf.d/default.conf`

You will see blank conf file, copy this conf to the file

```
#/etc/nginx/conf.d/default.conf

server {
    # server_name example.com www.example.com;

    # Symfony 3.x default web/app.php path
    root /home/$USER_NAME/www/$PROJECT_NAME/web;

    location / {
        # try to serve file directly, fallback to index.php
        try_files $uri /app.php$is_args$args;
    }

    location ~ ^/app\.php(/|$) {
        fastcgi_pass unix:/var/run/php7-1-fpm.sock;
        fastcgi_split_path_info ^(.+\.php)(/.*)$;
        include fastcgi_params;
        # When you are using symlinks to link the document root to the
        # current version of your application, you should pass the real
        # application path instead of the path to the symlink to PHP
        # FPM.
        # Otherwise, PHP's OPcache may not properly detect changes to
        # your PHP files (see https://github.com/zendtech/ZendOptimizerPlus/issues/126
        # for more information).
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        fastcgi_param DOCUMENT_ROOT $realpath_root;
        # Prevents URIs that include the front controller. This will 404:
        # http://domain.tld/app.php/some-path
        # Remove the internal directive to allow URIs like this
        internal;
    }

    # return 404 for all other php files not matching the front controller
    # this prevents access to other php files you don't want to be accessible.
    location ~ \.php$ {
        return 404;
    }

    error_log /home/$USER_NAME/log/$PROJECT_NAME/error.log;
    access_log /home/$USER_NAME/log/$PROJECT_NAME/access.log;
}
```

If you run it run now, you will get an error. Because, we did not create an directory for log, web assets... That's why don't run it!

`[root@webserver ~]# systemctl restart nginx.service`

Now, we have a look php-fpm configuration file.

`[root@webserver ~]# vi /etc/php-fpm.d/www.conf`

Replace these lines:

`user = apache` to `user = nginx`

`group = apache` to `user = nginx`

`;listen.owner = nobody` to `liste.owner = nginx`

`;listen.group = nobody` to `liste.group = nginx`

> __Important__: You have to be careful about semicolons!

Additionally, we won't use `listen = 127.0.0.1:9000`, that's why, we have to edit it.

`listen = /var/run/php7-1-fpm.sock`

`[root@webserver ~]# systemctl restart php-fpm.service`

# Time is Deploy time - YAY
You can use git or not, but I prefer git.

## Use git

I'll show you can you use git for deploying files, but we have to download git packages
`[root@webserver ~]# yum install -y git`

Than, I'll clone all repository and do this in tmp folder. Because after the deploy we won't use it again.
```
[root@webserver ~]# cd /tmp
[root@webserver tmp]# git clone https://gitsite.example/reponame/project.git
[root@webserver tmp]# mv project/ /home/$USER_NAME/www/$PROJECT_NAME
[root@webserver tmp]# cd
[root@webserver ~]# chown nginx:nginx -R /home/$USER_NAME/www/$PROJECT_NAME
[root@webserver ~]# chmod 755 -R /home/$USER_NAME/www/$PROJECT_NAME/var/cache /home/$USER_NAME/www/$PROJECT_NAME/var/logs
[root@webserver ~]# rm -rf /home/$USER_NAME/www/$PROJECT_NAME/var/cache/* /home/$USER_NAME/www/$PROJECT_NAME/var/logs/*
```
## Install all Composer stuffs

15f0a0a40484f0a224034a9ef560fa4e composer.bash

Use this line for downloading main composer.phar file.

Than you can run it.

Wait, you forgot something.

You have to change your $SYMFONY_ENV dev to prod.

### It is too important,

If you didn't do this, you will get an composer error.

```
[root@webserver ~]# export SYMFONY_ENV=prod
[root@webserver ~]# cd /home/$USER_NAME/www/$PROJECT_NAME
[root@webserver ~]# /usr/local/bin/composer install --no-dev -o --ansi
[root@webserver ~]# chown nginx:nginx -R /home/$USER_NAME/www/$PROJECT_NAME
```
## Download your php extensions right now

I think, this is more efficiently, if you don't have idea about your php requirements.

For example, I have to install

I ran it

`[root@webserver ~]# yum install -y php-pdo php-pdo_mysql php-xml php-zip php-mbstring`

Than run this command

`[root@webserver ~]# cd /home/$USER_NAME/www/$PROJECT_NAME`
`[root@webserver ~]# php bin/symfony_requirements`

```
Symfony Requirements Checker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

> PHP is using the following php.ini file:
  /etc/php.ini

> Checking Symfony requirements:
  ...........................WWW......


 [OK]                                         
 Your system is ready to run Symfony projects


Optional recommendations to improve your setup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 * posix_isatty() should be available
   > Install and enable the php_posix extension (used to colorize the
   > CLI output).

 * intl extension should be available
   > Install and enable the intl extension (used for validators).

 * a PHP accelerator should be installed
   > Install and/or enable a PHP accelerator (highly recommended).


Note  The command console could use a different php.ini file
~~~~  than the one used with your web server. To be on the
      safe side, please check the requirements from your web
      server using the web/config.php script.
```

Lastly, I download these extension

`[root@webserver ~]# yum install -y php-posix php-intl php-opcache`

```
[root@ln11 housing]# php bin/symfony_requirements

Symfony Requirements Checker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

> PHP is using the following php.ini file:
  /etc/php.ini

> Checking Symfony requirements:
  ...............................W........


 [OK]                                         
 Your system is ready to run Symfony projects


Optional recommendations to improve your setup
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 * intl ICU version installed on your system is outdated (50.1.2) and
   does not match the ICU data bundled with Symfony (60.1)
   > To get the latest internationalization data upgrade the ICU
   > system package and the intl PHP extension.


Note  The command console could use a different php.ini file
~~~~  than the one used with your web server. To be on the
      safe side, please check the requirements from your web
      server using the web/config.php script.
```

ICU 60.1 is not necessarily, but you can find for update in online. Default repository has libicu 50.1.2-15 (12/16/2017)

## Database stuffs

In this chapter little bit important because your second system it is...

```
cd /home/$USER_NAME/www/$PROJECT_NAME
export SYMFONY_ENV=prod
php bin/console doctrine:database:create
php bin/console doctrine:schema:create
```

## Check your ip address / domain in your browser.

If you get an error, let me know. Maybe I can help you.

## Errors

### Nginx open(), Permission Error

Check your SELinux status with

`[root@webserver ~]# getenforce`

If return Enforcing you have to run it

`[root@webserver ~]# setenforce 0`

If you run it again you will get Permisive, and you can run it.

### Already geting Nginx default page

If you look /etc/nginx/nginx.conf file you can see server{}, just this block you can comment it. like


```
[root@webserver ~]# vi /etc/nginx/nginx.conf
...
#server {
#    ...
#}
...
```

### White page

```
[root@webserver ~]# cat /home/$USER_NAME/log/$PROJECT_NAME/error.log

2017/12/16 13:05:14 [error] 1909#0: *1 FastCGI sent in stderr: "PHP message:
  PHP Fatal error:  Uncaught UnexpectedValueException: The stream or file
  "/home/berkhan/www/housing/var/logs/prod.log" could not be opened: failed
  to open stream: Permission denied in
  /home/berkhan/www/housing/vendor/monolog/monolog/src/Monolog/Handler/StreamHandler.php:107

Stack trace:
  ...
```

Solution is:

`[root@webserver ~]# chown nginx:nginx -R /home/$USER_NAME/www .`

## Final

If you have any question, let me know. You can use disqus (I prefer).
