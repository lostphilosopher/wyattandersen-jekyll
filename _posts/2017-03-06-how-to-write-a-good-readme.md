---
layout: blog
comments: true
title: "How to Write a Good README"
date: 2017-03-06
categories: open source
---

# How to Write a Good README

## Ode to documentation...

The humble README page cannot be code golfed, it cannot be represented by a UML diagram, and it cannot be unit tested. Yet it is the unsung hero of your codebase, and a corner stone of collaborative software development.

We often forget about our READMEs. Once a developer is immersed in a code base so many of its quirks seem trivial; its invocations routine. Yet for the uninitiated getting started with an unfamiliar code base can be a daunting challenge. Your README file can be your first chance to make a first impression, and bring a new developer up to speed on your codebase quickly and autonomously.

Once you've got a decent README in place you'll be surprised how often it comes in handy. You might even be grateful for it yourself if you get pulled off to another project and have to circle back months later. Your README can be the quick refresher you need to get back in the game.

## Components of a good README

The nomenclature may not be consistent, but there is a general consensus around the things your README should include. Here's what [GitHub](https://help.github.com/articles/about-readmes/) suggests a README should include:

> What the project does.
> Why the project is useful.
> How users can get started with the project.
> Where users can get help with your project.
> Who maintains and contributes to the project.

Here's the advice from [18F](https://pages.18f.gov/open-source-guide/making-readmes-readable/):

> A description of what the project is for.
> Instructions for how to develop, use, and test the code.
> Instructions for how people can help.
> List the licensing information for your project.
> List the contact information for your team as well as where to ask questions.

And here's what the [Rails framework](https://github.com/rails/rails/blob/master/railties/lib/rails/generators/rails/app/templates/README.md) offers in its template README files:

> Ruby version.
> Ruby version.
> System dependencies.
> Configuration.
> Database creation.
> Database initialization.
> How to run the test suite.
> Services (job queues, cache servers, search engines, etc.).
> Deployment instructions.

There's certainly other guides out there, but I think you get the general trends.

A README should contain:

* A description of the project
* Where to find the project (URLs)
* How to use the project
* How to get started with the project
* How to contribute to the project
* How to run the project's tests
* How to deploy the project
* Legal and licensing considerations
* Where to go for help with the project

Let's dig into each of these.

### About: A description of the project

This is your elevator pitch. Your chance to briefly discuss *what the project does* and *why the project does that*. This should be written with an entry level user in mind, but don't be a afraid to use the keywords you want them to associate with your project. Just make sure if you use buzzword language you explain it, and link to more information.

### Usage: How to use the project

In this section you should still be in sales pitch mode. Your elevator pitch has got the user in the door. Now it's time to show off what you are offering. This section doesn't need to be an exhaustive index of every possible user course of action (but it should link to such a list!). Instead it's the core functionality. Focus on the things most users came here looking for, and the key differentiators that set your project apart from other similar purposed tools. You can start each item with some abstract technical documentation, but then dig in and give a real world example. Preferably, something they can run themselves once they've followed your "How to get started" section.

### Getting Started: How to get started with the project

This is crucial. This is where you will lose potential new users, this is where the new employee considers a 'shoulder tap', this is the section you will be kicking yourself later if you don't write.

You probably can't over document this section. While it's a reasonable assumption that a Rails developer will know to start a local instance with `rails c` it doesn't cost you anything to remind them. Take it step by step, does your project have prerequisites? Minimum versions for something? Is there a script they should run that will do most of the setup automatically? Are there external set up steps like obtaining API keys or accounts? Do they need to run some sort of seeder? For some applications this is section is pretty trivial, but for others it can be a lifesaver.

The best thing to do once you've written this section is try it out yourself. Follow your own directions to the letter and wee how it goes. Then have a friend or coworker go through it. If either of you get confused or stuck - you've probably identified a "gotcha." These are one the most important things to note in README. If a user gets stuck and finds in your README a description of their problem and a link to the Stack Overflow article they were about to spend half a day looking for they will think you a prophet.

A final note on this: It's fine to send your user to other documentation for how to complete specific steps (installing a database, library, or VM for example). But bear in mind that your instructions are only as good as their weakest link. If your user gets stuck installing a dependency of your project they are more likely to hold it against your project than the dependency - as unfair as that may be.

### Contributing: How to Contribute to the Project

This section is crucial for Open Source projects, but is helpful for corporate projects as well. When writing this section think of user who thinks they've just identified a bug or area of improvement in your project, and is trying to figure out how to proceed. They'll want to know where to report this issue, and maybe how to offer their own solution. In either case they'll want to know how a fix for their solution gets into production (be that a library version or hosting environment).

#### Reporting an Issue

If your user or employee has an idea for making your project better the first thing you'll want them to do is document it. If there is specific debugging information you'll want them to include; make sure you ask for it explicitly (versions, operating systems, browsers, etc.). Even if they aren't going to fix the issue or add the feature, a well explained "steps to reproduce" or feature use case will make a big difference to someone who does work on it.

#### Running the tests

If someone is reading this section, they're considering working on the issue they've identified. You want them to have a good first impression of being a "contributor" to your project. This starts with the tests. Hopefully all this takes is a one liner, but if there are "gotchas" or prerequisites they should be aware of make sure your cover them here.

#### Coding Standards

A potential contributor is going to be annoyed if their hard work is rejected because they didn't do something that they didn't know they needed to do. Code formatting, linters, testing expectations. Git message / PR / branch formatting conventions, etc. are all things you should point out here if you have them. Many of these things can be automated, and should be.

#### Deployment

This section is extra important in a corporate setting, but applies to open source development as well. If part of your project's lifecycle is deployment to a library host or live domain you'll want to include instructions for how to do this. Both practical instructions like what buttons to push or commands to run, and bureaucratic notes like who needs to be notified and how issues get closed. This is also a good place to set some expectations around how long it will take for a contribution to reach a "published" state. If you have monthly releases, or limited time its worth noting that here so a contributor knows when they can expect to see their changes in the wild. This is particularly helpful if your contributor is trying to decide whether to proceed with a fork, or wait for changes to hit your project.

### Legal and Licensing

Include a license with your project. #JustDoIt. [1]

If there are any other legal considerations or formal guidelines this is a good place to lay them out. This is also where you should link to your Code of Conduct if you have one.

### Contact Us: Where to go for help with the project

Despite your stellar README people may still have questions. People will still have questions. Tell them where to send them. Got a Slack or IRC channel? Email address? Twitter handle? This is the place to draw attention to those. You could also triage a bit in terms of where to go with what type of questions. "How to Contribute" questions might go to a different channel than "Do you have this feature?" questions.

### Template

If you like this approach for writing READMEs here's [a template (in markdown format) as a Gist](https://gist.github.com/lostphilosopher/0ba5a45a32d8f1defa88ccd6c45a92f4) for writing them in this fashion.

---
1. Full disclosure: I'm bad at remembering to do this too...
