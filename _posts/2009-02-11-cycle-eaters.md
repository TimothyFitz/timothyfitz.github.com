--- 
layout: post
title: In the Lair of the Cycle-Eaters
tags: []

status: publish
type: post
published: true
meta: 
  _edit_last: "6738078"
---
<h3>Programmers are losing serious amounts of productivity to hidden work every day.</h3>
It's time to stop that, but wait, I'm getting ahead of myself.

In a different day and age, x86 assembler genius Michael Abrash coined the phrase<a href="http://www.gamedev.net/reference/articles/article1698.asp"> Cycle Eater</a> to describe how x86 assembly would have non-obvious slow downs. For instance an addition that should've executed in 2 cycles actually ran for an extra 6 cycles spent fetching the operands from memory. You'd assume you had optimal assembly when you'd be missing that your assembly was actually kinda slow. Had you known about your cycle eater, you could've re-ordered prior operations to optimize for memory fetching, regaining the optimal 2-cycle performance.

The phrase Cycle Eater perfectly describes much higher level problems that plagues software development. Cycle Eaters are everywhere. Cycle Eaters can be as simple as requiring an engineer to manually switch marketing promotions on and off. They can also be as complex as the time, knowledge and effort it takes to set up a new local sandbox or build environment.
<h3>The fundamental problem with Cycle Eaters is that you don't realize how often they're wasting your time.</h3>
Ever joined a new company only to spend a week getting your build environment up and get a build that actually runs? That cost has to be paid for every engineer, for every machine and for every reformat, for every reinstall. Not only does that cost add up, but the drive to avoid setting up a build environment causes cascading cycle eaters. Countless times I've seen engineers sitting there waiting while tests run or a build compiles while their laptop goes unused for development. They're avoiding the pain and headache caused by the build setup Cycle Eater.

Luckily Cycle Eaters are surprisingly easy to deal with. When I started contributing features to <a href="http://db.tigsource.com">TIGdb</a>, the commit and deploy process was entirely manual. It was easy to screw up and annoying manual work. My first deploy was by hand. I then resolved to never do that again. I automated away some of the work. My second deploy was by running a couple commands, and then a shell script to do the final deploy. Again I automated away some of the work. My third deploy was SSHing into the server and running a shell script. My fourth deploy was running a local shell script. My fifth deploy automated database migrations.

My example incrementally removed the Cycle Eater, and that's critically important. I'm not advocating that you go out and try to start a mammoth project to automate away everything that's slowing you down. That would be a severe violation of the you-aren't-going-to-need-it principle. Process automation is an interesting thing, because once you automate away a Cycle Eater, you may find your behavior dramatically changing. If it's free to deploy, you'll deploy more often. If it's free to set up sandboxes, everyone in marketing gets one!
<h3>Here's where something magical happens.</h3>
When you fix a Cycle Eater, you don't just get back the time you were losing to the Cycle Eater. There are often unpredictable emergent properties from this type of waste reduction. When you have free sandboxes, marketing starts using the same development tools that engineering uses. Marketing suddenly doesn't need to pull an engineer out of flow to get promotional material deployed.

Client software build and release processes are often extremely manual, often involving "that one guy who builds the installer." Once fully automated, releases can be cut daily with minimal cost. Daily releases result in dramatically better feedback, such as specifically which revisions caused regressions or improvements. That knowledge feeds back into the process, causing progressively higher quality client releases.

All this from simple incremental automation.

This isn't just my theory. It's an IMVU culture of removing Cycle Eaters. It's allowed an extremely aggressive policy for new hires: on the day that they start working, they will commit a fix to the website. It'll probably be a typo, but it will be a real fix pushed into production and live for every customer. On their first day. All thanks to slaying Cycle Eaters.

So start today. The next time you notice that your time is being eaten up by one of those little things you wouldn't normally fix, think about it. Just think about the solution to the problem, and then implement a step in that direction. It doesn't have to be a big step and you don't have to know how to completely fix the Cycle Eater. Just make a single incremental improvement.

That first step will be the hardest. You'll have to force yourself to overcome your natural tendency to ignore the Cycle Eater, but the results... I can't just tell you what it's like to push a button and have a full deploy just happen. It's a rush. There is something fundamentally pleasing about automating away wasteful work; you must experience it for yourself.
<h3>Go, and slay your Cycle Eaters.</h3>
