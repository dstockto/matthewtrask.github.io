---
layout: post
title:  "How To Survive your Team Lead leaving."
date:   2017-06-06
comments: yes
description: At least once, if not more, you will run into a time where the leader of your team leaves and you have to pick up the pieces. 
tags: Programming, Teams, Workplace, Hit By The Bus
---

 At least once, if not more, you will run into a time where the leader of your team leaves and you have to pick up the pieces. 

## Did you get hit by a bus?

A common expression with programming, and specialized teams within an office, is the famous/infamous "Hit by the Bus" document. Now, its not meant to sound morbid. Nor is it supposed to bear ill will towards someone, it is supposed to be how a team can pick up the pieces when the unexpected happens. The name comes from the fact that no one plans on getting hit by a bus, so it is a document for the unexpected. And it can help you weather multiple scenarios: Team Lead taking a new position and being asked to leave immediately, Team Lead needing to take extended leave of absence that may or may not leave them without internet for extended periods of times, or quite literally the lead is hit by a bus. Lets take a look at what should be on this document so you can survive the first few days. 

#### Passwords

Probably the first and most important item to deal with is passwords. Nothing is worse then watching a production server on fire and no way to access it. As a team, you should know how to access the production and staging environments. AWS has IAM roles, with various leves of permissions. A good tip here would be to create a bus user that can be accessed in extreme emergencies alone. Same thing for accounts such as CI services, services like Docker Hub if you use Docker, Github/Gitlab services, Slack, and whatever else your team uses. The possibilities here are endless. But your team should have a way to access them all. 

If you do everything with SSH or GPG keys, talk at length about how they are used, where, and how to regenerate and change them. 

#### Storage and Architecture

Speaking of services like AWS, if you have a moment, jot down a few thoughts about your infrastructure set up. Not all teams are able to have a full blown ops team, and this its up to the team lead to roll something that works. Specifically talk about how the infra scales, what all occurs during deployments... do you create new servers each time or is code just replaced? Talk about what services are used and why. A lot of developers are curious creatures by nature, but not all are privy to every decision made by the lead developers. If you use Heroku or something similar, make sure a few developers know what is going on and how to deploy with Heroku.

Talk briefly about the deployment process. How it is done, common pitfalls you hit when you do it, and how to navigate those issues should they arise. Im thinking specifically migrations here. 

Talk about future plans too. Give the remaining developers a bit of a road map to follow. Are you replacing legacy code in a certain way? Why did you create a class not commonly found in projects that may need to be explored by other developers? This is an area that will slip fast in quality. Its of the utmost importance to give developers a vision. In the wake of a lead leaving, itll be awkward, itll be hard, but the last thing you want it to be is visionless. 

#### Ways of contact

As a lead is leaving, voluntary or not, leave a way for the developers left to get in touch with you. You will begin to forget specific details, but you will retain a good idea of most things for some time, and its crucial that you are reachable for at least a week. Whether you choose to let management know about it is up to you but do you want to leave your team and burn the bridge? Not really. No matter how big the city, word can travel fast. So be ready to help occasionally. Obviously you wont be paid for this, but it does you some goodwill to help out initially. That first deployment post team lead will be rocky. 

#### Where to put this

The tricky part is where to store this. Obviously, you want to limit it to essential people only. You dont want to CEO, who may or may not be technical, to get it cause who knows what can happen then. A great place is in your teams password software. Another place, should you not use a password manager would be your repo. Hide this in the wiki, cause lets face it, wikis are never used anymore. You want it in a place that a developer can get to it quick, yet still not show it to the public. Definitely not sticky notes. 

## Thoughts

Its never fun to lose a team lead. This person may be a mentor to the junior and mid level developers on the team. They may have had a clear vision for the future. But with any kind of "hit by the bus" documentation, it helps the remaining developers pick up the pieces faster. Not only does it reduce confusion but it creates an idea of comfort too, which we all need sometimes. 

Till next time.
