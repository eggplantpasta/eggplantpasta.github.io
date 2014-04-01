---
layout: post
title: So what now?
description: "Installing Jekyll on OS X."
modified: 2014-03-27
category: articles
tags: [blog, jekyll, github pages, ruby, os x, homebrew]
share: true
---

It makes sense that the first thing I should document is how I got GitHub pages up and running with Jekyll.

I use OS X on my MacBook Air. If you're using OS X for any programming at all the first thing you should do is download and install XCode and the command line tools. You can get them both from the App Store. I'm just saying that up front becaue no one else seems to bother to mention it and I learned it, sadly, at the *end* of the install process (see bottom of page).


## tl;dr

The following is what I *should* have done to set up my GitHub user pages.

* Install [XCode](https://itunes.apple.com/au/app/xcode/id497799835?mt=12) and command line tools from the App Store.

* Create a [new repository](https://github.com/new) named eggplantpasta.github.io.

~~~bash
cd ~/Git
git clone https://github.com/eggplantpasta/eggplantpasta.github.io
cd eggplantpasta.github.io
echo "Hello World" > index.html
git add --all
git commit -m "Initial commit"
git push
~~~

* Check the new page is being served correctly at [eggplantpasta.github.io](http://eggplantpasta.github.io) (it could take up to 10 minutes to appear for the first time).

* Install homebrew and run `brew doctor` to ensure the environmnet is sane.

~~~bash
ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"
brew doctor
~~~

* Install [RVM](http://rvm.io) and Ruby, add to the path, and install dependencies (this may take a whie). 

~~~bash
\curl -sSL https://get.rvm.io | bash -s stable --ruby --auto-dotfiles
printf "\nsource ~/.profile" >> ~/.bash_profile
rvm requirements
~~~

* Install Jekyll and set up a new site.

~~~bash
gem install jekyll
rm README.md index.html
jekyll new .
jekyll serve --watch
~~~

* Go to [http://localhost:4000](http://localhost:4000) to check the local site is being served.

~~~bash
git add --all
git commit -m "Initial Jekyll commit"
git push
~~~

* Go to [eggplantpasta.github.io](http://eggplantpasta.github.io) to check the local site is being served.

Your work here is done.

## The epic saga

The following is what actually happened.

### GitHub Pages

I started reading the documentation at GitHub for [GitHub Pages](http://pages.github.com). That was pretty straight forward and I ended up with a "Hello World" being served from [here](http://eggplantpasta.github.io) in short order.

### Jekyll

The next thing was to get going on [Jekyll](http://jekyllrb.com). The quickstart on that first page was unclear about which level I should create my project in relation to the root of the repository (turns out it **is** in the root).

I googled around and found this awesome [24 Ways article](http://24ways.org/2013/get-started-with-github-pages/) which gave me a kickstart on the rest.

In the initial setup it talked about using a repo branch called "gh-pages" but because I was setting up a user page, not a project page, I finally figured out I could ignore that bit.

At the part where I needed to install Jekyll `sudo gem install jekyll` I received an error along the lines of `ERROR: Failed to build gem native extension.`

### Down the rabbit hole

Following a [link](http://andytaylor.me/2012/11/03/installing-ruby-and-jekyll/) from the 24 ways article I switched to new instructions. I already had the [OS X command line tools](https://developer.apple.com/downloads/index.action) installed[^1] so onto the next bit; installing [Homebrew](http://brew.sh).

### Homebrew

Of course the instructions didn't work for me - they never do.

~~~
ruby -e "$(curl -fsSkL raw.github.com/mxcl/homebrew/go)"
curl: (22) The requested URL returned error: 404 Not Found`.
~~~

A quick trip to the [Homebrew homepage](http://brew.sh) got me the correct install command:

`ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"`.

### The Doctor

At the end of this smooth install process I noticed a message saying `You should run 'brew doctor' before you install anything`. Always one to follow instructions, I dutifully did so only to be presented with a few screenfulls of warnings. Bummer.

`Warning: Broken symlinks were found. Remove them with 'brew prune'`

Well that was easily fixed.

`Warning: You have MacPorts or Fink installed`

I'd installed MacPorts over a year ago to install something-or-other. Since Homebrew seemed to be the package manager in vogue I felt no qualms in [uninstalling it](https://guide.macports.org/chunked/installing.macports.uninstalling.html).

`sudo port -fp uninstall installed` began clearing out way more than I remembered. Oops. Well we'll see if thats a bad thing later. I figure I can reinstall things using homebrew if I need to anyway.

`Warning: Your XQuartz (2.7.4) is outdated`

The [update](https://xquartz.macosforge.org/landing/) was long running but straight forward and sucessful.

`Warning: /usr/bin occurs before /usr/local/bin`

And finally just an edit of my `.bash_profile` leading to `Your system is ready to brew`. Yay!

### Installing RVM

I checked the [source](http://rvm.io/rvm/install) this time but the instructions were correct so I went ahead. Seems I had installed RVM previously (see what I mean about forgetting) but it went ahead and updated my install giving me the warning: 

`RVM PATH line not found for Zsh, rerun this command with '--auto-dotfiles' flag to fix it.`

Ok. I did what it told me to and this time I get told:

~~~
  * WARNING: You have '~/.profile' file, you might want to load it,
    to do that add the following line to '/Users/brett/.bash_profile':

      source ~/.profile
~~~

Alrighty. I did as told. Previously I had copy pasted the contents into `.bash_profile` but since it will only create it again I went with it's suggestion of `source`.

### Jekyll again 

`gem install jekyll`

Nope. `Gem::FilePermissionError`.

Ok. `sudo gem install jekyll`

Nope. `clang: error: unknown argument:`

Seems I [have to install cc-4.2](http://stackoverflow.com/questions/21664841/unable-to-install-jekyll-on-mac-osx-10-9-1-with-xcode-and-rvm-installed).

`brew install apple-gcc42`

Nope. seems I am [missing make](http://stackoverflow.com/questions/10725767/error-installing-jekyll-native-extension-build) which I can get by installing XCode (which I'd recently removed to make room). Curse you you miniscule SSD. So does that mean I didn't need apple-gcc42?

`brew uninstall apple-gcc42`

Now I'm following [these](http://davidensinger.com/2013/03/installing-jekyll/) instructions. Cross fingers.

XCode installed from app store.

Another check of `brew doctor`.

Which tells me to start XCode and agree to licence.

`rvm requirements` seems to be installing gcc46... it takes a loooong time (or perhaps it's crashed). Nope `top` seems to show make and clang and the fans are spinning wildly. More internet reading then... Facebook bought Occulus Rift! [Strange days indeed](https://www.youtube.com/watch?v=gBCdlBrgEmE).

Requirements installation successful.

`rvm install ruby` to get the latest stable version...

and finally `gem install jekyll`.

You can always add `--no-rdoc --no-ri` to a gem install to skip the documentation and save a little time and space.

### Finally

Time to create a new Jekyll website. First move the index.html and readme.md out of the way as jekyll expects an empty directory (it doesn't seem to mind the .dot files though).

~~~
jekyll new .
New jekyll site installed in /Users/brett/Git/eggplantpasta.github.io.
~~~

Generate the site and run the local server.

`jekyll serve --watch`

[Tada!](http://localhost:4000)

I fiddled a bit after this with the files but I'm leaving the actual real development using Jekyll to next time.

Push to GitHub, check, then bedtime.

[^1]: [That was my mistake](https://www.youtube.com/watch?v=9AKQ2H4QW9M).