---
published: false
layout: post
title: "Installing Oracle XE using Vagrant"
description: "Installing Oracle XE locally using Vagrant."
modified: 2014-04-21
category: articles
tags: [Oracle, Vagrant, TODO]
share: true
---

## Resources

[http://wphilltech.com/sublime-text-for-oracle-apex-developers/](http://wphilltech.com/sublime-text-for-oracle-apex-developers/)

[http://tuhrig.de/3-ways-of-installing-oracle-xe-11g-on-ubuntu/](http://tuhrig.de/3-ways-of-installing-oracle-xe-11g-on-ubuntu/)

[https://github.com/hilverd/vagrant-ubuntu-oracle-xe](https://github.com/hilverd/vagrant-ubuntu-oracle-xe)

## Post install
In sql developer create a connection for system/manager.

Connect and

~~~~sql
ALTER USER hr ACCOUNT UNLOCK;
ALTER USER hr IDENTIFIED BY hr;
~~~~

Create connection for hr. Connect and test.

