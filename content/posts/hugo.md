---
categories:
- Intro
date: "2015-06-27T13:45:30-07:00"
draft: false
tags:
- Hugo
- Blogging
title: Hugo
---

I met [SPF13](http://spf13.com/) last year -- remembered having a good chat with him and when I was
thinking about my blog, I considered various options:

* [Jekyll](http://jekyllrb.com/)
* [blogger](https://blogger.com)

Then I remembered Hugo.

It's been a very long time since I created a blog – I've owned AngelTech.com for a very long time,
but that's hosted w/o https certificates, and is a pain to move, due to locked DNS entries, so
I thought I'd try hosting on [Github pages](https://pages.github.com/).
(*ed note* later moved to firebase hosting)

Anyway, Steve (SPF13), wrote [Hugo](http://gohugo.io/) in [Go](http://golang.org/) which sounds a lot
more efficient than Jekyll's use of Ruby. (Never a fan of scripting languages).

So far, I'm quite happy with it, I'm about a 30 minute user.  At this point, I've found that many of
the available templates don't work right out of the box, w/ the exception of the list below. (I tried
them all)

Issues
--
1. When there is no theme, it still hangs in server mode.
2. Changes to config.toml don't get pickedup durring --watch

My Preferred Themes
--
* lanyon -- Black & White -- really good looking & behaving.
* [journal](https://github.com/mpas/hugo-journal) -- delightful = lots of red -- some tweaks needed.
(I chose this one!)
* hugoscroll -- delightful big colors -- needs customization

Other Themes
--
* greyshade -- good  (modify the about)
* heather-hugo -- good
* hyde -- good
* herring-cove -- good (near empty home page)
* html5 -- good -- very sparce home page -- no basic width
* hugo-base-theme - good - needs mods  -- huge picture
* hugo-bootswatch - Very nice
* hugo-incorporated -- Really like -- missing About, has XML
* landing-page-hugo -- really nice looking, not for me.
* liquorice -- nice bw theme -- missing about
* nofancy -- simple nice.
* pixyll -- Nice - big & bold - bw
* shiori -- very professional -- missing about
* simple-a - nice -- very sparse
* slim - weird UX
* tachyons -- nice, but full screen -- awkward for blogs.
* tinyce -- minimal, missing about - Missing para breaks
* twentyfourteen -- lots of search boxes -- very long lines

Now I'm about 2 hours into it.  Still happy -- but disappointed at the Theme quality.
