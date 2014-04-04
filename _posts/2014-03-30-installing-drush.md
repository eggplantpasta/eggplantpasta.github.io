---
layout: post
title: Installing Drush
description: "Installing drush and drupal on csoft.net."
modified: 2014-03-30
category: articles
tags: [hosting, drupal, drush, csoft, BSD]
share: true
---

## Installing Drush on OS X

Installing Drush on OS X is fairly straight forward. I'm writing this from memory but I think it went a little like this...

* **Prerequisites:** Install [XCode](https://itunes.apple.com/au/app/xcode/id497799835?mt=12) and command line tools from the App Store. Install [homebrew](http://brew.sh/).

* Following the Drush install instructions [here](https://github.com/drush-ops/drush)...

* Install [Composer](https://getcomposer.org/doc/00-intro.md#globally-on-osx-via-homebrew-) globally (via. homebrew)

~~~bash
brew update
brew tap josegonzalez/homebrew-php
brew tap homebrew/versions
brew install php55-intl
brew install josegonzalez/php/composer
~~~

* Install Drush 6.x (stable at time of writing)

~~~bash
composer global require drush/drush:6.*
~~~

* Test it

~~~bash
drush --version
~~~

## Installing Drush on Csoft.net

I've been hosting various sites at [csoft.net](https://www.csoft.net) since about 2000 and using Drupal on there since around 2004 (verson 4.5 I think). If you're comfortable on the command line they help you look after yourself. They're solid.

The install of Drush on Csoft is a little more involved.


## Notes to write up later.

[Instructions](http://definitivedrupal.org/erratum/download-drupal-then-change-directory-not-other-way-around)
~~~
drush dl drupal-7.x --drupal-project-rename=sitename.com
drush si --db-url=mysql://root:rootpass@localhost/formmsgs
~~~

[Drush PHP](https://drupal.org/node/1302418)

## Common drush commands

`drush en module_name -y` Download and install module.