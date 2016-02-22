---
layout: post
title: Blog beginnings, Jekyll, and GitHub Pages
date: 2016-02-21 01:00:00
tags: web dev, jekyll, github
---

This will be the first of hopefully many posts on my new blog. (Anu tells me that "hello, world" doesn't really count.) Blogging has been one of those things I've had in the back of my mind for a while. It gives me the opportunity to practice writing and---at the same time---document interesting things that I learn to both share with others and for myself to look back on later. 

## Jekyll and GitHub Pages


This blog uses the [Jekyll](https://jekyllrb.com/) static site generator and is hosted on [GitHub Pages](https://pages.github.com/). A few years ago, I had started a [blog at Wordpress.com](https://jyqi.wordpress.com/). Before starting up again this time, I did some research and settled on my current system for the following reasons:

* While Wordpress.com is a free service, using my **custom domain** (jayqi.com) would require paying $13/year. GitHub Pages lets me do it for free. 
* Static site generators are more **lightweight and simple** than dynamic content management systems (CMS) like Wordpress. Smashing Magazine has a [nice article](https://www.smashingmagazine.com/2015/11/modern-static-website-generators-next-big-thing/) about the recent rising popularity of static sites.
* **GitHub Pages can host a Jekyll static site for free.** I could host either a CMS like Wordpress or a static site on my DigitalOcean droplet, but why use the bandwidth if I don't have to? 
* A good opportunity to **practice common software development techniques** like version control and Markdown. 

There are many open-source static site generators---[StaticGen.com](https://www.staticgen.com/) has a directory. Jekyll is the most widely used one, being one of the oldest and with direct support by GitHub Pages, so it seemed like a good choice. I could, of course, also use a different static site generator, build the site locally, and push the built html pages to GitHub Pages. However, I liked Jekyll because it is widely used (easier to find help), simple (Octopress is for example more feature-rich but more complicated), and actively developed. 

## Strata Alt theme

The [Jekyll theme I'm using](https://github.com/jayqi/Strata-Alt-Jekyll-Theme) is customized from [Strata-Jekyll-Theme](https://github.com/CloudCannon/Strata-Jekyll-Theme) by [CloudCannon](https://github.com/CloudCannon), which in turn is based on the [Strata template](http://html5up.net/strata) by [HTML5 Up](http://html5up.net/). Google "html template" and HTML5 Up is sure to be one of the top results. I'm a fan of HTML5 Up's aesthetics, and I'm already using the [Identity template](http://html5up.net/identity) as my splash page at [jayqi.com](https://jayqi.com/). I was looking for a left-sidebar-style template, and none of the other ones at [Jekyll Themes](http://jekyllthemes.org/) convinced me. The templates at HTML5 Up free under a [Creative Commons license](http://html5up.net/license), and they are also nice because they're [responsive](https://en.wikipedia.org/wiki/Responsive_web_design), meaning that the layout adapts to different display sizes for different devices. 

I've customized the template a bit to suit myself---for example, I reduced the sidebar from 35% to 25% when viewing at desktop resolutions. I'm planning to maintain my version of the Strata Jekyll theme on GitHub at [jayqi/Strata-Alt-Jekyll-Theme](https://github.com/jayqi/Strata-Alt-Jekyll-Theme) in the spirit of open source. 

## How to do it yourself

In the interest of not making a massive wall of text, I will detail how I set up the blog in a [separate post](2016/02/20/How-to-set-up-Jekyll-on-GitHub-Pages.html). 