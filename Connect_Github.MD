In case RStudio still asks for username and password when you push, check if it the remote.origin.url is set to ssh protocol:
```
git config -l
```
Look at the line starting with 'remote.origin.url'. If it its url a http url like 'https://' switch your protocol.
You can also find the SSH url from in your github project. Click on the green 'Clone or Download' button.

```
git config remote.origin.url git@github.com:your_username/your_project.git
```

