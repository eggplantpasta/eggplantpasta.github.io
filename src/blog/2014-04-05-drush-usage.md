---
layout: base
title: "Drush Usage and Commands"
tags: post
---

The traditional drush command reference site is [drush.ws](http://drush.ws) but a newer one has just recently popped up - [Drush Commands](http://www.drushcommands.com). Both are good although I don't think drush.ws is being updated because the most recent version it documents is 5.

The following are examples of some of the ways I use Drush.

* Do a fresh [drupal install](http://definitivedrupal.org/erratum/download-drupal-then-change-directory-not-other-way-around).

```bash
drush dl drupal-7.x --drupal-project-rename=sitename.com
cd sitename.com
drush si --db-url=mysql://dbuser:dbpassword@localhost:port/dbname
```

* To download, install, and enable a module.

`drush en module_name -y`

* Clear cache

`drush cc`

* Update Drupal core and contrib projects and apply any pending database updates (Same as pm-updatecode + updatedb). This lists the pending updates and asks if you want to continue. Remember to take a copy of ".htaccess" and "robots.txt" before doing a core update so you can integrate any changes afterwards.

`drush up`

* Print site alias records for all known site aliases and local sites.

`drush sa`

* Open a SQL command-line interface using Drupal's credentials.

`drush sqlc`


