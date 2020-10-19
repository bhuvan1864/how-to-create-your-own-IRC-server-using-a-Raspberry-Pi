# how-to-create-your-own-IRC-server-using-a-Raspberry-Pi
Dating back to the 1980’s, IRC is one of the classic chat protocols that’s still the driving force behind many modern online communities, including the popular Twitch streaming platform. Today, there’s no shortage of IRC clients and servers available. You can also setup your own IRC server with Raspberry Pi.


There are two main benefits to creating your own server:

1. Complete control over the chat experience
With your own IRC server, you’ll have the freedom to assign your own moderators, create channels for the topics you care about, and have the final say in who can and can’t join your server – perfect if you’re sick of your online discussions getting hijacked by trolls, bots, spammers and other digital undesirables.

2. Take control of your data
Are you concerned about a third party leaking your information accidentally, selling it on purpose, or using it in targeted adverts?

By running your own server, you can maintain control over all your data, ranging from your username and email address, right through to your IRC chat logs.



# What you’ll need:
*Raspberry Pi running Raspberry Pi OS
*Power cable that’s compatible with your Raspberry Pi
*External keyboard and a way to it to your P.
*HDMI or micro HDMI cable, depending on Raspberry Pi model
*External monitor
*Ethernet cable if not connecting over Wi-Fi

# Getting started : Let us set up your Raspberry PI
To start, connect the power cable and all the peripherals to your Raspberry Pi.Once your Raspberry Pi has booted, make sure it is connected to the Internet. Open the Terminal and type the following commands to update the system:

  sudo apt update && sudo apt -y upgrade
  
If Raspberry Pi does install any updates, then reboot the Pi before moving to the next step.

# Install the Ircd-Hybrid server:
You’ll be creating ab IRC server using the Ircd-Hybrid daemon. Install the Ircd-Hybrid package using the following command:

  sudo apt install ircd-hybrid
  
This download can take a while, so now’s the perfect time to go grab a cup of coffee!

# Secure your server: creating an encrypted password
You’ll need to create an encrypted password that you’ll use to connect to your IRC server as an operator, which will give you increased privileges, similar to a moderator or admin account.

To create an encrypted password, run the following command:

  /usr/bin/mkpasswd your-password-here
  
PS:Replace “your-password-here” with the password you want to use.

The Terminal will now return a series of letters and numbers, which is your encrypted password. Make a note of this password, as you’ll need it to set up your server’s operator account.

# Configuring your IRC server 
Next, you’ll need to configure the Ircd-Hybrid software:

  sudo nano /etc/ircd-hybrid/ircd.conf

This opens the ircd.conf configuration file in Raspberry Pi’s Nano text editor.
This file contains many settings, but as a minimum you should make the following changes:

# 1. Give your IRC server a name:
Scroll to the 'serverinfo {' block and find the following:

name = "hybrid8.debian.local";

You should give your server a unique name. For example:

name = "Bhuvan'sPrivateServer.irc";

# 2. Provide a description
You’ll need to provide a short description which will be displayed whenever someone connects to your IRC server.

Find the following:

description = "ircd-hybrid 8.1-debian";

Replace this text with your own description. For example:

description = "Raspberry Pi IRC Server";

# 3. Describe your network
Scroll to the following section:

network_name = "debian";
network_desc = "This is My Network";

These two lines describe the network where your server is running, so you should update it to reflect your specific network. For example:

network_name = "MyNetwork";
network_desc = "This is my Raspberry Pi IRC Network";

# 4. Set some limits
By default, Ircd-Hybrid allows 512 connections at any one time. If you want to change this limit, then find the following line:

default_max_clients = 512;

You can now increase or decrease this 512-user limit. In this case, I am only allowing a maximum of 100 connections to my IRC server:

default_max_clients = 100;

# 5. Create your operator
Next up is defining some settings for the operator. Scroll to the operator { block. Note that this section may require uncommenting, so delete the first # symbol in each line.
With that done, find the following line:

name = "sheep";

Replace this line with the name that you want to assign to your operator group:

name = "operator";

You need to specify who can run the operator command by editing the following line:

user = "*@192.0.2.240/28";

This will allow anyone to access operator, if they have the correct credentials:

user = "*@*";

Finally, add the encrypted password that you generated earlier. Find the following:

password = "xxxxxxxxxxxxx";

Make sure you replace this line with the encrypted password and not the plain text version!

Once you’re happy with the information you’ve entered, save the configuration file by pressing the Ctrl + O and then Ctrl + X to close.

# Run your IRC server
Restart the Hybrid-IRCD server by typing in this command:

  sudo /etc/init.d/ircd-hybrid restart

Once the server restarts, it’s ready to use!

# mIRC: Connecting to your Raspberry Pi server
You can connect to your IRC server using any IRC client. I’m using mIRC, but other popular alternatives include WeeChat, and LimeChat for macOS.

To connect to your IRC server, launch your chosen client and then opt to add a new server. Depending on your IRC client, you should now be prompted to enter the following information:

Description: This is how the server will be displayed in your IRC client, so enter any value you want to use.
Address: This is the IP address of your Raspberry Pi IRC server. If you don’t know the IP address, you can retrieve this information by opening a Terminal on your Raspberry Pi and running the hostname -I command.
Ports: You should set this to 6667, as this is the default for most servers.

Click “Add” to be able to connect to your IRC server.

As you can see, it is rather easy to set up an IRC server on your Raspberry Pi. There are tons of things that Raspberry Pi can do, too, like perform as a captive portal Wi-Fi access point, a music server, or even a personal web server. 

All these and more will be uploaded soon...
until then,
hasta la vista 


-B





  
  

