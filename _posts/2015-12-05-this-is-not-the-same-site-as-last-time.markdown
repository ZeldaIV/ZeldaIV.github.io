---
layout: post
title: This Is Not the Same Site as Last Time.
modified:
categories: blog
excerpt:
tags: []
image:
  feature:
date: 2015-12-05T10:33:25+01:00
---

For those of you who have visited my page before, you may have noticed that the page looks very different than last time you visited.

**Heres why:**

It's been years since I did anything web-related, so when I finally wanted to create a website, I wanted to get up and running as fast as possible. Blinded by the eager to get started, I chose the quick solution: [Wix][wix]. I did not spend enough time reading up on the documentation, as I did not really know what I was looking for, or what I needed. I just wanted a site, and I did not want to host it myself.

Wix does an amazing job of letting you get started fast, and it is very easy to implement a lot of great features. If you want a site with a blog, you just drag the blog app on to your site, and you have a blog. Want comments? Just drag the comments app, and voilá you have comments. You get everything you need, just a few clicks and drags. Even integration with [Google analytics][google_analytics] was a breeze to setup. Wix provides a very nice user interface and is very easy to use. They have really done a great job at creating a good tool to get up and running fast with a site. They even have quite a few good looking themes you can use.

Everything was looking good. I was somewhat pleased with the design, and the features the site offered. So what happened? Well, as I was working on the post about [Automate Pod Spec Pushing][automate_pod_spec] I really wanted to show some of the code I was using, some sample scripts to get you up and running with your own solution. I needed some way of displaying code like they do on [Stack Overflow][stackoverflow] with syntax highlighting. I discovered to my great disappointment that there was no easy way of accomplishing this on Wix. Their blog does not support html-editing, so there was no way to have their blog do this. Linking to other sites, such as gists in GitHub just was not an option. But I could use the [Google blogger][blogger] app instead, and use the [SyntaxHighlighter][syntaxhighlighter], after a bit of fiddling with this, it just was not possible to make it work, as the 0 reponses to my [StackOverflow question][stackoverflow_question] so clearly demonstrates.

In my search to make this work I discovered something new; [GitHub Pages][github_pages] and [Jekyll][jekyll].
So GitHub can host my site directly from my git repository, I get a great tool for developing the site, and it is all under version control. Wow! I was impressed, and quite quickly realized this was what I needed. My posts are now written in markdown with support for syntax highlighting in an easy way. I can still use my domain, and it is easy to create new posts with [Octopress][octopress].

All I had to do to get started was run these commands:
{% highlight bash %}
$ gem install jekyll
$ jekyll new theBlog
$ cd theBlog
$ jekyll serve
{% endhighlight %}

But I recommend if you want to start you own, and don't want to design too much, check out [Made Mistakes][made_mistakes].

My work process is now start the server locallay with this command:
{% highlight bash %}
  $ bundle exec jekyll serve --watch
{% endhighlight %}

The --watch flag makes jekyll watch for changes in files and updates the site if it finds any.
This makes it really easy to check how the site or a post looks.

Create a new post with Octopress:
{% highlight bash %}
  $ bundle exec octopress new post "Post title"
{% endhighlight %}

I then write the post in my favorite editor. Which is [Atom][atom] right now.

When I am pleased with my post, I just run:
{% highlight bash %}
$ git add .
$ git commit -m 'New post'
$ git push
{% endhighlight %}

A new post is available on the web.

I am really impressed about what Jekyll, Octopress and all the other plugins and theme-makers have pulled of, that I regret I did not discover this earlier. But I guess this is what it is like to explore new territory. Makes me wonder what other great tools exists, yet to be discovered.



[wix]: http://wwww.wix.com
[google_analytics]: https://www.google.com/analytics
[github]: https://www.github.com
[jekyll]: http://jekyllrb.com
[automate_pod_spec]: {% post_url 2015-11-28-automate-pod-spec-pushing %}
[stackoverflow_question]: http://stackoverflow.com/questions/34015369/syntaxhighligter-not-working-in-blogger-resources-not-found
[blogger]: https://www.blogger.com
[github_pages]: https://pages.github.com
[syntaxhighlighter]: http://alexgorbatchev.com/SyntaxHighlighter/
[octopress]: http://octopress.org
[made_mistakes]: https://mademistakes.com/work/jekyll-themes/
[atom]: https://atom.io
