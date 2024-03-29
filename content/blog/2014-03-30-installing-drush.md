---
title:  "Installing Drush"
description: "Installing drush and drupal on csoft.net."
date:   2014-03-29
tags: 
  - hosting
  - csoft
  - BSD
  - drupal
  - drush
---

## Installing Drush on OS X

Installing [Drush](https://github.com/drush-ops/drush) on OS X is fairly straight forward. I'm writing this from memory but I think it went a little like this...

* **Prerequisites:** Install [XCode](https://itunes.apple.com/au/app/xcode/id497799835?mt=12) and command line tools from the App Store. Install [homebrew](http://brew.sh/).

* Install [Composer](https://getcomposer.org/doc/00-intro.md#globally-on-osx-via-homebrew-) globally (via. homebrew).

```bash
brew update
brew tap homebrew/dupes
brew tap homebrew/php
brew install composer
```

* Install Drush 6.x (stable at time of writing).

```bash
composer global require drush/drush:6.*
```

* Test it

```bash
drush --version
```

## Installing Drush on Csoft.net

I've been hosting various sites at [csoft.net](https://www.csoft.net) since about 2000 and using Drupal on there since around 2004 (version 4.5 I think). If you're comfortable on the command line (BSD) they help you look after yourself. They're solid.

The install of Drush on Csoft shared hosting is a little more involved than on OS X. Both Composer and Drush require command line PHP rather than the Csoft default of fast CGI. This can be found at /usr/local/php-[version]/bin/php and must be specified explicitly. Make sure to use a version of PHP with openssl to avoid the following error.

```bash
Some settings on your machine make Composer unable to work properly.
Make sure that you fix the issues listed below and run this script again:

The openssl extension is missing, which means that secure HTTPS transfers are impossible.
If possible you should enable it or recompile php with --with-openssl
```

* Install Composer locally and set up an alias to ensure it runs using the correct php. 

```bash
curl -sS https://getcomposer.org/installer | /usr/local/php53-fat/bin/php -- --install-dir=bin
alias composer='/usr/local/php53-fat/bin/php ~/bin/composer.phar'
```

* Use Composer to install Drush.

```bash
composer global require drush/drush:6.*
```

* Add the following aliases to your .bash_profile. The drush alias uses the [currently recommended](https://drupal.org/node/1302418) way of running under a particular version of PHP by setting the DRUSH_PHP environment variable and calling the drush shell script.

```bash
alias composer='/usr/local/php53-fat/bin/php ~/bin/composer.phar'
alias drush='DRUSH_PHP=/usr/local/php53-fat/bin/php ~/.composer/vendor/drush/drush/drush'
```

* Reset the environment and test your new drush install

```bash
. ~/.bash_profile
drush --version
```

## Updating Drush

To update to a newer version in the future:

```bash
composer self-update
composer global update
```
