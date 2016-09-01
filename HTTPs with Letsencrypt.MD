Use letsencrypt to generate your keys for the server

Connect to your machine using using SSH e.g. with Putty

You will need git installed:
```
# Amazon Linux
sudo yum update
sudo yum install git

# Ubuntu
sudo apt-get update
sudo apt-get install git
```
Install letsencrypt. Make sure to replace with your <host.domain.name>
```
git clone https://github.com/letsencrypt/letsencrypt
cd letsencrypt
```
Generate the keys 
```
# Amazon Linux
./letsencrypt-auto certonly --standalone -v -d <host.domain.name>
# Ubuntu
./letsencrypt-auto certonly --standalone -v -d <host.domain.name> --debug

#Follow the instructions
```

All generated keys and issued certificates can be found in `/etc/letsencrypt/live/<host.domain.name>`. Rather than copying, please point your (web) server configuration directly to those files (or create symlinks). During the renewal, `/etc/letsencrypt/live` is updated with the latest necessary files. 
[More information directly from letsencrypt](http://letsencrypt.readthedocs.io/en/latest/using.html#where-are-my-certificates)

##### Debugging 
In case you have rstudio already installed and configured to run on port 80 you might get an error when setting up letsencrypt. You can use port 443 instead of port 80 to register the certificate.

Make sure to stop the apache server: 
```
sudo service httpd stop
/letsencrypt-auto certonly --standalone --standalone-supported-challenges tls-sni-01 --renew-by-default --rsa-key-size 4096 --domains <host.domain.name>
sudo service httpd start
```

[Source: Letsencrypt Forum](https://community.letsencrypt.org/t/cant-host-anything-on-port-80/5250)


### Renewing the Keys

#### Manual Process
Just follow the same step as during key generation
```
# Amazon Linux
./letsencrypt-auto certonly --standalone -v -d <host.domain.name>
# Ubuntu
./letsencrypt-auto certonly --standalone -v -d <host.domain.name> --debug

#Follow the instructions
```
##### Debugging 
In case you run into urllib3 'module missing error:
you might be missing required modules. Install and try above command again

First connect to the instance using SSH e.g. with Putty
```
sudo su
cd letsencrypt
pip install requests
pip install cssselect
pip install urllib3
```
[Source: Stackoverflow](http://stackoverflow.com/questions/27440060/how-to-fix-importerror-no-module-named-packages-urllib3)
