---
layout: post
title: Automate Pod Spec Pushing
modified:
categories: blog
excerpt:
tags: []
image:
  feature:
date: 2015-11-28T20:13:00+01:00
---

If you have ever used private pods, you are probably familiar with the process of updating the version number, lint the pod, and then push it up to your private repo. If you on top of that use git-flow as you work process, which I highly recommend that you do, you have to decide when to push your spec. Should you do this on the developing branch, the release branch or on the master branch. Well the pod will probably refer to the version you tag the commit with, so it makes sense to push the spec on the master branch.

But if the library you have is a multiplatform library, you may not be the one developing this library, and it may not even be developed on OS X. This means you or someone else on a mac will have to deal with updating the pod spec. Of course this is possible, but it is actually alot of extra work, let me try to describe the process.

First of all, the person responsible for the library have to publish the release branch, then you (or whoever will update the pod spec) will have to pull the release branch, update the pod with the new version. Then you lint, to check if everything is ok, but you do not want to push the pod yet, as anyone else using this pod, might update, and get the new version, which is not available yet because you are still on the release branch, and the tag does not exist yet. So you have to push the release branch, wait for the responsible person to finish the release, and once everything is in the master branch, with tag and all, you can push the pod. After you pull the repo again of course.

{% highlight swift %}
func test() {
  var you = "none"
  let this = true
  println(you)
}
{% endhighlight %}

Dealing with all this is somewhat cumbersome, so I propose a different solution:
Let your CI do the job.

Here is how I have done it.

1. Create a template for you podspec in the repo of the source code.
2. Create a script that can update the version, and push the spec.
3. Make the script available to your CI.
4. Whenever the master branch is beeing built on your CI the script will automatically run, updating the version to the current tag, lint the spec and push it.

I have even done this for the develop branch so that it is possible to get snapshot versions of the library, to develop things in parallell. An extra added bonus is that if the linting fails on your CI you will know immediately you have to fix something, be that new source files or other dependencies. Also you can have the version in you pod formatted like this: x.y.z-SNAPSHOT so anyone using that pod knows it is under development.

This actually makes sense in several ways. You skip the whole cycle of pulling and pushing the release branch of the library. The pod repo will be updated every time your CI builds either the snapshot or the final release. You don't have to fiddle around with manually updating the spec.

Let me know if you have any opinions in regard to this.
