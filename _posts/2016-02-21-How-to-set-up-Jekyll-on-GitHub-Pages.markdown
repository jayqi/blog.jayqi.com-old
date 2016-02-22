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


## A git workflow to deal with theme templates 

In addition to using git to manage my website's production files, I want to easily keep up-to-date with changes I might separately make to the theme's repo. I also want to be able to work on theme files in my local repo and get those changes incorporated into the theme's repo. 

### Aside: a small rant

It feels like by virtue of using version control software like git, it should be easy to have a scheme where one can keep the website theme template up-to-date, right? Weirdly, there is not a lot of info I could find via Google on what the best practices for this are. 

One general git tool, [submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules), seems like it's meant for this sort of thing. Unfortunately, it doesn't work. A submodule need to be completely contained in a single subdirectory of your repo. With Jekyll's file structure, the multiple things you'd want from a theme template like **_layouts/** and **css/** are mixed in with things you'd be customizing for your site, like **_config.yml** and **_posts/**. The only way to get it to work is to split the theme up into a whole bunch of separate repos for each directory, which doesn't make any sense conceptually or practically.

Putting the theme into one subdirectory (e.g., **source/**) and then symlinking to the relevant theme files (e.g., **index.html** and **_layouts/**) does not work either. Jekyll will not build symlinks into **_sites**.

So there isn't a good way to keep template files separate from customized files. The only way to manage changes is use ``git merge`` and hope that the conflicts aren't too complicated. 

### Branches and merging

I use branches to separate my website production files from a clean copy of the theme template. Atlassian has a pretty good [guide to how branches work](https://www.atlassian.com/git/tutorials/using-branches/git-branch). This isn't a necessary thing to do but helps me keep organized. 

I have two branches:

* **master** -- where I keep my production files
* **template** -- where I keep a clean copy of the template

The new branch can be created with the command  
    
    git branch template

Then I swapped to the **template** branch and set its upstream remote to **upstream**.

    git checkout template
    git --set-upstream upstream

That way whenever I need to get changes from the **upstream** GitHub repo, I can swap to it and pull down the changes

    git checkout template
    git pull
Similarly, I can also push local template changes to **upstream**

    git push upstream template:master
The ``template:master`` is there because otherwise commits will be pushed to a **template** branch on the remote instead of **master**. 
    
When I want to work on my blog, I can use ``git checkout master`` to make **master** the active branch and have my production files in my working directory.

If I need to merge changes from **template** into **master**, I can checkout master and then use

    git merge template --no-ff
to merge changes. Similarly, I can also merge template file changes from **master** into **template** the same way by doing the commands with the opposite branches. 

The two branches aren't really necessary. I could always merge directly from **upstream** into **master**, and push template changes directly from **master** to **upstream**. However, keeping the two branches makes it easier for me to conceptually keep the production website separate from the template. 

## Previewing locally

To preview my website locally, I installed the **github-pages** gem following the advice of the [GitHub Pages documentation](https://help.github.com/articles/setting-up-your-pages-site-locally-with-jekyll/).

First, make a **Gemfile** containing

    source 'https://rubygems.org'
    gem 'github-pages'
Then, you can use

    bundle exec jekyll build --safe
to build the website into **_sites/** and

    bundle exec jekyll serve
to have it viewable locally at http://localhost:4000/. If you have draft posts in the **_drafts/** folder, you can run 

    bundle exec jekyll serve --drafts
to include them.

## Publishing to GitHub

The remote **origin** should be pointing to the ***yourusername*****.github.io** repo on GitHub and be set as the upstream for **master** already. I ended up renaming it to **live** with

    git remote rename origin live
because it felt more descriptive to me.

Then, publishing is easily done by using committing changes and 

    git push live master
    
And that's it. 