## Installation with Amazon Linux
Prerequisites: 
[install and configure Shiny Server](https://www.rstudio.com/products/shiny/download-server/)
[https with letsencrypt](https://github.com/maxjacu/RstudioServer/blob/master/HTTPs%20with%20Letsencrypt.MD)


When you have installed and configured Shiny and you're sure it works, modify your config file so it only serves to 127.0.0.1 (the local machine). This ensures that we don't accidentally expose the open server to the entire Internet.

Log into Amazon Linux EC2 Instance using SSH
Update shiny.conf to `listen 3838 127.0.0.1;` by making changes to the config.
` sudo vi /etc/shiny-server/shiny-server.conf`
```
# Tell Shiny Server that we want to run as the user whose
# home directory we find the application in.
run_as :HOME_USER:;

# Define a server that listens of port 3838.
server {
  listen 3838 127.0.0.1;

  # Define a location at the base URL
  location / {

    # Allow users to host their own apps in ~/ShinyApps
    user_dirs;

    # Optionally, you can restrict the privilege of hosting Shiny applications
    # only to members of a particular Linux group.
    # members_of shinyUsers;
  }
}

```

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
Open config:
```
sudo vi /etc/httpd/conf/httpd.conf
```
Within Editor - Add following to config
press `i` then insert with right mouseclick
```
LoadModule proxy_module modules/mod_proxy.so
LoadModule auth_openidc_module modules/mod_auth_openidc.so
```
Save Changes `:wq`

Create Virtual Host
```
#Create vhost.conf
cd /etc/httpd/conf.d
sudo touch vhost.conf
sudo nano /etc/httpd/conf.d/vhost.conf
```
Sign up to [auth0](auth0.com). 
`You will need to follow the steps in the Apache tutorial. Note: when you are logged in to Auth0, the tutorial includes your own variables in the configuration to make it easier for you.

Create a configuration file for your website using the configuration from the tutorial as a starting point. Replace everything from OIDCProviderIssuer to Location with the code in the tutorial.` [Source](https://auth0.com/blog/2015/09/24/adding-authentication-to-shiny-open-source-edition/)

Paste following information provided by auth0 into new file (right mouse-click), then exit with Ctr+X
It should look like something like this
```
<VirtualHost *:443>
  ProxyPass / http://localhost:3838/
  ProxyPassReverse / http://localhost:3838/
  ProxyPreserveHost On

  OIDCProviderIssuer https://<your-tenant>.auth0.com
  OIDCProviderAuthorizationEndpoint https://<your-tenant>.auth0.com/authorize
  OIDCProviderTokenEndpoint https://<your-tenant>.auth0.com/oauth/token
  OIDCProviderTokenEndpointAuth client_secret_post
  OIDCProviderUserInfoEndpoint https://<your-tenant>.auth0.com/userinfo

  OIDCClientID <YourClientID>
  OIDCClientSecret <YourClientSecret>

  OIDCScope "openid profile"
  OIDCRedirectURI https://<your-website>/auth
  OIDCCryptoPassphrase <passwordToEncryptTheSessionInformationOnTheCookie>
  OIDCCookiePath /

  SSLEngine on
  SSLCertificateFile /path/to/server.crt
  SSLCertificateKeyFile /path/to/server.key

  <Location />
     AuthType openid-connect
     Require valid-user
     LogLevel debug
  </Location>

</VirtualHost>
```

### Save & Restart Apache

Once you’re finished setting up all your Virtual Hosts, save and exit vhosts.conf (`ctrl + x if` you were using Nano) and restart Apache, like so…

`sudo service httpd restart`

*Sources:*

https://github.com/pingidentity/mod_auth_openidc/wiki
http://blog.zwiegnet.com/linux-server/install-mod_proxy-plugin-to-apache-centos/
https://pkgs.org/centos-6/epel-x86_64/jansson-2.6-1.el6.x86_64.rpm.html
https://auth0.com/blog/2015/09/24/adding-authentication-to-shiny-open-source-edition/
http://nouveauframework.org/blog/vhosts-running-multiple-sites-on-a-single-aws-ec2-instance/
