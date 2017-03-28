---
layout: blog
comments: true
title:  "Microservices: Means or Ends"
date:   2017-03-10
categories: microservices, development
---

# Microservices: Means or Ends

The following comes from a talk I gave at [MicroMN](https://www.meetup.com/MicroMN/) sponsored by [Field Nation](https://www.fieldnation.com/).

<img src="https://i.stack.imgur.com/Ev5Ux.jpg" class="img img-responsive" alt="Scene from the movie The Matrix where Neo tries to bend a spoon with his mind." title="The Matrix Bent Spoon"/>

> "Try only to realize the truth. There is no spoon. Then you'll see that it is not the spoon that bends, it is only yourself."
\- The Matrix

"Try only to realize the truth. There are no microservices. Then you’ll see that it is not the application that is Service Oriented, but only your development practices."

Put less abstractly, in the words of Martin Fowler:

> “The term "Microservice Architecture" has sprung up over the last few years to describe a particular way of designing software applications as suites of independently deployable services. While there is no precise definition of this architectural style, there are certain common characteristics around organization around business capability, automated deployment, intelligence in the endpoints, and decentralized control of languages and data.”
\- [Martin Fowler](https://martinfowler.com/articles/microservices.html)

Microservices, like design patterns, don’t exist because someone in a research group invented them, published a paper, and blew the software development communities’ collective mind. And microservices, unlike the tag line for every sponsored microservices link on Google cannot be bought off the shelf. They exist because software developers encountered a set of problems repeatedly, and with the aid of training, experience, intuition and all those other terms we use to describe “trial and error” to our employers - arrived at a set of practices that countered these problems. People observing and participating in this trend started using various phrases for it around 2011, but by 2012 this suite of problem solving practices was generally referred to as microservice architecture.

There are two important parts of this bit of history. The first is simply that a microservice is not a monolithic concept. Rather it is composed of micro-concepts. Each independently providing costs and benefits, and occasioning another set of costs and benefits at each union of the contained subsets.

The second is that microservices as pattern and concept came about descriptively, not prescriptively. “Monolith,” the term often associated with whatever the opposite of whatever a microservice is, has become a dirty word in some circles. As if monolith somehow implies “spaghetti code,” “deep coupling”, “junior developers,” and “the decline of political efficacy and moral integrity in modern society surely brought on by autotuned music and asymmetrical haircuts.” When in fact “monolithic architecture” is merely a term to describe a different set of characteristics. Refactoring your giant bowl of spaghetti coded monolith into micro-bowls of spaghetti code is not only unlikely to solve any of the problems encountered in your original application, but now you don’t even know which bowls have the meatballs in them.

I claim, that if your response to technical and business challenges brought on by your current application and its relation to your business model is to “go to microservices” without first:

1. Doing a blameless post mortem of your application and your development practices.
2. Identifying and evaluating solutions to each actual problem you’ve identified.
3. Taking a step back, looking at your solution set, and asking yourself what sort of architectural techniques would bring those solutions about.

You have put your solution cart before your problem horse.

It is entirely possible that an earnest assessment of your codebase will lead you to development practices that are characteristic of microservices, but you have to leave open the possibility that your journey will lead you elsewhere.

Here’s what I mean by that. We’re all familiar with the success Amazon and Netflix have had with microservices. The componentization of their architecture has allowed them to pinpoint weaknesses, and to create whole new products by combining existing services. Or even opening a single service up to the outside world. That’s cool. That’s damn cool. When I think about working in that environment I see a Star Trek utopian future where features and unit tests practically write themselves. But then the angel on my shoulder, who looks surprising like
_Jurassic Park_’s Dr. Ian Malcolm, for reasons I’m still processing with my therapist, chimes in:

<img src="https://cdn.meme.am/cache/instances/folder590/500x/62533590.jpg" class="img img-responsive" alt="Scene from the movie Jurassic Park where Dr. Malcolm questions the choice to resurrect dinosaurs." title="Jurassic Park could doesn't mean should"/>

> “Yeah, yeah, but your scientists were so preoccupied with whether or not they could that they didn't stop to think if they should.”

YAGNI - Ya Ain’t Gonna Need It, is more than a dopey acronym; apparently all it takes to succeed in American politics. It’s the voice of wasted hours of work and never used features calling out from the great garbage collected beyond warning future developers that we’re here to generate value for employers by creating value for our users. That’s it. If independently deployable single purpose services are the best next step to get there - by all means take it. He who hesitates is Blockbuster. But if it isn’t, don’t let the hype seduce you away from what you fired up that terminal to do in the first place.

Researching for this talk I read a great example of what a web based calculator built with microservices would look like. You’d have a service that renders a GUI, and does nothing more than render output received in an expected format, and pass along input also in an expected format.  You’d have a service that routes the user input to any number of services that operate on it, one for addition, one for subtraction, one for multiplication, or maybe not, maybe you reuse the one you already have for addition. Clean, simple, beautiful, easily expanded, the unit tests would practically write themselves.

<img src="http://www.cumulogic.com/wp-content/uploads/2014/09/microvsmono.png" class="img img-responsive" alt="Simple microservice diagram." title="Simple Microservice Diagram"/>

But the ugly truth is that very few of us are writing systems with that level of logical clarity and clear lines of demarcation characteristic of a calculator. These lines of demarcation are related to what Michael Feathers, in Working Effectively With Legacy Code, calls “seams.”

> “A seam is a place where you can alter behavior in your program without editing in that place.”
\- Michael Feathers, in _Working Effectively With Legacy Code_

A seam represents joined behavior between two otherwise unrelated systems. They are why you get tripped up unit testing your sign up flow after you add the “Welcome” email your marketing team asks for. Feathers devotes a whole chapter to them and how to handle them properly. It takes work, and adding microservices to the mix doesn’t solve the problem on its own. In fact it’s probably easier to identify seams in a monolith than across microservices.

The calculator example reminds me of physics classes in college where the textbook gives you E = MC^2 and shows you how to solve for E, and the test gives you E = MC^2 and asks you to prove the existence of Rick Rolling.

<img src="http://www.jbdavisinnovates.com/wp-content/uploads/2013/10/sand_copy.jpg" class="img img-responsive" alt="A line drawn in flat wet sand." title="Line in the Sand"/>

Much of our discussion of microservice architecture sweeps possibly the hardest part of microservice architecture under the rug. Where do you draw the line between services when the business itself is complex, and ever changing. In a world where making sure developers don’t commit API secret keys to public repos remains a real problem how do we ensure that those same developers write consistent interfaces for their services, and don’t introduce cascading dependencies, or redundant services, or redundant services? In even the simplest of e-commerce sites the lines between users, carts, receipts, and orders are often harder to draw than we’d like. What happens when those lines are inherently blurred?

I’ll tell you what happens, I work for Optum. We’re part of UnitedHealth Group, number 6 on the Fortune 500, and the largest health insurer on the planet. We use a lot of microservices. My specific team in the process of moving to Event Driven Architecture powered by Kafka. This is because so much of healthcare is necessarily interconnected. The number of steps on your FitBit is relevant to you, possibly to your employer, to your health insurer, to your broker, to your doctor, maybe even your social network. One piece of data often needs to go may places and be used in many ways. Furthermore, access to that data needs to be controlled, the data needs to be aggregated, anonymized, de-anonymized, cached, published, and archived. Microservices all the way down. Terabytes of data every day. A significant part of what I do in all of this, and what my team, department, and several other departments do is try to connect data with people. In an ideal world there would be some sort of “customer microservice,” behind some sort of “authentication microservice,” that talks to an “authorization microservice.” In this rosey world of milk and honey I’d be able to use some sort of unique identifier to connect a developer with all the information on an individual that they are authorized to access.

<img src="http://static1.squarespace.com/static/55ad5011e4b026cf2525000a/55ef3698e4b0f68e0e7069ec/55ef36a6e4b0f68e0e706b17/1389724912000/network-diagram-v2.jpg?format=original" class="img img-responsive" alt="Messy microservice diagram" title="Messy Microservice Diagram"/>

In the real world of nuclear winter and cannibalistic sewer dwelling mole people - those three microservices do exist, as do dozens more with the same names and the same stated purpose. Each accessing a subset of the data and returning a subset of that data in a format one particular developer thought was a good idea at the time and often named with a series of arcane acronyms whose meaning is a closely guarded secret protected by a cult of DBA-warrior-monks rumored to be living in the mountains of Peru. Or a data center in Hopkins.

The point is that even though we have a good use case for microservices, and chose to use them, doesn’t mean that we always use them well. [1] And by not using them well we miss out on many of the benefits we started using microservices for in the first place.

Alright. I’ve vented I feel better. Let’s get proactive.

Let’s look back at to how I told you “going to microservices,” if it is to come about, should come about:

1. Doing a blameless post mortem of your application and your development practices.
2. Identifying and evaluating solutions to each actual problem you’ve identified.
3. Taking a step back, looking at your solution set, and asking yourself what sort of a beast thou hath wrought, and by what technical invocations you can bring this beast into being.

Here’s some good news. Many of development practices that you’ll identify in step two, are prerequisites for microservice architecture, and are value-positive in and off themselves. I have a similar theory on Open Source Software Development. Many of the development practices it takes to open source a code base, in any productive sense, are just general best practices - good things to do:

- Document your code.
- Test your code.
- Agree on standards and nomenclature (contributor guidelines).
- Open lines of communication.
- Practice code reviews.
- Use version control.
- Standardize environments.
- Provide reliable reproducible development environments.

If you start doing any or all of those things your application will improve. Once you’re doing enough of them “going to Open Source” will be a simple matter of flipping a switch on GitHub and publicising your change.

“Going to microservice architecture” is somewhat like this. Things that you’ll need to do include:

- Draw lines around business components (hard, but worth it)
- Separate those “components” into module, controller, class, and/or file structures that enforce and provide them.
- DRY your code base, weed out redundancy, elevate abstractions.
- Identify challenges and bottlenecks. (Setting yourself up to chose the right tool for the job.)
- Test your code.
- Document and or standardize your interfaces.
- Cross train development teams, de-silo.
- Build competency in infrastructure as code and automated deployments.

If you start doing any or all of those things your application will improve. Once you’re doing enough of them “going to microservices” will be a matter of taking one of your internal modules and externalizing it into an independently deployable component service. Rinse and repeat. Furthermore, if you try to start writing microservices without doing these things first - you’re going to have a bad time.

And again, many of these development practices are value-positive in of themselves. The easier you think making the transition to a microservice architecture would be, the more ready you are to actually do it, and the more unnecessary you might find it to be.

And here’s why it’s important to find out if microservices are unnecessary in your situation. Despite their light and airy name they are rarely as minimalist as they appear. We’re all familiar with the idea of technical debt: this being the notion that when you cut corners in software development you are accumulating an amount of “todo” work that will one day come due. What we don’t talk about enough is our “technical credit limit” which is deeply connected to technical debt, but rather than representing work that needs doing it represents the scope of the possible work that you may need to do. If you write your whole application in PHP you will never have to deal with the consequences of Ruby’s metaprogramming nuclear option. If you write some services in PHP and some in Ruby - now you might.

With each technology you add to your stack you are increasing your technical credit limit. Just like your real credit limit - this has both pros and cons. On the pro side, a high technical credit limit might be the only way to seize that great deal or market opportunity that has presented itself. On the con side, a high technical credit limit can leave you underwater with more languages, databases, frameworks, patterns, and their associated unique quirks than you have development cycles to handle. In a fierce market where members of your dev team can and will leave at any moment you need to be prepared for the woman who holds all the institutional knowledge on your container orchestration, React front end, or authentication microservice to leave - and take a sizeable chunk of that vital knowledge with her. This is the technical credit limit equivalent of looking at the receipt for that awesome jet ski you just bought and remembering you don’t have a trailer, don’t live near water, and have nowhere to put it in your two bedroom apartment.

In the words of Obama, let me be clear, I’m not trying to Rails against microservices. All of their pros are very real. My goal has been to highlight some cons that are sometimes overlooked, and remind you that there’s more than one way to sort a two dimensional array of N cats. Make sure that the problem you are solving isn’t “we don’t use microservices.” And make sure that you aren’t transferring the problems that microservices are said to solve to your application and business model.

Solve the problem in front of you. Do the next best thing for you business. Take it incrementally, you can work towards a microservice architecture and reap benefits at every step. In this sense it’s not about microservices, or “going to microservices,” it’s about a culture that makes incremental improvements and has the courage to follow them. To microservices, to monoliths, and anywhere in between.

Try only to realize the truth. There is no spoon. There are no microservices. Then you’ll see that it is not the application that is Service Oriented, but only your development practices.

---
1. It's a big company. Large sections of the technical architecture are really well built. The end product that the customer uses is reliable. What suffers are internal services and new projects that struggle to interface with the existing architecture.
