---
layout: post
title: A Talk About Functional Programming
modified:
categories: blog
excerpt:
tags: []
image:
  feature:
date: 2015-11-29T13:15:00+01:00
---

Earlier this year [Inge Solvoll][ingesol] and I decided we wanted to do a talk about functional programming at this years [Trondheim Developer conference][tdc-2015], and the benefits of choosing functional programming. We decided that it would be fun if we could perform live coding ( which seems to be popular nowadays), building a working app. So to make things a bit exciting we built a server in Clojure, and an iOS-app. The server will push football events to the iOS-App, and the user can choose to see all events at the same time, or follow only a selected match. We also implemented search functionality. 

To make this work we landed on using [Reactive Extensions][reactivex] for the iOS-app, which is a fairly small library, and quite easy to use. It allows you to make observables of pretty much anything, and has a very rich functional API.

You can find the source code for the [iOS-App][ios-app] and the [Clojure server][clojure-server] on GitHub.

This talk is In Norwegian (my apologies to any english speaking visitors).
{% include vimeoPlayer.html id=146478440 %}






[tdc-2015]: http://2015.trondheimdc.no
[ingesol]: http://twitter.com/ingesol
[reactivex]: http://reactivex.io
[ios-app]: https://github.com/ZeldaIV/TDC2015-FP
[clojure-server]: https://github.com/ingesolvoll/tdc-clj
