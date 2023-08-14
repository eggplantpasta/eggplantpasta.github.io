---
title: "Installing the MineCraft Server at DigitalOcean"
description: "Installing a MineCraft Server on a DigitalOcean droplet."
date: 2014-04-21
tags: 
  - Minecraft
  - DigitalOcean
  - hosting
  - TODO
---

Setting up an MineCraft server on [DigitalOcean's](https://www.digitalocean.com/) cheapest droplet (virtual server) is straight forward and works suprisingly well for a small number of players. In this guide I assume you are a little familiar with the command line and virtual servers. If you need help in this area DigitalOcean has a large number of [tutorials](https://www.digitalocean.com/community/articles/how-to-create-your-first-digitalocean-droplet-virtual-server) to get you started.

## Create your droplet

* Create Droplet on [DigitalOcean](https://www.digitalocean.com/)

## Configure the software

* ssh root@dnsname or ip address
* Update Ubuntu
  `apt-get update 
   apt-get dist-upgrade`
* Install Java `sudo apt-get install openjdk-7-jre-headless`
* sudo apt-get install screen

## Secure the server

* [set up iptables](https://www.digitalocean.com/community/articles/how-to-set-up-a-firewall-using-ip-tables-on-ubuntu-12-04) firewall for ssh (tcp 22) and minecraft (tcp 25565)
* log in as minecraft `ssh minecraft@minecraft.pudiga.org`
	* list current rules `sudo iptables -L`
	* flush current rules `sudo iptables -F`
	* `sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT`
	* allow ssh `sudo iptables -A INPUT -p tcp --dport ssh -j ACCEPT`
	* allow minecraft `sudo iptables -A INPUT -p tcp --dport 25565 -j ACCEPT`
	* drop all others `sudo iptables -A INPUT -j DROP`
    * loopback access `sudo iptables -I INPUT 1 -i lo -j ACCEPT`
    * sudo apt-get install iptables-persistent
    * sudo service iptables-persistent start
* fix default editor `update-alternatives --config editor`
* add an unprivileged user `adduser minecraft`
* add privileges `visudo`
* reboot for good luck

## Install MineCraft

* copy the link to the latest minecraft server from the bottom of [this page](https://minecraft.net/download)
* download it `wget -O minecraft_server.jar https://s3.amazonaws.com/Minecraft.Download/versions/1.7.9/minecraft_server.1.7.9.jar`
* Start it `screen -S "Minecraft server"`
* exit screen by `ctl-a d`
* reattach screen by `screen -R`
* java -Xmx512M -Xms512M -jar minecraft_server.jar nogui
* vi vi server.properties
* white-list=true
* vi white-list.txt