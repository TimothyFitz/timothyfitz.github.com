--- 
layout: post
title: "Continuous Deployment: Speed, Fear and Safety."

type: post
published: false
---

There are a lot of confused ideas floating around about Continuous Deployment. By far the most common is that Continous Deployment is all about going _fast_. Unfortunately this misconception prevents adoption by exactly the type of people who could benefit the most, people who are afraid of their current deploy process and even more afraid of going faster or deploying more often!

Almost everyone I meet is afraid of delpoying code. Like seriously deeply afraid. The thinking goes that deployment is many mundane deploys punctuated by moments of extreme terror. Unfortunately this leads to the classic deployment downward spiral: deploys are risky so let's do less. Less deploys means each deploy has more changes bundle together, which makes deploys riskier. So let's do less! 

In truth, Continuous Deployment is about addressing this fear head on. The only way to break out of this downward spiral is to consciously acknowledge it and attempt to address the underlying factors. The explicit goal of Continuous Deployment is to make deployment feel _safe_. If you're afraid of deploys, you're not doing Continuous Deployment _by definition_.

Feeling safe really only requires two things. Your process has to ensure that changes are safe to deploy before they go out, and when inevitebly you deploy a change that makes it through and still breaks things you need a culture of shared responsibility.

How do you make sure changes are safe to go out? Well first you stop making stupidly fky changes. Bundling up every single commit for a month straight and trying to release it in a big bang is silly. The odds of failure are stacked against you. Deploying more often counterintuitively leads to significantly decreased risk of failure on deploys. Most small changes are cheap to apply, cheap to test and cheap to roll back. If you only ever ship small changes (even if it's lots and lots of them), your overall failure rate will go down, and the customer impact of failures will also go down. 

But that's not enough. If changes that do break production are treated as personal failures, you're back in the downward spiral. In Continuous Deployment it is always the deploy pipeline that is responsible for ensuring that deploys are safe. If there's ever a failure in production blame the process first. This has to be as shameless and blameless as possible. For example, after a production issue most companies will do a post-mortem. Commonly in these post-mortems you'll see a timeline of events containing specific employee's names and mistakes. Instead, these post-mortems should refer to the employee's roles, and maybe at the end have a list of people participating in the meeting. Anyone doing your job could've make the mistake you made, and the only way your deployment process can get better is if you think of mistakes and bad commits as _the rule_ and not the exception.

If you make these two changes institutionally and make sure to reinforce them regularly, you'll end up in the sweet spot: developers feel _safe_ when they're deploying. Safety isn't a quarterly goal or a bullet point for buzzword compliance. **Safety is a fundamental prerequisite for a healthy business.** 

Luckily for us, once the process is safe and developers actually feel safe suddenly everything changes. Think about how differently you might develop features if there was no part of your codebase you were afraid to touch. That is what Continuous Deployment gives you. Speed not through shipping crap faster, but sustainable long term speed through developing software the right way the first time.

