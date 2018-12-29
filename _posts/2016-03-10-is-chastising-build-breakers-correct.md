---
published: false
layout: post
section-type: post
comments: true
date: '2016-03-10 06:30:23 +0530'
title: Is Chastising Build Breakers Correct?
---
_** Update: Recently, I delivered a talk at Discuss Agile Conference Bangalore 2016 and XP Conference 2016 about the same subject.  Here are [the slides](http://bit.ly/ci-failures) **_

<iframe width="560" height="315" src="https://www.youtube.com/embed/3pdGQYIXGz8" frameborder="0" allowfullscreen></iframe>

  
  
Continuous Integration is a powerful way to identify and eliminate certain risks, particularly when multiple teams are rallying towards a planned release.  Even if you are not working on a planned release, Continuous Integration will help you to cut-out a release sooner than you would if you did not have CI.

When organizations or teams start adopting Continuous Integration for the first time, they develop an untold habit to chastise the _build breaker_, whenever a build breaks. Most of the time, the reprimanded _build breaker_ is a person and not a thing, a machine or a process :)

Even at organizations which gamify the work environment, a red-card, negative points or bad-karma is added to the person’s score board when he or she breaks builds.  Some organizations take it to the extreme by making the number of build failures to affect the appraisal of a developer.

This blog post is dedicated to convincing you that this is not the right way to do Continuous Integration, just in case you were wondering where this is leading.

## Can a developer prevent broken builds?

Let us start by questioning ourselves how much control does a developer have on whether his commit would break the build or not. 

I prefer to visualize the code branches as roads in a city.  Any developer who is working towards a commit is like a driver driving his car in the direction of a road merge - a point where his road merges with another bigger road.  

![Screen Shot 2016-05-07 at 7.44.17 AM.png]({{site.baseurl}}/images/Screen Shot 2016-05-07 at 7.44.17 AM.png)


Unlike real world, the driver cannot signal to potential vehicles on the other road using lights, sound or anything.  He has no other option than to directly drive into the road-merge just hoping that he will not get hit by another vehicle on the other road.  See? The developer has very little control on whether the build will break in the CI system or not. 

However, in the code universe, the driver does not die or get injured when another vehicle crashes into his.  He can just repair his car and proceed ahead fully alive and able!

## What if build breakage hurts the developer's career?

If the build breakage cannot be tolerated, then the driver could stop the car before the merge, get down, look for oncoming vehicles and then drive to the merge if none found.  Hey, but what if a lightning-speed Ferrari comes on the road just at the moment when the driver went back to car after reassuring himself that there were no vehicles approaching from the other road?  In the world of shared codebase, particularly in enterprises, such lightning-speed Ferraris are more common.  So, if build breakage is frowned upon, the developer slows down and even after that he cannot be sure not to break the build - blame the Ferraris!  Imagine what could happen to the motivation levels of that developer if the trend continues!

## Hey, What if the car could not run properly even before merge?

I made a convenient assumption that the car is in a runnable state before the road merges!  This assumption might turn out to be wrong sometimes or even many-a-times.  The car(code) might not be in a runnable state or have some defects (Gas out! Brakes are God’s will! Can run only at the speed of a Tonga!) before road merges. Hence, the car stops the moment it is put into the merged road, which has harsher conditions.  This would block the other vehicles coming into the merged road, causing ruckus!  

In this case, it may be argued that it is the wrong judgment of the developer which caused the ruckus here.  However, if the system or process does not enforce a pre-commit verification of P0 failures, the developer cannot be blamed.  After all, the whole idea of CI is to make sure that the mistakes of an individual developer should not turn out to be costly to the organization.  

Many a times, it turns out to be that the developer’s road does not have the same conditions (read as infrastructure) as the broader merged road and hence, a developer could never be sure if his car would run in merged road.

## Types of CI Failures

Shortly put, CI failures can be of two categories:

1. Unavoidable
2. Avoidable

In case of unavoidable failures, don’t blame the developer.  After all the very advantage of CI in your organization just demonstrated itself by this build failure.

In case of avoidable failures too, don’t blame the developer. Avoid the failures using technology or process and more importantly allow this avoidance-methodology to evolve over time.  

## How do I motivate collective code ownership then?

If you want to motivate your developers to collectively own the code, instead reward the developers who ‘fix’ a broken build, particularly when they fix it without adding tech-debt.  This subtle change from ‘_punish the breaker_’ to ‘_reward the fixer_’ will make sure that your CI pipeline is almost 'always up' and churning out quality software.

This shift will not only add to your employee satisfaction but also make you help kick-ass software in short time, without wasting time on discussions about “Whose fault is it?”.  In short, this will give your teams a slight shift in orientation away from “blame game” culture towards “ownership” culture.  What do you think about this? Let me know! I am all ears (and eyes too)!
