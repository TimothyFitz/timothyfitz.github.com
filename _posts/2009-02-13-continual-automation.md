--- 
layout: post
title: Emergent Properties of Continual Automation
tags: []

status: publish
type: post
published: true
meta: 
  _edit_last: "6738078"
---
Once a task has been automated to take dramatically less time, a threshold is crossed and  at which point you can exploit emergent properties.<strong> Or in other words, crazy-ass improvements.</strong>

While the most dramatic examples I have relate to our test and <a href="http://timothyfitz.wordpress.com/2009/02/10/continuous-deployment-at-imvu-doing-the-impossible-fifty-times-a-day/">deploy</a> infrastructure, I'll skip rehashing those here.

Most companies manage to end up with weeks of effort required to create local development environments. I've heard stories of major bay area companies with internal package management hell that meant there were only two or three people in the entire (thousands of employees) company that could actually create working development setups.

How automated can this process get? At IMVU the entire setup process for our website is an SVN checkout and running a script. At that point a local instance of apache and memcache are running. Port 80 is serving up a local development copy of the website. <strong>There is no work left. </strong>

What does this level of automation give you? Here's where things start to take off. Now I can easily install a sandbox on my home machine, on my laptop or even on an EC2 instance all without effort. I can start to parallelize my work effort: run regression tests on one machine, poke at code to understand it on the other. We can one-off install sandboxes on machines to run data crunching. This is how we've generated the numerous incarnations of rendered 3d art in our registration flow. 

When we spin up new engineers we target a working sandbox by lunch and a typo fix live in production by end of day. <strong>On the first day of their employment. </strong>This is one of our best ways to demonstrate our cultural differences from most development shops.

We can give sandboxes to marketing, and have them develop promotion materials against instantly up to date code. Marketing can run tests (which they occasionally break!) and even commit and push material live to the website. This isn't just saving engineering time, it's allowing marketing to be dramatically more effective. No more telephone or bouncing e-mail the mockups back and forth.

Instead of resorting to complicated test-cluster setups, our testing pipeline is just fourty seperate sandboxes operating with full parallelism. Should a machine break, or some other stray-electron corrupt an install, it's a tiny amount of effort to restore the machine from a fresh state.

More importantly, our sandbox install and update procedures are the same thing. It's incredibly easy to experiment with new features, software packages or other setup changes and have every other developer running with them at their next code update. We've experimented with different versions of php, including switches to toggle between php4 and php5. We added Privoxy to flag accidental 3rd-party dependencies in Selenium, solving a large class of accidental test dependencies.

All of these benefits are amazing, but <strong>what was more incredible is that we didn't really anticipate any of them.</strong> This is emergence at its finest. In dramatically lowering the cost of sandbox creation we dramatically lowered the costs of numerous dependent activities, and in doing so we changed the very shape of our development practices. This is the application of<a href="http://groksystems.com/"> Systems Theory</a> at it's finest.

<strong>We didn't get here overnight.</strong> We didn't get here in a few weeks. We didn't get here by funding a project. We got here by a culture. That culture overridingly said, if you did it twice it's time to start automating. Every time you repeat a task, make progress on automating it. It doesn't have to be big, flashy, bold or fanciful. It just has to be progress. You'll quickly find this culture reinforces itself, automating common tasks makes other engineers want to automate them even more.

Sometime today you will come across a task that you've done before. You'll notice the commands are coming from muscle memory or the steps are fully documented. <strong>Automate it</strong><strong>. If not now, then when?</strong>
