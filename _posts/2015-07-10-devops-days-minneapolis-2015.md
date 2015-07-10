---
layout: blog
comments: true
title:  "DevOps Days Minneapolis 2015"
date:   2015-07-10
categories: devops, conferences
---

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">&quot;Only area of tech industry that needs more str8 white dudes is fixing the [str8 white dudes] in the industry&quot; - <a href="https://twitter.com/jonlives">@jonlives</a> <a href="https://twitter.com/hashtag/DevOpsDays?src=hash">#DevOpsDays</a></p>&mdash; Rainbow DashOps (@mattstratton) <a href="https://twitter.com/mattstratton/status/619167395605803008">July 9, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

^ I wouldn't write a blog post if I didn't want people to read it, think about it, and talk about it. However, statistically speaking, you've got plenty of opportunities to read the thoughts of a straight white man on any aspect of tech so here's some people who: 1. Were speakers or organizers of this event. 2. Write about tech, and might even write about this event. 3. Aren't straight white men.  

- [http://bridgetkromhout.com/](http://bridgetkromhout.com/)  
- [http://beero.ps/](http://beero.ps/)  
- [http://www.coolleen.com/serendipity/](http://www.coolleen.com/serendipity/)
- [http://www.leanessays.com/](http://www.leanessays.com/)

(But still come back and read this! :-) )

#DevOps Days Minneapolis 2015#

In my second year at CaringBridge our DevOps single point of failure moved to a new opportunity. Our vagrant machines started to fall behind our production environment and the progress we made towards continuous delivery was stopped in its tracks. Needless to say, we weren't doing DevOps. (ProTip: If your company's DevOps effort has a single point of failure, you're probably not doing it either.)

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">“We’re all in charge of <a href="https://twitter.com/hashtag/devops?src=hash">#devops</a> .. It’s everyone’s responsibility” - <a href="https://twitter.com/beerops">@beerops</a> <a href="https://twitter.com/hashtag/DevOpsDays?src=hash">#DevOpsDays</a></p>&mdash; .json (@jasonhand) <a href="https://twitter.com/jasonhand/status/618786822018084864">July 8, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Around this time we got a new Sys Admin with interest in Chef, and he and I teamed up to figure out: 1. What DevOps is. 2. How to make it work. I can't say our efforts were a resounding success, but meaningful progress was made (reliable Vagrant machines, Chef managed prod servers), and I certainly learned a lot. Ever since, I've been participating in meet ups and conferences, and still trying to answer those questions.

Here's what I've got after [DevOps Days Minneapolis 2015](http://www.devopsdays.org/events/2015-minneapolis/).

#What is DevOps?#

It seems impossible to talk about DevOps without waxing IT on what it is. It's similar to Agile in that way. It's also similar to Agile in that it is more verb than noun. You cannot purchase DevOps, or even hire DevOps, but you can use tools and hire (or train) people that are more... "DevOps-y" than others.

Here's something that I've heard a lot, but didn't really sink in until this conference (and particularly [Katherine Daniels, aka @beerops](http://beero.ps/) talk - FYI: she has a [book coming](http://shop.oreilly.com/product/0636920039846.do)): **DevOps is about empathy.** Empathy for your colleagues in other teams (deveopment, ops, project management, QA, customer care, etc.) and empathy for your users. As a developer I'm often tempted to code like I'm a physicist living in a frictionless world of perfect spheres.  

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">DevOps meme from <a href="https://twitter.com/beerops">@beerops</a> talk. :-) <a href="https://twitter.com/hashtag/devopsdays?src=hash">#devopsdays</a> (We&#39;re all in charge of DevOps!) <a href="http://t.co/RJ1gEX5P5T">pic.twitter.com/RJ1gEX5P5T</a></p>&mdash; Wyatt Andersen (@wandersen02) <a href="https://twitter.com/wandersen02/status/618787057855369220">July 8, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

A DevOps frame of mind inspires empathy for the Ops Team or Sys Admins who have to deal with the consequences of my faulty assumptions - sometimes in the middle of the night with people yelling at them. DevOps thinking also reminds me that the only experience that really matters is the end user experience. If what I make doesn't work on their machine - it doesn't work.

But empathy isn't a boolean I can flip on in `wyatt.config`. It takes effort and practice to develop. One way to foster empathy is collaboration with other teams ("pair ops-ing" - [@beerops](https://twitter.com/beerops)). Talk to your Ops team, talk to your QA team. Work with your Ops team, work with your QA team. Figure out what their headaches are, and understand their pain points. Talk to your users, and if at all possible - watch them use your product. That flashy animation might be killing their page load time, or they might be wondering why you need their real name to recommend cat videos to them. Always remember - **you are not your users**.

"Designers are not typical users" - [The Design of Everyday Things](http://www.amazon.com/Design-Everyday-Things-Donald-Norman/dp/0262525674)

##How do you make DevOps work?##

Now let's assume you are one with your colleagues, one with your users, and one with your product.  

![Think the scene from the Matrix where Neo can "see" the code that governs the world around him.](http://i.stack.imgur.com/zymAc.gif "He is the One. - Morpheus")  

Now what?

You need more than a DevOps state of mind to make DevOps work, there are still technical windmills to slay.

[Mary Poppendieck](http://www.poppendieck.com/people.htm), author of [Lean Software Development: An Agile Tool Kit](http://www.amazon.com/exec/obidos/ASIN/0321150783/poppendieckco-20), and one of my favorite tech voices shared some wisdom on how to actually make the DevOps sausage.

The one that hit me the most - **Feature Flags**.

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">Continuous Delivery: Deployments (technical) happen all the time. User facing changes are toggled with a switch (release). <a href="https://twitter.com/hashtag/devopsdays?src=hash">#devopsdays</a></p>&mdash; Wyatt Andersen (@wandersen02) <a href="https://twitter.com/wandersen02/status/619155466849890304">July 9, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

Feature flags allow you to push "work in progress" code out to your production environment without exposing your users to an incomplete (and possibly buggy) experience. They're a crucial part of Continuous Delivery because they allow you to actually deploy what you're working on continuously instead of in large staccato  chucks. I'd say more, but we'd all be better off reading [Martin Fowler's thoughts on the subject](http://martinfowler.com/bliki/FeatureToggle.html) instead.

Another gem from Mary's talk was her encapsulation of Microservice Architecture.

<blockquote class="twitter-tweet" lang="en"><p lang="en" dir="ltr">Microservice: A small &quot;do one thing well&quot; independently deployable service with its own database. Managed by its own team. <a href="https://twitter.com/hashtag/devopsdays?src=hash">#devopsdays</a></p>&mdash; Wyatt Andersen (@wandersen02) <a href="https://twitter.com/wandersen02/status/619152151101599745">July 9, 2015</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

My approach to microservices is best captured [here](http://martinfowler.com/bliki/MonolithFirst.html), and I'm by no means a fanboy, but their potential in the DevOps space is hard to ignore. Microservices open up a world of flexibility in terms of "right tool for the job," "dog fooding," and probably dozens more tech-buzz-isims.

##DevOps | Empathy | Culture | Diversity | Inclusion - Presented without segue...##

Technology is bringing about some [cool, meaningful things](http://gizmodo.com/a-therapeutic-robot-teddy-bear-will-play-with-kids-in-t-1708757467). And a lot of just [cool things](https://www.kickstarter.com/projects/1384275386/bartesian-the-first-capsule-cocktail-machine/description). But the tech industry has a very serious dark side. Namely - women's talents and contributions are often ignored, and when notice is taken it's often in the form of violent harassment. Racial minorities and people with diverse sexual orientations experience similar discrimination, and career obstacles. Ageism is also a big problem. The class and economic issues that intersect with tech and inequality exceed my ability to string together words at this time.

I said a little about all this at the top, and there's a lot of good writing about it already. What I will say now is this:

I love what I do, and I take my profession seriously. But I'm not always proud of my industry. The spirt of inclusion, and culture of empathy that I witnessed at DevOps Days Minneapolis 2015 (and at several recent Twin Cities tech events) have made me proud, if not of the whole tech industry - of the part of it that I move in.

**Conference Sponsors:**  
- [SaltStack](http://saltstack.com/)  
- [VictorOps](https://www.victorops.com/)  
- [Pivotal](http://pivotal.io/)  
- [SumoLogic](https://www.sumologic.com/)  
- [PuppetLabs](https://www.puppetlabs.com/)  
- [HP](http://www.hpsoftware.com/)  
- [Docker](https://www.docker.com/)  
- [Elastic](https://elastic.co/)  
- [PagerDuty](https://www.pagerduty.com/)
- [SPS Commerce](http://www.spscommerce.com/)  
- [Target](http://www.target.com/)  
- [sysdig](https://sysdig.com/)  
- [JUT](http://www.jut.io/)  
- [New Relic](https://newrelic.com/)  
- [Chef](https://www.chef.io/)  
- [Dell](http://www.enstratius.com/)
- [10th Magnitude](http://www.10thmagnitude.com/)
- [Gov Delivery](http://www.govdelivery.com/)
- [Ansible](http://www.ansible.com/)  
- [Scout](https://scoutapp.com/)  
- [BuzzFeed](http://www.buzzfeed.com/)  

^ Thanks for making this event possible!
