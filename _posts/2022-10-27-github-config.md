---
title: Configure Global Git username and email
date: 2022-10-27
categories: []
tags: [git,terminal]
---

In this post I will show you how to configure your Git username and email

<!--more-->

# Config Git for the entire system

Your username and email are linked to all commits on your machine. When you set these values, every commit done on a repository will have the details you set in the following commands.

If you don't set these values, you will be faced with an error stating that the `user.name` and `user.email` have not been configured when trying to push your commits. 

To fix this error simply run the following commands in terminal

``` sh
git config --global user.name "Your Name"
```

``` sh
git config --global user.email "youremail@domain.com"
```

To confirm that the changes have been made:

``` sh
git config --list
```

``` 
# Output
user.name=Your Name
user.email=youremail@domain.com
```

This will save your settings in `~/.gitconfig`. A good idea will be to include this in your backup process for when/if you reinstall or want to move this config to another computer

# Configure Git for a single repository

Open terminal and CD into the directory

``` sh
cd ~/projects/my_project
```

Set the username and email address 

``` sh
git config user.name "Your Name"
```
``` sh
git config user.email "youremail@domain.com"
```
Notice: The `--global` tag is not there.

To confirm the change has been made run

``` sh
git config --list
```

``` 
# Output
user.name=Your Name
user.email=youremail@domain.com
```

Repo specific configs are saved in `.git/config` under the root directory of your project. In this case `~/projects/my_project/.git/config`

# Conclusion

The Git username and password can be configured for both system or repository wide using the `git config` commands