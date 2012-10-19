--- 
layout: post
title: What webhooks are and why you should care
tags: []

status: publish
type: post
published: true
meta: 
  _edit_last: "6738078"
---
 Webhooks are user-defined HTTP callbacks. Here's a common example: You go to github. There's a textbox for their code post webhook. You drop in a URL. Now when you post your code to github, github will HTTP POST to your chosen URL with details about the code post. There is no simpler way to allow open ended integration with arbitrary web services. 

This tiny interface is used in obvious ways: bug tracking integration, sms messaging, IRC and twitter.

The same tiny interface is also used in non-obvious ways, like Run Code Run which offers to build and run your project's tests for you. All by just plugging a runcoderun.com URL into GitHub. 

Webhooks today offer a lot of value as an instant notification mechanism. Have events your users care about? Give them a webhook for those events and you've given them the power and flexibility to integrate that event stream into their life. 

For all of that power, webhooks are impressively simple to implement. It's a one liner in almost every language.

{% highlight python %}urllib.urlopen(user.webhook.url){% endhighlight %}

While there's a lot of value in webhooks today, it's the future that really interests me. Webhooks are composable. You'll point a webhook at a site that will call other webhooks. It might process the data, record it, fork it off to multiple webhooks or something stranger still. Yahoo Pipes tried to do this, but ultimately you were limited to what Yahoo Pipes was designed to do. Webhooks can be integrated and implemented everywhere. They piggyback the fundamental decentralized nature of the web. 

I imagine a future where twitter feed updates instantly call a webhook. I've pointed that webhook at a service that does bayesian filtering. The filtering has been set up to determine if the tweet looks time-sensitive "Anyone interested in getting dinner tonight?" vs time-insensitive "Webhooks are cool." Time sensitive posts call another webhook, this time set to sms my phone. Note that nowhere in this future am I writing any code. I don't have to.

It's important that we get to this level of customization for the masses. It's also important for adoption that we use the web's native verbs. We understand HTTP on a fundamental level. It's simple, scales and makes sense. 

You should care because webhooks will be ubiquitous. You should care because they're going to reshape the internet. You should care because webhooks are the next step in the evolution of communication on the internet and nothing will be left untouched.
