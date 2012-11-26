--- 
layout: post
title: Getting Started with Continuous Deployment

type: post
published: true
---

One of the most common questions I’m asked about continuous deployment is “Continuous deployment sounds awesome! I have this existing project/&#8203;team/&#8203;corporation. How do we get started?” I absolutely do not recommend halting your company and spending months building out a “perfect” continuous deployment pipeline. There are quite a few ways to incrementally build and use continuous deployment systems, which I’ve bucketed into the four options.

As a quick refresher, let me recap the basic components of a continuous deployment pipeline. If every developer isn’t committing early and often, then head over to wikipedia’s article on continuous integration and start there. Once your entire team is practicing continuous integration, you’re ready to to pick a continuous integration (CI) server. The CI server is the cornerstone of all continuous deployment automation. I recommend Buildbot or Jenkins. 

Your CI server has a few jobs. On every commit your CI server should run all of your automated test coverage. This is your safety net. If your automated test coverage completes successfully, your CI server will then run your automated deployment scripts. Now that your code is being deployed, you’ll want application and system level production monitoring and alerting. If anything goes wrong (user signup breaks, master database CPU spikes, etc) you want to be alerted immediately. Finally, you need a formal root cause analysis process for learning from production failures and investing in future prevention. Of course there are many more advanced practices that can be added to the continuous deployment pipeline, like a cluster immune system, but those all come after you’ve built and learned from the basic pipeline.

In a nutshell: Commit &rarr; Tests &rarr; Deploy &rarr; Monitor

So how do you incrementally build out such a complicated pipeline? Here are the four options I recommend:

## Just ship it.
Automate your deployment. Deploy to production on commit. Worry about tests when your regressions become costly. Use root cause analysis to drive further investment in your pipeline.

* Pro: Quickest path to getting value out of CD
* Pro: Easy to do when project is starting
* Con: Expect heightened regression rate until automated testing/monitoring catches up with deploy rate.
Best for: startups, brand new pre-customer software, software where regressions are relatively cheap. Remember: If you have no users, regressions are free!

## Ship to staging first. 
Automate your deployment. Deploy to staging servers instead of production. Treat staging failures like as if they were production failures. Slowly build up your automated test coverage, and application monitoring/alerting. When comfortable with the regression rate in staging, start continuously deploying to production.
* Pro: Easiest to sell to conservative stakeholders
* Pro: No risk of continuous deployment causing regressions in production.
* Con: Regressions often won’t be caught in staging, giving a false understanding of regression rate. This is a big deal. Your staging servers won’t have real users hitting real edge cases, and they probably won’t have the traffic, data size, scalability issues or reliability measurement of your actual production servers. You will regress in all of these areas without knowing it. This all leads to a false confidence in the abilities of your continuous deployment pipeline.
* Con: The cost of building out the whole continuous deployment pipeline, without the return of the feedback of deploying to production.
Best for: proving methodology to conservative stakeholders, projects with existing staging deployment that is regularly tested, and dipping toes in the continuous deployment waters.

## Ship a low risk area first. 
Automate deployment of a low-risk area. As infrastructure is built out / regression rate drops, roll out automated deploy to other areas.
* Pro: Real learnings, real continuous deployment
* Pro: Minimal risk of costly regressions
* Con: Low-risk areas are often able to have regressions without Q/A or customers noticing, leading to slow feedback cycle
* Con: Requires that you have or build a well isolated area of your codebase.
Best for: proving methodology to less conservative stakeholders, projects with isolated low-risk code areas, and utilizing continuous deployment infrastructure as it’s built.

## Ship your highest-risk area first.
Automate deployment of your highest-risk area (i.e. billing). Build out the full continuous deployment pipeline for your riskiest area, including a large automated test suite. This means significant up front investment, but If continuous deployment works for your company’s highest risk area then you’ve proven it will work everywhere else. While this approach sounds crazy, if your company decides continuous deployment is critical to it’s success then nailing continuous deployment for your highest-risk area makes the rest of adoption a downhill battle instead of an uphill one. 
* Pro: Real learnings, real continuous deployment
* Pro: Once successful, rolling out to the rest of the company should be an easy sell
* Pro: Easiest to measure before/after regression rates accurately
* Con: Must build significant automated testing, alerting, monitoring and deploy/rollback infrastructure up front
* Con: Regressions will be more expensive
Best for: top-down mandate to build and invest in continuous deployment, proving methodology beyond doubt in large organizing, organizations large enough to devote team to implementing continuous deployment, and moving large organization to continuous deployment as fast as possible.

Which of these options is right for you comes down to some combination of risk-adversity and organization size. While the overall cost of building out the full pipeline might be significant, you should be able to choose a method from above and invest in your pipeline while you continue to successfully ship your product. The important part is gaining proportional return as you invest in your infrastructure, allowing you to reap benefits from continuous deployment as soon as possible.

So what are you waiting for? Get started already!
