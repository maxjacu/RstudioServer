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

#Clone an existing GitHub project to new RStudio project

In RStudio, click New project as normal. Click Version Control.

In Clone Git Repository, enter the GitHub repository URL as per below. Change the project directory name if necessary.

In RStudio, again click Tools -> Shell … . Enter:

`git config remote.origin.url git@github.com:ewenharrison/test.git`

## Sources 
(http://www.r-bloggers.com/rstudio-and-github/) 

(http://applyr.blogspot.com/2014/05/rstudio-pushing-to-github-with-ssh.html)
