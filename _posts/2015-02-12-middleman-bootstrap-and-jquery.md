---
layout: post
title: Middleman, Bootstrap, and jQuery
categories: [stupidly simple tips]
tags: []
published: True

---

*New category. Stupidly Simple Tips. For all the minor pieces of information I find that should be easy to find online, but for some bizarre reason just aren't. Some of these may be glaringly obvious. Some of them won't. Either way, I hope they help someone avoid my bits of aggravation.*

# The Problem

Using [Middleman](https://middlemanapp.com/)? You should be. It's fantastic (yes, this blog is on Jekyll until I have time to move it, *hush*). What's that? You also love [Bootstrap](http://getbootstrap.com/)? What a coincidence, we're peas in a pod, you and I. 

Just add this to your gemfile[^middleman]:

```
gem "bootstrap-sass", "~> 3.3.3", :require => false
```

Next step, rename ```all.css``` to ```all.css.scss``` and add the following to the top of the file:

    @import "bootstrap-sprockets";
    @import "bootstrap";

As a bonus, if you want a bunch of awesome helpers that are detailed in some [slick documentation](http://fullscreen.github.io/bh/), then add this to your gemfile:

```
gem 'bh', '~> 1.2'
```

And this to your config.rb:

```
activate :bh
```

But let's say you're *really* crazy. Let's say you do all that and and then expect all of the Bootstrap jQuery methods to *just work* because you're new to static site generators and half-assumed that the Bootstrap gem would have a dependency on jQuery and pull in the relevant gem(s) so that things like drop-down menus would be functional from the start. HA! Nope. As much as you may want your elements to prance about the screen, you're stuck in static land.

# The Solution

Add this to your gemfile:

```
gem "jquery-middleman"
```

And add these lines to your all.js under "source > javascripts":

    //= require jquery  
    //= require bootstrap-sprockets

Run ```bundle install```, and you should be good to go. If not, try the standard steps of restarting the server and clearing the cache. 

# In Sum

In hindsight these lines are blindingly obvious, but they're nowhere in the Middleman docs. Well, to be perfectly fair they are *alluded* to in the docs, but I'm guessing I'm not the only Middleman beginner that has missed the obvious. Or I'm just attempting to balm my injured pride. Either way, if you needed this info laid out explicitly, there you go. Hope I saved you some ranting. 

<br>

---

<br>

[^middleman]: The specifics on why you use ```:require => false```, and allusions to including jQuery, are actually in the [Middleman documentation here](https://middlemanapp.com/advanced/asset_pipeline/).