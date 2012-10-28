--- 
layout: post
title: Cloud Elasticity
tags: []

status: publish
type: post
published: true
meta: 
  _edit_last: "6738078"
---
<strong>Abstract</strong>

It's time to take advantage of the cloud's free parallelism. Most existing use cases merely map existing techniques to the cloud. Elasticity is a critical mesaurement: the time it takes to start a node up, and your minimum time commitment per node. Short lived but massively parallel tasks that were once impossible thrive in a highly elastic world. Big prediction: Clouds are going to get more elastic indefinitely; they'll trend with Moore's law.

<strong>Cloud Elasticity</strong>

It's time to take advantage of the cloud's free parallelism. Lot's of infrastructure has moved off to the cloud, but it's being done so naively. The storie seem to fall into three categories: "I'm serving my wordpress on an ec2 instance.", "we used a few machines to OCR a bunch of pdfs." and "When it came time to add capacity, we just clicked a button." These use cases are all things you would do if you bought hardware, but are easier because of cloud computing.

Let's try a scenario where we're going to push public clouds to their breaking point. We want to run our test suite, which takes four hours, as fast as possible. How fast is that today? For this example, let's assume EC2 nodes always take exactly one minute to start (a fair estimate of reality). Let's also assume test setup is another minute, flat. We can spawn four nodes and have all of the tests done in one hour and two minutes. We can spawn forty nodes and have the tests done in eight (4 * 60 / 40 + 2) minutes. We can spawn four hundred nodes and have the tests done in 2:36. That's not just fast, that's fast enough to change the rules around when you run tests. That's fast enough to change the nature of software development.

Sadly this scenario isn't realistic today, because there are two important measures of cloud elasticity: spin-up elasticity and spin-down elasticity. Spin-up elasticity is the time between requesting compute power and recieving it. Spin-down elasticity is the time between no longer requiring compute power and no longer paying for it. In the case of EC2 these numbers aren't balanced, it's a minute to spin up and up to an hour to spin down. EC2's true elasticity is an hour!

Which is a shame, because what really interests me are the services pushing the edges of elasticity. Services that can <em>only</em> exist in a world where computing power blinks in and out of existence. Services that offer to spread your <a href="http://saucelabs.com/">workload</a> as widely as technologically possible. Services that take your long running tasks and give you results immediately, at minimal extra cost.

So here's my big prediction:

Thanks to computing power's exponential growth, cloud computing's elasticity will exponential decay; we'll see a 1/2 reduction in spin-up and spin-down time every year and a half.

For a while this elasticity will go towards making offline tasks faster. Tasks like compressing large amounts of video will at most take about as long as the elasticity times. Cool stuff, but not very novel uses. It's when the elasticity starts to approach the "off line" vs "on line" threshold that things get crazy. What if it's only a second to spin a machine up or down? We can start to have machine per web request, or machine per social interaction (IM, tweet or hug).

What happens when we have 5 second elasticity? (About as long as a user will wait for a UI interaction to complete without multitasking)

What happens when we have 15 millisecond elasticity? (About as fast as your eyes can refresh)

I don't pretend to know what the next big revolution in computing is going to be; but I'll sure as hell be watching the services pushing cloud elasticity to it's edges. If there is a revolution to be had in cloud computing, that's where it'll start.
