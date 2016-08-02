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
In case you run into urllib3 'module missing error:
you might be missing required modules. Install and try above command again
```
sudo su
pip install requests
pip install cssselect
pip install urllib3
```
