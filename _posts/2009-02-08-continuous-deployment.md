--- 
layout: post
title: Continuous Deployment
tags: []

status: publish
type: post
published: true
meta: 
  _edit_last: "6738078"
---
Alex has just written a refactoring of some website backend code. Since it was a small task, it's committed and Alex moves on to the next feature.

When the code is deployed in production two weeks later it causes the entire site to go down. A one-character typo which was missed by automated tests caused a failure cascade reminiscent of the bad-old-days at twitter. It takes eight hours of downtime to isolate the problem, produce a one character fix, deploy it and bring production back up.

Alex curses luck, blames human infallibility, inevitable cost of software engineering and moves on to the next task.

This story is the day-to-day of most startups I know. It sucks. Alex has a problem and she doesn't even know it. Her development practices are unsustainable. "Stupid mistakes" like the one she made happen more frequently as the product grows more complex and as the team gets larger. Alex needs to switch to a scalable solution.

Before I get to the solution, let me tell you about some common non-solutions. While these are solutions to real problems, they aren't the solution to Alex's problem.

1. More manual testing.
This obviously doesn't scale with complexity. This also literally can't catch every problem, because your test sandboxes or test clusters will never be exactly like the production system.

2. More up-front planning
Up-front planning is like spices in a cooking recipe. I can't tell you how much is too little and I can't tell you how much is too much. But I will tell you not to have too little or too much, because those definitely ruin the food or product. The natural tendency of over planning is to concentrate on non-real issues. Now you'll be making more stupid mistakes, but they'll be for requirements that won't ever matter.

3. More automated testing.
Automated testing is great. More automated testing is even better. No amount of automated testing ensures that a feature given to real humans will survive, because no automated tests are as brutal, random, malicious, ignorant or aggressive as the sum of all your users will be.

4. Code reviews and pairing
Great practices. They'll increase code quality, prevent defects and educate your developers. While they can go a long way to mitigating defects, ultimately they're limited by the fact that while two humans are better than one, they're still both human. These techniques only catch the failures your organization as a whole already was capable of discovering.

5. Ship more infrequently
While this may decrease downtime (things break and you roll back), the cost on development time from work and rework will be large, and mistakes will continue to slip through. The natural tendency will be to ship even more infrequently, until you aren't shipping at all. Then you're forced to do a total rewrite. Which will also be doomed.

So what should Alex do? Continuously deploy. Every commit should be instantly deployed to production. Let's walk through her story again, assuming she had such an ideal implementation of Continuous Deployment.
Alex commits. Minutes later warnings go off that the cluster is no longer healthy. The failure is easily correlated to Alex's change and her change is reverted. Alex spends minimal time debugging, finding the now obvious typo with ease. Her changes still caused a failure cascade, but the downtime was minimal.

This is a software release process implementation of the classic Fail Fast pattern. The closer a failure is to the point where it was introduced, the more data you have to correct for that failure. In code Fail Fast means raising an exception on invalid input, instead of waiting for it to break somewhere later. In a software release process Fail Fast means releasing undeployed code as fast as possible, instead of waiting for a weekly release to break.

Continuous Deployment is simple: just ship your code to customers as often as possible. Maybe today that's weekly instead of monthly, but over time you'll approach the ideal and you'll see the incremental benefits along the way.
