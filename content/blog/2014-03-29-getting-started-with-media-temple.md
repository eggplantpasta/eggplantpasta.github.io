---
title:  "Media Temple"
description: "Getting started with Media Temple."
date:   2014-03-29
tags: 
  - hosting
  - drupal
  - media temple
---

## Well that was short lived

I'd heard about [Media Temple](http://mediatemple.net) for years. People give them good reviews ([CSS-Tricks](http://css-tricks.com)) and their [grid hosting](http://mediatemple.net/webhosting/shared/) seemed perfect for a high traffic site I was involved with.

>Media Temple loves your success. So we built the Grid hosting platform to handle any traffic spike. From hundreds of visitors to hundreds of thousands, we’ll keep your site online.

* $20 a month
* SSD database storage
* Host up to 100 websites
* 1TB monthly bandwidth
* 100 GB storage
* shell access

So I [signed up](https://ac.mediatemple.net/order/domain.mt) and got deep into configuring it for hosting a new drupal site when I discovered [this](http://www.anthonymclin.com/hosting-drupal-mediatemples-grid-service) person who performance tested them and discovered MySQL issues with Drupal.

More googling uncovered [this](https://forum.mediatemple.net/topic/6558-504-gateway-timeout-errors-for-drupal-site/), [this](https://drupal.org/node/1289828), and [this](http://mediatemple.net/blog/2007/01/19/anatomy-of-mysql-on-the-grid/).

Seems like (mt) is not the right choice for Drupal hosting. I'm back on CSoft for development while I research the best solution for this new site.
