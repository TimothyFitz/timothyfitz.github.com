--- 
layout: post
title: "Continuous Deployment at IMVU: Doing the impossible fifty times a day."
tags: []

status: publish
type: post
published: true
meta: 
  _edit_last: "6738078"
---
I recently wrote a post on <a href="http://timothyfitz.wordpress.com/2009/02/08/continuous-deployment/" target="_blank">Continuous Deployment</a>: deploying code changes to production as rapidly as possible. The response on news.ycombinator was, well...

"Maybe this is just viable for a single developer ... your site will be down. A lot." - <a href="http://news.ycombinator.com/item?id=472049" target="_blank">akronim</a>

"It seems like the author either has no customers or very understanding customers ... I somehow doubt the author really believes what he's writing there." - <a href="http://news.ycombinator.com/item?id=472133" target="_blank">moe</a>

...not exactly what I was expecting. Quite the contrast to the reactions of my coworkers who read the post and thought "yeah? what's the big deal?" Surprising how quickly you can forget the problems of yesterday, even if you invested most of yourself into solving them.

Continuous Deployment isn't just an abstract theory. At IMVU it's a core part of our culture to ship. It's also not a new technique here, we've been practicing continuous deployment for <a href="http://startuplessonslearned.blogspot.com/2008/09/lean-startup.html" target="_blank">years</a>; far longer than I've been a member of this startup.

It's important to note that system I'm about to explain evolved organically in response to new demands on the system and in response to post-mortems of failures. Nobody gets here overnight, but every step along the way has made us better developers.

The high level of our process is dead simple: Continuously integrate (commit early and often). On commit automatically run all tests. If the tests pass deploy to the cluster. If the deploy succeeds, repeat.

Our tests suite takes nine minutes to run (distributed across 30-40 machines). Our code pushes take another six minutes. Since these two steps are pipelined that means at peak we're pushing a new revision of the code to the website every nine minutes. That's 6 deploys an hour. Even at that pace we're often batching multiple commits into a single test/push cycle. On average we deploy new code fifty times a day.

So what magic happens in our test suite that allows us to skip having a manual Quality Assurance step in our deploy process? The magic is in the scope, scale and thoroughness. It's a thousand test files and counting. 4.4 machine hours of automated tests to be exact. Over an hour of these tests are instances of Internet Explorer automatically clicking through use cases and asserting on behaviour, thanks to Selenium. The rest of the time is spent running unit tests that poke at classes and functions and running functional tests that make web requests and assert on results.

<span class="captioned_image"><img class="size-full wp-image-34" title="Waterfall" src="http://timothyfitz.files.wordpress.com/2009/02/waterfall.png" alt="Buildbot running our tests sharded across 36 machines." width="640" height="278" />Buildbot running our tests sharded across 36 machines.</span>

Great test coverage is not enough. Continuous Deployment requires much more than that. Continuous Deployment means running all your tests, all the time. That means tests must be reliable. We've made a science out of debugging and fixing intermittently failing tests. When I say reliable, I don't mean "they can fail once in a thousand test runs." I mean "they must not fail more often than once in a million test runs." We have around 15k test cases, and they're run around 70 times a day. That's a million test cases a day. Even with a literally one in a million chance of an intermittent failure per test case we would still expect to see an intermittent test failure every day. It may be hard to imagine writing rock solid one-in-a-million-or-better tests that drive Internet Explorer to click ajax frontend buttons executing backend apache, php, memcache, mysql, java and solr. I am writing this blog post to tell you that not only is it possible, it's just one part of my day job.

Back to the deploy process, nine minutes have elapsed and a commit has been greenlit for the website. The programmer runs the imvu_push script. The code is rsync'd out to the hundreds of machines in our cluster. Load average, cpu usage, php errors and dies and more are sampled by the push script, as a basis line. A symlink is switched on a small subset of the machines throwing the code live to its first few customers. A minute later the push script again samples data across the cluster and if there has been a statistically significant regression then the revision is automatically rolled back. If not, then it gets pushed to 100% of the cluster and monitored in the same way for another five minutes. The code is now live and fully pushed. This whole process is simple enough that it's implemented by a handfull of shell scripts.

The point is that Continuous Deployment is real. It works and it scales up to large clusters, large development teams and extremely agile environments.

And if you're still wondering if we are a company that "has no customers", I'd like to refer you to our million dollar a month revenue <a href="http://www.flickr.com/photos/treborinato/2871009707/in/set-72157607385306405/" target="_blank">mohawks</a>.
