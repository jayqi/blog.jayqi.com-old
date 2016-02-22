---
layout: post
title: How to set up Jekyll on GitHub Pages
date: 2016-02-21 02:00:00
tags: web dev, jekyll, github
---

In my [previous post]({{ site.baseurl }}/2016/02/21/Blog-Beginnings-Jekyll-and-GitHub-Pages.html), I discussed why I chose [Jekyll](https://jekyllrb.com/) and [GitHub Pages](https://pages.github.com/) for my new blog. In this post, I will document how I set things up. 

The GitHub Pages website has a [guide for setting up your site](https://pages.github.com/#tutorial) and another [guide for setting up Jekyll](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/). They are good general resources, but I will discuss the specifics of about what I did. 

## Getting started with a template

The vanilla Jekyll theme is pretty barebones, so I imagine most people will want to use a template. There are [many](https://github.com/jekyll/jekyll/wiki/Themes) [theme](http://jekyllthemes.org/) [directories](http://themes.jekyllrc.org/) [to check out](http://jekyllthemes.io/), though they have quite a bit of overlap. 

If you want to use a Jekyll theme that is in a repository hosted on GitHub, a good practice seems to be to fork a copy for yourself. That way, the original theme is a remote for your copy and you can fetch and merge any updates that might get made to the theme. 

You can simply rename your forked repo to ***yourusername*****.github.io**, and your site will be live. (GitHub will build a Jekyll site automatically.) You can then clone your repo to your local system. Before actually beginning to write and publish posts, I recommend taking a look at the next section about my version control workflow.

In my case, I had to jump through a few extra hoops because I wanted to maintain a [separate repo for my version of the Strata theme](https://github.com/jayqi/Strata-Alt-Jekyll-Theme). If you don't care about that, you can skip to the next section. Following [this tip on forking your own GitHub repo](http://kroltech.com/2014/01/01/quick-tip-how-to-fork-your-own-repo-in-github/), what I did was:

* Fork the template I wanted to use. In my case, I forked CloudCannon's [Strata-Jekyll-Theme](https://github.com/CloudCannon/Strata-Jekyll-Theme) and renamed it to [/jay/Strata-Alt-Jekyll-Theme](jayqi/Strata-Alt-Jekyll-Theme). This is where I'm going to maintain my development of the theme. 
* Create a blank repo ***yourusername*****.github.io** on GitHub where my site will be deployed. 
* Clone the GitHub ***yourusername*****.github.io** repo to my local machine. The local repo will automatically have the GitHub repo as a remote named **origin**.  
``git clone https://github.com/jayqi/jayqi.github.io.git``
* Add the forked template repo (for me, jayqi/Strata-Alt-Jekyll-Theme) as a remote named **upstream** to my local repo.  
``git remote add upstream https://github.com/jayqi/Strata-Alt-Jekyll-Theme.git``
* Pull a copy of the forked template repo (for me, jayqi/Strata-Alt-Jekyll-Theme)  
``git pull upstream master``


## A git workflow for web development using templates 

### Aside: a small rant

It feels like by virtue of using version control software like git, it should be easy to have a scheme where one can keep the website template up-to-date, right?  


One general git tool, [submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules), is meant for this sort of thing, but unfortunately, didn't work. A submodule need to be completely contained in a single subdirectory of your repo. With Jekyll's file structure, the multiple things you'd want from a theme template like **_layouts/** and **css/** are mixed in with things you'd be customizing for your site, like **_config.yml** and **_posts/**. The only way to get it to work is to split the theme up into a whole bunch of separate repos for each directory, which doesn't make any sense conceptually or practically.

Putting the theme into one subdirectory (e.g., **source/**) and then symlinking to the relevant theme files (e.g., **index.html** and **_layouts/**) does not work either. Jekyll will not build symlinks into **_sites**.

### Branches and merging


## Previewing locally