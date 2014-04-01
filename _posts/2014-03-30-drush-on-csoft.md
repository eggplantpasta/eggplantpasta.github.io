---
layout: post
title: Drush on CSoft
description: "Installing drush and drupal on csoft.net."
modified: 2014-03-30
category: articles
tags: [hosting, drupal, drush, csoft, BSD]
share: false
---

I've been hosting various sites at [csoft.net](https://www.csoft.net) since about 2000 and using Drupal on there since around 2004 (4.5)


[Instructions](http://definitivedrupal.org/erratum/download-drupal-then-change-directory-not-other-way-around)
~~~
drush dl drupal-7.x --drupal-project-rename=sitename.com
drush si --db-url=mysql://root:rootpass@localhost/formmsgs
~~~

[Drush PHP](https://drupal.org/node/1302418)

## Common drush commands

`drush en module_name -y` Download and install module.