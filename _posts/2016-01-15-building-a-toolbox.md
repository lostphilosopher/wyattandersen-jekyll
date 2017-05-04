---
layout: blog
comments: true
title:  "Building a toolbox"
date:   2016-01-15
categories: development
blurb: "One of the most valuable personal development projects I took up in 2015 is being deliberate about assembling a set of tools to solve problems I'm faced with regularly building out sites and applications for early stage startups." 
---
# Building a toolbox

One of the most valuable personal development projects I took up in 2015 is being deliberate about assembling a set of tools to solve problems I'm faced with regularly building out sites and applications for early stage startups. I've looked at every task I've taken on as a chance to solve that problem in the general case. This has been valuable on two fronts:

*First:* It puts me in the right mind set to solve the problem I'm working on in a thorough, well documented, and reproducible way.

*Second:* It has given me satisfaction in my work even if the actual project at hand isn't particularly interesting to me.

I'll dig a bit deeper into each of those.

## Mind Set

If I need to do something, my instinct is to just do it - in the first way I find that makes sense and works. My focus is on solving the problem, overcoming the obstacle, and moving on to the next one. Sometimes this is what it takes to get something done given external constraints. Most of the time though, there's no harm in spending some extra time and energy to think about the meta level of the problem, and find the best possible solution. Then to take some time really digging into it, documenting it, and thinking about how you could reproduce it elsewhere if you had to solve the problem again. A simple example from the development perspective is rebasing a feature commit so that you can refer back to that PR when you need to do the same thing again later [1].

## Satisfaction

This has been the biggest gain of this approach for me. If you're in the business of building software for someone else you've almost certainly found yourself doing something you don't think is a good idea. In the start up space you might also find yourself building something that won't keep the business afloat, and might realistically never see the light of day. Sure you want to avoid these situations in the first place, but we all know it's gonna happen sometimes.

Thinking of that work as building or honing a tool set means that even if it never gets used, or wasn't a great idea, I can still be happy that I've found a good way to do it, or gotten better at doing it. Next time it might well be exactly the right thing to do.

## Here's the toolbox I've got going so far:

**Website Building:** [Jekyll](https://jekyllrb.com/) and [GitHub pages](https://help.github.com/articles/using-jekyll-with-pages/). This combo gives me a framework for building out a website, free hosting, blogging out of the box, and solid performance with static pages. Using a JavaScript and various APIs I've been able to add some basic application functionality and dynamic content to round out the final product.

**Web Application Building:** [Ruby on Rails](http://rubyonrails.org/), [PostgreSQL](http://www.postgresql.org/), and [Heroku](https://www.heroku.com/). Rails is pretty handy on its own, but paired with gems like [Devise](https://github.com/plataformatec/devise) and [Active Admin](https://github.com/activeadmin/activeadmin) it can get you from 0 to featured application in record time. PostgreSQL can do basically whatever you need it to, including using it as a document database. Heroku plays nicely with rails, has tons of documentation, and is a breeze to deploy.    

**Frontend AB Testing:** [Optimizely](https://www.optimizely.com/) has a decent GUI for non-technical users, can get a rudimentary test going quickly, and deploys with ease. It also has a rich feature set for more complicated use cases.

**Payment Processing:** [Braintree](https://www.braintreepayments.com/) is the approved payment vendor for my company, so this wasn't really a choice, but it does everything I need it to, and their customer support is fantastic.

**Realtime Chat with Customers:** I've been using [Intercom](https://www.intercom.io/). It's easy to install, has a good non-technical GUI, and offers a variety of plans to fit the particular projects needs.

The point here isn't to encourage you to adopt these tools. This is just a few examples of things I've picked and why. The point is that I've been reaping benefits by spending a little extra time researching what options are out there for solving the problem in front of me, and then reusing that tool every time I see the same problem.  

## Conclusion

This approach has improved my day to day. Maybe it would be helpful for you? The first step is to be deliberate about phasing the problem you're trying to solve in a general way, and then to tackle it as if you'lBuilding a toolbox

**PS:** Got a tool set already? Starting one? Add it to the comments! Might be a good place for someone else to start.  

---
1. Yeah, I know this is a best practice in general, but this was the first time I really saw a tangible benefit from it.
