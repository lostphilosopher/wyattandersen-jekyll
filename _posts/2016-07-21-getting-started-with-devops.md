---
layout: blog
comments: true
title:  "Getting Started with DevOps"
date:   2016-07-21
categories: development, devops
---
# Getting Started with DevOps

## Backstory

I had a couple conversations at [DevOps Days Minneapolis](http://www.devopsdays.org/) about how get started with DevOps. I've collected my thoughts here.

> From wikipedia: "DevOps (a clipped compound of development and operations) is a culture, movement or practice that emphasizes the collaboration and communication of both software developers and other information-technology (IT) professionals while automating the process of software delivery and infrastructure changes. It aims at establishing a culture and environment where building, testing, and releasing software can happen rapidly, frequently, and more reliably." [1]

DevOps, like any other buzzword, represents a powerful tool and a dangerous trap. Sometimes simultaneously. Getting started down the right path, especially at a large organization can be daunting task. DevOps requires buy in, people skills, technical skills, and a commitment to improvement, iteration, communication, inclusivity, and learning.

There are many right ways to take the first step. In what follows I offer how I've done it, as a framework for how I believe you can do it.

## Baby Steps to the Elevator

<img src="http://4.bp.blogspot.com/-adrx_R5Iy5s/UstJWAVVozI/AAAAAAAAAlo/GLeHNllVwvQ/s1600/baby-steps.jpg" class="img img-responsive" alt=" Scene from What About Bob? where Dr. Marvin poses with his book, Baby Steps to the Elevator" title="Baby Steps to the Elevator"/>

### Identify

Perhaps the worst way to implement DevOps is as "a solution in search of a problem." Before you start reading up on [DevOps](https://smile.amazon.com/Effective-DevOps-Building-Collaboration-Affinity/dp/1491926309), [CI](https://smile.amazon.com/Continuous-Integration-Improving-Software-Reducing/dp/0321336380), [CD](https://smile.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912), [monitoring](https://smile.amazon.com/Effective-Monitoring-Alerting-Web-Operations/dp/1449333524), [chatops](https://stackstorm.com/2015/12/10/chatops_pitfalls_and_tips/), [hugops](https://twitter.com/search?q=%23hugops), and [@beerops](https://twitter.com/beerops), ask yourself what you believe DevOps will be able to do for you, and why you need that. This can be "shorter release cycles," "less down time," "fewer production defects," "reduced infrastructure costs," "visibility into X," "shared ownership of X" etc. You might also want to factor in what problems will be most compelling to whoever you need buy in from as you try to grow a DevOps culture in your organization.

### Quantify

Your next task is define a metric that can prove to yourself and others that your problem has been solved, or improved. This is also a litmus test for whether or not you've identified a problem. If you can't find a metric for it you probably need to drill into it deeper. Once you've got your metric, determine your baseline, where are you at with it right now? Remember (document) how you made this calculation since you'll have to come back to it later.

### Document

Dig into your problem space, understand what goes into in now, step by step. Become an expert on the way thing are. What does your process look like today? What gets done? Who does it? How do they do it? The better you know this, the better you'll be able to improve it. Build a spreadsheet, and get this documented. Don't skimp on this step it's one of the most important.

### Correlate

Now comes the fun part. Look at the document you built in the previous step, and notate where a DevOps tools / approaches / philosophies / methodologies / mentalities / etc. could make a difference. Build (document) a mind  map, or a spreadsheet, or whatever helps you identify ways to impact your problem space. Look for improvements, but don't forget to look for redundancies, waste, and anything that can be eliminated.

### Choose

Pick one piece of the document you've created above that you see as low cost high benefit, a confidence booster, or an easy win. Look for something that you're excited to work on. Make sure it's something that you believe will impact that metric you defined already.

**Examples:**  

- Standardize releases by keeping ops scripts on GitHub.
- Automate testing by having devs use [git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) to run tests pre-push.
- Automate deployments by implementing [Travis](https://travis-ci.com/) or [Jenkins](https://jenkins.io/).
- Identify performance improvement opportunities by implementing [Skylight](https://www.skylight.io/) or [New Relic](https://newrelic.com/).
- Improve the code base by finding errors with [Papertrail](https://papertrailapp.com/) or [Nagios](https://www.nagios.com/).
- Build collaboration by starting a weekly Dev/Ops [brown bag](https://smile.amazon.com/Creating-Brown-Bag-Lunch-Program-ebook/dp/B01ACLXSKK) or social lunch.  
- Build better features by utilizing more perspectives by getting serious about diversity and inclusion.

### Attack

Now that you've got a starting point, try out a solution. Look at this as an experiment, you don't have to keep your solution in place if it doesn't work, and you can try another solution later. #YOLO

### Track

Moment of truth. Did it work? Has your metric improved? Are there other changes? Can others see the improvement? What went right, what went wrong (this is great time for a (retrospective)[https://smile.amazon.com/Project-Retrospectives-Handbook-Team-Reviews/dp/0932633447], (after action report)[http://www.acq.osd.mil/dpap/ccap/cc/jcchb/Files/Topical/After_Action_Report/resources/tc25-20.pdf] or postmortem).

### Iterate

If you didn't improve your metric that's still a win, you've collected data, you've found a way not to make a light bulb. Figure out where you went wrong, and try again! If your metric is improving, keep tracking it, and circle back to "Choose" it's time to take another step, rinse repeat, DevOps[2].

### Summary

1. Identify the problem you are trying to solve.
2. Formulate a metric that allows you to measure whether, and to what extent you have solved that problem.
3. Create document that identifies each step in the process(es) relevant to the problem you're trying to solve.
4. From your document identify what DevOps tools/approaches/philosophies might be able to improve (or eliminate!) each step in the process.
5. Pick a "low hanging fruit" problem and solution pair.
6. Use your DevOps tool / technique on the problem / solution pair.
7. Track your metric, have things improved? Do others think it has improved? Can you prove that it has improved? If it hasn't why not? What went wrong?
8. Depending on how 7. went for you: either repeat from 5., or restart from wherever things went wrong. Repeat.

---

1. https://en.wikipedia.org/wiki/DevOps
2. That's it? DevOps? No! **DevOps is not a binary**, it's a gradient, your goal is to find the shade that fits your organization - maximizing benefits and minimizing costs. This guide is meant only to help you through your first few steps.
