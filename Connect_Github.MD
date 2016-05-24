#How to connect RStudio to github 

If RStudio prompts you for a username and password every time you try to push your project to Github, open the shell (RStudio menu: Tools/Shel…) and do the following:

1) Set username and email (if you did not do that before)

```
git config —global user.name “your_username” 
git config —global user.email “your_email@example.com”
```

2) Create SSH key

`ssh-keygen -t rsa -C “your_email@example.com”`

In RStudio, go to menu Tools / Global options / Git SVN / View public key and copy the key to your Github account setting (Edit profile / SSH keys / Add SSH key).

To check that ssh-authentication works, try to run

`ssh -T git@github.com`

and you should get something like

`Hi your_username! You’ve successfully authenticated, but GitHub does not provide shell access.`

In case RStudio still asks for username and password when you push, check if it the remote.origin.url is set to ssh protocol:
```
git config -l
```
Look at the line starting with 'remote.origin.url'. If it its url a http url like 'https://' switch your protocol.
You can also find the SSH url from in your github project. Click on the green 'Clone or Download' button.

```
git config remote.origin.url git@github.com:your_username/your_project.git
```

## Sources 
(http://www.r-bloggers.com/rstudio-and-github/) 

(http://applyr.blogspot.com/2014/05/rstudio-pushing-to-github-with-ssh.html)
