---
title: "Social Media Links"
description: "Configuring custom social media links without javascript."
date: 2014-04-12
tags: 
  - html
  - socal media
  - open graph
---

The various social media platforms all offer a way add buttons to an article or site giving the user a way to "like" or "share" a page. These supplied buttons use off-site javascript or styling that is not under your control. It slows the page load times and looks out of place.

A better way to link is by using a [URL scheme](http://stackoverflow.com/questions/7157411/adding-a-google-plus-one-or-share-link-to-an-email-newsletter).

*Remember to encode the strings you include in the URLs below*

### Facebook
Although not facebook's preferred way there is a URL scheme supported by them to allow [sharing](https://developers.facebook.com/docs/plugins/share-button).

```html
<a href="https://www.facebook.com/sharer/sharer.php?u=sitename.com" target="_blank">
 Share on Facebook
</a>
```

There were more [options](http://stackoverflow.com/questions/12547088/how-do-i-customize-facebooks-sharer-php), such as summaries and images, allowed previously in this scheme but the prefered way now is for you to define these using open graph meta-data (see below).

### Twitter

```html
http://twitter.com/share?text=text goes here&url=http://url goes here&hashtags=hashtag1,hashtag2,hashtag3
```

### Google+

```html
https://plus.google.com/share?url=your-page-url
```

Google uses it's own meta data format to specify custopm images etc. but it will fall back to open graph if that's what is available.

### Pinterest

With the pinterest share, it needs to have an image source on the end like this:

```html
http://www.pinterest.com/pin/create/button/?url=example.com&description=blabla&data-pin-do="buttonPin"&data-pin-config="none"&media=example.com/image.jpg
```

or 

```html
&img src=example.com/image.jpg
```

## Open Graph
[Open Graph Protocol](https://developers.facebook.com/docs/opengraph/) meta data is used among other things to supply data about your article when sharing. This data goes in the head of your html page, for [example](http://ogp.me)

```html
<html prefix="og: http://ogp.me/ns#">
<head>
<title>The Rock (1996)</title>
<meta property="og:title" content="The Rock" />
<meta property="og:type" content="video.movie" />
<meta property="og:url" content="http://www.imdb.com/title/tt0117500/" />
<meta property="og:image" content="http://ia.media-imdb.com/images/rock.jpg" />
...
</head>
...
</html>
```

This open graph data is used by FaceBook, Twitter, and Google+ amongst others to determine how to share or include your content.
