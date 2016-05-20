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
./letsencrypt-auto certonly --standalone -v -d <host.domain.name> --

#Follow the instructions
```

All generated keys and issued certificates can be found in `/etc/letsencrypt/live/<host.domain.name>`. Rather than copying, please point your (web) server configuration directly to those files (or create symlinks). During the renewal, `/etc/letsencrypt/live` is updated with the latest necessary files.
[More information directly from letsencrypt](http://letsencrypt.readthedocs.io/en/latest/using.html#where-are-my-certificates)
