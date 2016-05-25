#Automatically start server on ec2-restart 

`vi /etc/rc.local`

Add line: 
```
[...]
sudo rstudio-server start
```

#Start Server in Screen to keep a command running in putty even after closing terminal 

###Notes 

- this is not needed for RStudio-Server

**Create Screen** 

Login to EC2 using SSH/Putty

In Terminal execute:
```
screen
<your command>
```

Press CTR + A +D to detach from the screen

You can now log off from the session

**To get back where you left off** 

Login to EC2 using SSH/Putty

`screen -RD` to reattach to the screen (if there's more than one you'll get a list of current screen sessions and you'll have to supply the session number) from a new session
