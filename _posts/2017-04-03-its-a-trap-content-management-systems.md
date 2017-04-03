---
layout: blog
comments: true
title:  "It's a trap! Content Management Systems"
date:   2017-04-03
categories: development, cms
---

# It's a trap! Content Management Systems

Content Management Systems (CMS), as they are generally conceived, are a trap. This will apply to "roll your own" systems and to boxed solutions like [WordPress](https://wordpress.com/)/[Drupal](https://www.drupal.org/) or [Refinery](http://www.refinerycms.com/). The problem isn't with the software (though technical problems will arise). The problem is with the user's expectations and the failure control them.

## The CMS Trap: Dissected

### Infinite Scope

The problem is that CMS, by (lack of) definition, implies infinite scope. They are frequently expected to provide:

- WYSIWYG interfaces
- Access to the application's database content
- The ability to interact with the application's API
- Support and incorporation of all manner of static content from text, to images, to custom style sheets
- Support and incorporation of dynamic elements like forms
- Marketing features like SEO optimization and AB Testing
- Auditing tools like authorization, change logging, and approval queues
- Ease of use tools like previewing and draft saving
- Audience targeting tooling for showing different content to different user's based on their profile or context
- And much more...

For any of these features you can think of several boxed CMS solutions that provide them, but it's unlikely that any boxed system will contain every feature you need (at least not once the "Version 2" round or change requests make it down the pipeline. This means that if you use a boxed solution you'll end up heavily customizing it (and battling its no longer valid assumptions), or you'll end up rolling your own - which is just as bad of an idea as it sounds.  

CMS's are exceptionally susceptible to the "can't you just..." threat vector. The answer is generally, "yes." Most features are reasonable requests with a possible execution plan, but the lack of neatly defined scope means these requests will quickly spiral until small changes take unreasonable amounts of time. I've worked on CMS solutions at both ends of this evolutionary spectrum. It's one of the slipperiest of all scope creep slopes. Double black diamond.

<img src="https://images-na.ssl-images-amazon.com/images/G/01/OutdoorRecStore/2015/subcat_hero/skiing-down-1691x536-2015-04._CB309299060_.jpg" alt="Picture of a steep skiing hill and cautious skier." title="Double Black Diamond Skiing Hill" class="img img-responsive"/>

### Circumvention of Quality Control

CMSs get content in production at the click of a button. They bypass code review, automated test suites, and any other checks wisely put on a developer's production access. While auditing can put some brakes on this crazy train the auditor tends to have the same blind spots as the person who wrote the content. They'll know to check that the link works but they might not think that link is the result of a dynamically generated route that's subject to change. They'll know to test that a CMS driven form submits the data they expect but not whether the data remains useable if it comes from a different encoding or has encountered strings it needs to escape.

The development team is immersed in these issues every day. They're cultured to notice these things and yet sometimes they still miss them. They often rely on IDEs and automated linters and test suites to help them with these risks. Getting these tools to work on CMS content is not always possible and keeping the CMS friendly and useable when these tools encounter problems is its own unique challenge.

### YAGNI – You Aren't Going to Need It

The idea of a CMS is so alluring to the people that imagine using it that it has become the "exercise bike" of software projects.  Everyone would like one and thinks they'd use it if they had it. Few that have them really use them, and those that use them often find the problem they got them to solve is harder than it seemed and requires more discipline, management, and work than initially factored in.

There are plenty of valid real world use cases for a CMS (or at least the idea of one). But _all projects_ will appear to benefit from them – leading people considering them to identify false positives. This perceived applicability couples with a perceived cost saving benefit. The cost of developing a web product, when you're at the point of considering a CMS, is often better understood than the cost of the CMS. On its face it seems that a tool that lets an intern make updates to a webpage or application will save money versus having a full development team take on that change. However, CMSs fall victim to their own version of the "99 Percent Rule."

> "The first 90 percent of the code accounts for the first 90 percent of the development time. The remaining 10 percent of the code accounts for the other 90 percent of the development time." - [Jon Bentley](https://www.amazon.com/Programming-Pearls-2nd-Jon-Bentley/dp/0201657880)

> "A CMS will manage 90 percent of the content it's meant to. The remaining 10 percent will require 90 percent of the development effort it would have taken to do 100 percent of the work _without_ a CMS. (This doesn't include the amount of work it took to make or adopt the CMS.)"

The cost savings of a CMS often evaporate when this rule is factored in.

#### You Already Have a CMS

If you like pithy/profound tech phases, here's another for you:

> "Any sufficiently advanced CMS is indistinguishable from software deployment."

What does this mean? In a sense your development tools, web stack, deployment pipeline, issue queue, version control system, and development team are a CMS. HTML is a CMS. HTML managed by Git is a more full featured CMS. HTML driven by Rails and Postgres and styled by SASS all under Git and Github version control is an even more robust CMS. Any CMS you adopt or create will never match the CMS provided by your existing stack.

Will replacing your "stack CMS" with WordPress or a home rolled solution be able to maintain or surpass the results you've gotten with your stack CMS? Is the content you are considering bringing under WordPress or a home rolled CMS changing so often that it requires a special CMS just to keep up? Even in the "Continuous Integration Deploy on Demand"[1] context that you operate in? (If you don't operate in that context - start there before you consider a CMS.)

## The Bear Who Sees the Trap...

> "There is a Russian proverb: The bear who sees the trap cannot be caught." - Josef Yurinov, Mercenaries: Playground of Destruction [2]

Are you dissuaded from using a CMS? Would it surprise you if I told you that wasn't my goal?

There are plenty of real world contexts where a CMS is the only option. I rejected that truth for awhile, but a designer friend who once worked for the digital arm of a newspaper convinced me otherwise. And even if I _was_ right and CMSs are always the wrong solution...

> [Construction Supervisor] You're going to have to accept it. This bypass has got to be built and it's going to be built. Nothing you can say ...
> [Arthur Dent] Why's it got to be built?
> [Construction Supervisor] What do you man -- why's it got to be built? It's a bypass! You've got to build bypasses. – Douglas Adams, Hitchikers Guide to the Galaxy

You'll end up adopting or building a CMS at some point, so you might was well get ready to make the best of it.

### Springing the Trap

The secret to escaping the CMS Trap is control how you spring it - like letting the bar of a mouse trap down slowly so it doesn't snap your finger.

#### Know your limits

The most important piece is to define the scope. Not just at the project and feature level, but at the philosophical level. Your organization needs to understand what their CMS is, and **what it's limits are**. All software has limits, and each limit suggests alternative software, but you have to make a choice and **accept a set of limitations**. What is your CMS? What does your CMS do? What doesn't your CMS do? The more clarity you can pack into the answers, the better your software will be.

> "If you know the enemy and know yourself, you need not fear the result of a hundred battles. If you know yourself but not the enemy, for every victory gained you will also suffer a defeat. If you know neither the enemy nor yourself, you will succumb in every battle." – Sun Tzu, Art of War

---

1. "Continuous Integration is a software development practice where members of a team integrate their work frequently, usually each person integrates at least daily - leading to multiple integrations per day. Each integration is verified by an automated build (including test) to detect integration errors as quickly as possible. Many teams find that this approach leads to significantly reduced integration problems and allows a team to develop cohesive software more rapidly. This article is a quick overview of Continuous Integration summarizing the technique and its current usage." - [Martin Fowler](https://martinfowler.com/articles/continuousIntegration.html)
2. Yuuuup. Quoting a video game.
