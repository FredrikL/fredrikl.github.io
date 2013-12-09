---
layout: post
title: Recent changes
status: publish
type: post
published: true
---

So I've made some (mostly) under the hood changes to this blog. Lets start with the visible part I've dropped the blog part from the domain, the redirect is permanent but it might be a good idea to update your rss feed.

The fun parts are that the blog has moved from wordpress to using [jekyll](http://jekyllrb.com/) and is hosted on github from [this](https://github.com/FredrikL/fredrikl.github.io) repository. Migrating to jekyll was rather simple, there's plugins that support conversion from a wordpress backup xml file to jekylls structure. Since I liked the theme ([decode](https://github.com/ScottSmith95/Decode)) used on the wordpress site I 'ported' it to jekyll, or well cherry picked some parts and removed most things that I didn't need. Since I also moved the blog up from blog. to the top level I had to support the old links too, that is done using a [nginx](http://nginx.org/) instance that does a redirect (301, permanent) from blog.* to the top level with the path intact.

A big bonus with jekyll is that I can write my posts in [markdown](http://en.wikipedia.org/wiki/Markdown) and they are stored as simple text, no weird database or anything.

When I moved of one.com I lost my mail account that was connected to the domain, and since google apps doesn't accept any new accounts for free anymore I looked around for an alternative that could work. While outlook.com does offer custom domain hosting if looked around a bit more and found [zoho](http://www.zoho.com/mail/) they offer a bit less space per account than google but has pop3/imap access and overall as fast as gmail.