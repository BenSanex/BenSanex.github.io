---
layout: post
title:  "New blog"
date:   2023-08-02 19:57:57 -0500
categories: blog post
---
I found it highly inappropriate that as a professional web devleoper my personal site was garbage. Granted it was written 7 years ago when I was just learning what I was doing. Now since I do this professionally I do'nt wnt to have to deal with the same frustrations I do all day and end up figuring out some other cloud provider so I discovered that github pages works with this jekyll thing and I'm rolling with that for now. Its cheap and seems pretty easy so far although my first attempt at this post got steamrolled into another *Welcome to Jekyll!* post. I'm leaving that one there just for my own reference because this site is for me anyway I do what I want.

For future me (or someone unlucky):

[Github get started page](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

Some notes from my install
1. Ruby comes with `bundle` already so no need to install it on your own.
2. Make sure to get Ruby with the dev kit. The winget package name was wrong in the Ruby docs. I used `RubyInstallerTeam.RubyWithDevKit.3.2`
3. Make sure you're doing your `jekyll new` in either the root of the repo or in `/docs` because this is what github pages looks at to serve your site.
4. Still not sure what to put in config.yml for `baseurl`
5. I needed to add `gem webrick` to the gemfile. Idk if its a windows thing or what.