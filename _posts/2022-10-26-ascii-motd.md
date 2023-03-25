---
title: Display custom banner upon login of SSH Shell
date: 2022-10-26
categories: []
tags: ["ascii", "ssh"]
---

Would you like to upgrade your server's SSH terminal when someone logs in? Add some custom text?

<!--more-->

## How to add a Banner to your SSH Shell terminal

Would you like to display a Message of the day when someone, hopefully someone you allow or want, connects to your server to see a welcome message like below:

![Example of MOTD](/assets/img/posts/ascii-ssh-motd/featured-ssh-motd.png)

To do this is really simple to do on any Linux Server.

Simply follow the steps below:

### Edit the Message of the Day file

Connect to your server via SSH and you will be greeted with the boring Message of the day.

Run the following command in terminal
``` bash
sudo nano /etc/motd
```

Now go to a site that can generate ASCII text for you. I used a tool created by [PatOrJK](http://patorjk.com/) which can be found at [http://patorjk.com/software/taag/](http://patorjk.com/software/taag/ "URL to ASCII Generator"). 

Enter the welcome message you would like the user to see. Just remember to keep it short and sweet. Generally what is used is the name of the server or what the server is used for.

For example if its a Mail Server, you would see "MAIL" as the welcome server. More commonly used in home labs is the name of the server itself (If they are using cool names)

You can browse the list of styles of ASCII 'fonts' they have but what I suggest you do is click the "Test All" button. This will generate a list of the text you entered in all the fonts available. Then browse through and see which one you prefer.

Once you have found the epic look of the font copy the content and then return to your Terminal Session and paste it in the `motd` file.

Save and close the file, then log out the server then log in again and low and behold, there is your gorgeous master piece.