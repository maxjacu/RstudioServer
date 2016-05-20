# Installation with Amazon Linux

Log into Amazon Linux EC2 Instance using SSH

Install auth_openidc_module
```
sudo rpm -ivh https://github.com/pingidentity/mod_auth_openidc/releases/download/v1.8.8/mod_auth_openidc-1.8.8-1.el7.centos.x86_64.rpm
sudo rpm -ivh http://dl.fedoraproject.org/pub/epel/6/x86_64/jansson-2.6-1.el6.x86_64.rpm
sudo rpm -ivh ftp://rpmfind.net/linux/centos/7.2.1511/updates/x86_64/Packages/pcre-8.32-15.el7_2.1.x86_64.rpm --replacefiles
```
Check its availability
```
ls -l /usr/lib64/httpd/modules/mod_auth_openidc.so
```
**Open config:**
```
sudo vi /etc/httpd/conf/httpd.conf
```
Within Editor - Add following to config
press `i` then insert with right mouseclick
```
LoadModule proxy_module modules/mod_proxy.so
LoadModule auth_openidc_module modules/mod_auth_openidc.so
```
Save Changes
```
:wq
```

start apache
`sudo service httpd start`

stop apache
`sudo service httpd stop`


*Sources:*
https://github.com/pingidentity/mod_auth_openidc/wiki
http://blog.zwiegnet.com/linux-server/install-mod_proxy-plugin-to-apache-centos/
https://pkgs.org/centos-6/epel-x86_64/jansson-2.6-1.el6.x86_64.rpm.html
