---
title:  "Drush Site Aliases"
description: "Configuring drush site aliases for local and remote sites."
date:   2014-04-06
tags: 
  - TODO
  - drupal
  - drush
  - aliases
  - ssh
---

## Local aliases on OS X

Drush aliases allow you to refer to sites via shortnames like @dev or @live. They also allow you to refer to sites when not in the root directory and even remote sites across an ssh link.

Aliases are defined in alias files. An alias file containing extensive examples and documentation is shipped with drush and can be viewed by giving the command `drush docs-aliases` or referenced from GitHib [here](https://github.com/drush-ops/drush/blob/master/examples/example.aliases.drushrc.php).

An alias file can be of a few forms and stored in various places but in general I like to use "group" alias files stored in the .drush directory of my home folder e.g.: `~/.drush/sitename.aliases.drushrc.php`. I have one file per project defining (typically) a local, dev, and live site. Alias groups create an implicit namespace that is named after the group so the alias is referred to as @group.site e.g.: `drush @sitename.dev status`


The minimum definition of a local alias is:

```php
<?php
$aliases['dev'] = array(
  'root' => '/home/username/www/dev.sitename.com',
  'uri' => 'dev.sitename.com',
);
?>
```

There are many more options than this which makes it tedious to define by hand. To shortcut the process for a working site drush itself can output the required definition. Change to the root of the working site and issue the command:

```bash
drush site-alias --with-db --show-passwords --with-optional @self
```

## Remote aliases



## Examples of alias usage

