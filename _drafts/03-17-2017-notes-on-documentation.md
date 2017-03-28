---
layout: blog
comments: true
title: "Notes on Documentation"
date: 2017-03-17
categories: documentation
---

# Notes on Documentation

## Motivation

Writing [How to write a good README]() I wanted to cover a few things that didn't quite fit the theme. This post is where those ideas ended up.

### Dry Docs

> DRY: Don't Repeat yourself

We're all familiar with the concept of [DRY code](https://en.wikipedia.org/wiki/Don't_repeat_yourself), but what about DRY Docs?

If you put the same documentation information in multiple places you run several risks:

- Updates and Maintenance: When you make changes that forces your documentation to change you have to update several places. Will one get missed?
- Source of Truth: If two sources of documentation disagree how does a new user know who to trust?
- Knowing Where to Look: Where do I go for pricing information? Where do I go for technical information? Where do I go for usage information? It should be clear to the person looking for this info where they need to look (wiki? README? website?).

There are several possible solutions to these problems. Perhaps the easiest is putting all your documentation in one place. The project README can be that place. But this solution isn't right for all projects.

If you do need to spread documentation about your project across multiple sources. The key is to be clear about what purpose each documentation source serves, and to minimize overlap. Then, when you need to cross reference, link to the other source. And make a reference available to show users which source to check for different sorts of information.

### Automation

The bad news is I have never use a documentation automation tool that really worked. (Unless you count some API documentation generators like [API Blueprint](https://apiblueprint.org/) or [Swagger](http://swagger.io/)).

The next best thing? Process. Build development practices the ensure code changes trigger documentation updates just like they do testing.

### Review

Code reviews are easy to implement, manage, and enforce. They have incredible power to improve your code base and to distribute knowledge.

### Testing
