---
layout: blog
comments: true
title:  "A Software Testing Strategy"
date:   2017-03-27
categories: testing, development
blurb: "Testing is one of areas of software development better suited for paint brushes than test tubes. There is overwhelming consensus on the value of testing. Like exercising or eating healthy - we all know we should do it. What I'm going to do here is bring together some battle proven best practices and ideas around unit testing, and present them in a format consistent with my experience."
---

# A Software Testing Strategy

## The Art of Unit Testing

Testing is one of areas of software development better suited for paint brushes than test tubes. There is overwhelming consensus on the value of testing. Like exercising or eating healthy - we all know we _should_ do it. But, in testing, like exercising and eating healthy, despite good intentions we often don't. And when we do test we're often disillusioned by the difficulty of setting up a testing strategy and writing tests, and soured by the lack of the immediate gratification of tangible results. (Does any of that remind you of January?)

What I'm going to do here is bring together some battle proven best practices and ideas around unit testing, and present them in a format consistent with my experience. The idea is to provide a strategy that you can readily apply to how your team approaches testing and can re-use across projects of various scales and circumstances.

That said, this is merely _a system_ not _The System_. Take what of it you find valuable or reject it wholesale - my only insistence is that having **a strategy, a system, a shared consensus is vastly superior to having none**.

### Why have a unified testing strategy at all?

If each developer, or each project employs their own testing strategy you will miss out on many of the benefits software testing is able to provide (even if each independent strategy is sound).

Here's an example, most testing tools provide either a human readable output, or are written in a human readable DSL (or both). This is by design. Your test suite should be able to communicate to its user a decent idea of what the project does, how it works, and where its risk points are. This is where testing and ["Test Driven Development (TDD)"](https://martinfowler.com/bliki/TestDrivenDevelopment.html) intersects with ["Behavior Driven Development (BDD)"](https://dannorth.net/introducing-bdd/). In Rudy for example, [RSpec](http://rspec.info/) makes both forms of testing possible with a single tool.

If your testing strategy includes a cultural norm of writing one of your test layers (and we'll get to these later) in a BDD format (even if it doesn't strictly tie to a BDD tool set) you'll have a place to point people to to understand the project at a deeper level without parsing through the code itself. Your unit tests are, or can be, technical documentation of your code base.

This can be a great benefit of testing, but it's only possible if the team is deliberate about how they write their tests and what tools they use to write them. Doing 80% of the work provides much less than 80% of the value.

Another example is coverage and confidence. Testing ought to enable [continuous delivery](https://martinfowler.com/bliki/ContinuousDelivery.html) and [continuous integration](https://martinfowler.com/articles/continuousIntegration.html). Your test suite should be an accurate measure of how "production ready" your code base is. While "code coverage"[1] is not a be all end all indicator if you can look at a projects coverage report and know what it means, _without looking at the tests_ it can be a very powerful metric. This is only possible if you know how the tests are written.

One final reason to have a testing strategy is that with one in place you can prevent yourself and your team from making unnecessary decisions and consequently experiencing "decision fatigue."

> "No matter how rational and high-minded you try to be, you can’t make decision after decision without paying a biological price." - [John Tierney](http://www.nytimes.com/2011/08/21/magazine/do-you-suffer-from-decision-fatigue.html)

A software engineer writing code has to make decisions with every line; the more you can say "this is how we do this here" the more they can fall back on that autopilot and save their decision making energy for more useful or challenging tasks. Each developer should not have to reinvent the team's unit testing strategy from whole cloth every time they sit down with new a project. Standards save time. Standards are good.

## The Strategy

### Agile Test Pyramid: The Foundation

The core of the testing strategy I'm advocating is the _Agile Test Pyramid_, an approach coined by Mike Cohn in his book [Succeeding with Agile](https://www.amazon.com/gp/product/0321579364). Sofia Palamarchuk summarizes the philosophy behind it as:

> "When most of our efforts are focused on automation at the UI level, the focus is on finding bugs, whereas with the agile pyramid, the idea is to prevent them." - [Sofia Palamarchuk](http://www.abstracta.us/2015/10/26/best-testing-practices-for-agile-teams-the-automation-pyramid/)

<img src="https://abstracta.us/wp-content/uploads/2015/10/Screen-Shot-2015-11-04-at-9.11.59-PM-compressor-1.png" class="img img-responsive" alt="ofia Palamarchuk's and Abstracta.us diagram of the Agile Test Pyramid." title="The Agile Test Pyramid"/>

The Test Pyramid consists of three layers. The base of the pyramid is the _Unit Test Layer_. It is the most powerful and important layer of the pyramid. If you have no tests or testing strategy - this is where you start. The next layer of the pyramid is the _Service Test Layer_, note that this does not imply Service Oriented Architecture, but rather:

> "In the way I’m using it, a service is something the application does in response to some input or set of inputs." - [Mike Cohn](https://www.mountaingoatsoftware.com/blog/the-forgotten-layer-of-the-test-automation-pyramid)

The final layer of the pyramid is the _UI Test Layer_. While still important, UI tests are the most expensive to produce, the hardest to maintain, and do the least good.

If you catch a bug at the UI Test Layer, it's likely that a lot of work will have to get investigated and **re**-done to fix the bug. If you catch the bug at the Unit Test Layer the bug fix should be much easier (in TDD that should be the code you are in the process of writing - _right now_). This means that while all tests can find failures, unit tests are the fastest way to fix bugs, and as Mike Wacker on Google's blog puts it:


> "A failing test does not directly benefit the user.  While this statement seems shocking at first, it is true. If a product works, it works, whether a test says it works or not. If a product is broken, it is broken, whether a test says it is broken or not. So, if failing tests do not benefit the user, then what does benefit the user? A bug fix directly benefits the user." - [Mike Wacker](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html)

The strategy I'll lay out below is based in the idea of the Test Pyramid so I'll cover it one layer at a time.

### Unit Test Layer: Unit Testing and Dependancies

#### Theory

Much of the finesse and ambiguity of unit testing hinges on the definition of a "unit."

> "Object-oriented design tends to treat a class as the unit, procedural or functional approaches might consider a single function as a unit. But really it's a situational thing - the team decides what makes sense to be a unit for the purposes of their understanding of the system and its testing." - [Martin Fowler](https://martinfowler.com/bliki/UnitTest.html)

Referring to the definition of a "unit" Martin Fowler goes on to say,

> "A more important distinction is whether the unit you're testing should be sociable or solitary." - [Martin Fowler](https://martinfowler.com/bliki/UnitTest.html)

If you're unfamiliar with "solitary unit testing" (and it's opposite, "sociable unit testing") here's how Jay Fields describes it:

> "Solitary Unit Testing is an activity by which methods of a class or functions of a namespace are tested to determine if they are fit for use. The tests used to determine if a class or namespace is functional should isolate the class or namespace under test by stubbing all collaboration with additional classes and namespaces." - [Jay Fields](http://blog.jayfields.com/2014/07/solitary-unit-test.html)

The general consensus is that "solitary" unit testing is better, and if you're doing sociable testing you're either: Doing "unit testing" wrong, or doing another sort of testing. If you're doing another sort of testing it may be valuable, but it can't replace unit tests.

Jay Fields rules for solitary tests are:

> "The Foo class will have an associated FooTests class.

> Never cross boundaries.

> The Class Under Test should be the only concrete class found in a test." - [Jay Fields](http://blog.jayfields.com/2014/07/solitary-unit-test.html)

#### Practice

Here's how I approach unit testing.

Every class (`Foo`) in my codebase has an associated `FooTest` class as part of my test framework ([RSpec for Ruby](http://rspec.info/) and [PHPUnit for PHP](https://phpunit.de/)). Every public method in `Foo` class has a corresponding test in `FooTest` (in Ruby with RSpec for example, `def bar` will have a `describe '.bar'`). From there I break down the possible logic flows and create a "context" (as Rspec calls them) for each scenario. This can be done in TDD by mapping out your method in your test or for a legacy method by diagraming its actual flow ([mini white boards](https://www.amazon.com/Brands-Contempo-Magnetic-Erase-Inches/dp/B00PRYQQES) are great for this). Structuring your tests this way will help remind you to bail early with "[guard clauses](https://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html)." Here's an example of the sort of test outlines you can create:

```
# Before refactoring
def checkout
  if current_user
    if current_user.cart.has_items?
      if params['promo_code'].present?
        Order.place(discounted: true)
      else
        Order.place(discounted: false)
      end
    else
      return redirect_to '/products'
    end
  else
    return redirect_to '/signup'
  end
end

# Test outline:
# User is signed in
#   User has items in their cart
#     User has a promo code in their URL
#     User does not have a promo code in their URL
#   User does not have items in their cart
# User is not signed in

# After refactoring
def checkout
  return redirect_to '/signup' unless current_user

  return redirect_to '/products' unless current_user.has_items?

  Order.place(discounted: params['promo_code'].present?)
end

# Test outline in RSpec
describe 'checkout' do
  context 'with a signed in user' do
    context 'when there are items in the users cart' do
      context 'when there is a promo code in the URL' do
        # Test...
      end
      context 'when there is no promo code in the URL' do
        # Test...
      end
    end
    context 'when there are no items in the users cart' do
      # Test...
    end
  end
  context 'without a signed in user' do
    # Test...
  end
end
```

I also like to make use of constants to avoid tests that compare strings. [2]

Managing dependancies is much larger topic than I'll cover here. The gist of the issue is that some of your code will call methods external to the class under test. **You should not be testing those external methods.** Instead you should use a construct (called a "[test double](http://xunitpatterns.com/Test%20Double.html)") to stand in for them. The sorts of test doubles available for this are defined by Gerard Meszaros in his book _[xUnit Test Patterns](https://www.amazon.com/gp/product/0131495054)_ and are listed below (I'll be using the descriptions from Martin Fowler's blog):

> **Dummy objects** are passed around but never actually used. Usually they are just used to fill parameter lists.

> **Fake objects** actually have working implementations, but usually take some shortcut which makes them not suitable for production (an InMemoryTestDatabase is a good example).

> **Stubs** provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test.

> **Spies** are stubs that also record some information based on how they were called. One form of this might be an email service that records how many messages it was sent.

> **Mocks** are pre-programmed with expectations which form a specification of the calls they are expected to receive. They can throw an exception if they receive a call they don't expect and are checked during verification to ensure they got all the calls they were expecting. - [Martin Fowler](https://martinfowler.com/bliki/TestDouble.html)

The test double you use will depend on the dependency you're trying to resolve. What's important is that you don't test external methods themselves. If you're confused on the terminology, there's a good discussion on [Stack Overflow](http://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub). The important thing is that in a unit test you don't test the external method itself. As long as your solution means you aren't testing the external method itself, you're probably good to go.

For further discussion around structuring unit tests (in Ruby/RSpec) see [betterspecs.org](http://betterspecs.org/).

**A note on TDD:**

["Test Driven Development (TDD)"](https://martinfowler.com/bliki/TestDrivenDevelopment.html) is best summarized with the adage:

> Red -> Green -> Refactor (repeat)

The idea is simple, when you start a new feature, rather than starting by writing `Foo` write `FooTest`. Fill it out with tests for the methods that `Foo` will need to have. All of these tests will be failing ("Red"). Once you've got an idea of what `Foo` should look like and have your failing tests in place - start working on filling out those methods in `Foo`. As you implement your methods you can re-run your tests until they start to pass ("Green"). Throughout you'll find things you missed up front or methods that are hard to test or implement, this is expected and means you need to "Refactor." This cycle continues as your newly refactored code breaks your old tests. It's a powerful approach, but a hard habit to form.

There are plenty of books and blogs about TDD. Here's a starting point - [The Cycles of TDD](http://blog.cleancoder.com/uncle-bob/2014/12/17/TheCyclesOfTDD.html) by _Clean Code_'s Uncle Bob Martin (Robert C. Martin).

**Example:** [fizz_buzz.rb](https://github.com/lostphilosopher/unit_testing_fizz_buzz/blob/master/fizz_buzz.rb) and associated [tests](https://github.com/lostphilosopher/unit_testing_fizz_buzz/blob/master/spec/fizz_buzz_spec.rb).

### Service Layer: APIs and Controllers

#### Theory

Service layer testing is the middle ground between unit tests which test specific methods in isolation and GUI testing which tests the full breadth of the app - simulating a human operator.

If your app is an API then your service layer tests and your UI layer tests will be the same thing.

Service layer tests are permitted to be sociable. You want to test the full back end execution stack (API calls, database hits, etc). The only thing you leave out is the GUI.

Here's what Mike Cohn has to say on service layer testing:

> "All applications are made up of various services. In the way I’m using it, a service is something the application does in response to some input or set of inputs. Our example calculator involves two services: multiply and divide. Service-level testing is about testing the services of an application separately from its user interface. So instead of running a dozen or so multiplication test cases through the calculator’s user interface, we instead perform those tests at the service level. Where many organizations have gone wrong in their test automation efforts over the years has been in ignoring this whole middle layer of service testing. Although automated unit testing is wonderful, it can cover only so much of an application’s testing needs. Without service-level testing to fill the gap between unit and user interface testing, all other testing ends up being performed through the user interface, resulting in tests that are expensive to run, expensive to write, and brittle." - [Mike Cohn](https://www.mountaingoatsoftware.com/blog/the-forgotten-layer-of-the-test-automation-pyramid)

#### Practice

Controller testing can be blurry area between unit testing and service testing. You can write solitary unit tests for your controllers and separately write sociable service layer tests for those same controllers. I don't think there's anything _wrong_ with doing this. It's more pure and technically correct. However, it's a lot of work, and _somewhat_ redundant. So here's how I approach it - **skinny everything**. [3] Your controllers should be _really skinny_ with virtually no logic of their own except routing user input and object output. If you've constructed your controllers this way you can get away with not "unit testing" them since their functionality has been properly tested in the unit tests for the objects they call. You can then spend your time focusing on sociable service layer tests for your controllers.

**This is a pragmatic recommendation not an idealistic one.** We all know you've got limited time and testing is a hard sell already. If you're going to "cut a corner" this approach to service layer testing will limit the damage. If you're _really_ pressed for time skip service layer tests and ui tests entirely and focus on unit tests. They will always get you the most "bang for your buck."

**Example:** [fizz_buzz_app.rb](https://github.com/lostphilosopher/unit_testing_fizz_buzz/blob/master/fizz_buzz_app.rb) and associated [tests](https://github.com/lostphilosopher/unit_testing_fizz_buzz/blob/master/spec/fizz_buzz_app_spec.rb).

### UI Layer: Automate All The Things

[Full disclosure - I've never been a QA Engineer. Writing UI tests has only been a hobby for me.]

#### Theory

The most important part of UI testing is: **automate**. Human beings clicking buttons and typing on keyboards is a painfully slow way to find bugs in an application (the whole point of testing). Furthermore, it can't be done on demand. Step one in testing your UI is pick a tool that will let you script your tests. Most tools use [XPath](https://www.w3.org/TR/xpath/) manipulation to let you target HTML elements and interact with them. Some tools can be run "headless" meaning they don't pull up an actual browser. Others pull up a real browser that you can watch step though the tests and even interact with yourself.

UI tests are a great confidence builder. You can write a test script that clicks its way from your home page to your product list to the cart to your checkout page and even checks an email account for a receipt! Seeing a test like that pass brings a warm glow of confidence in your codebase.

However, these sorts of tests are expensive to maintain. Your UI layer changes often - new language and layouts from marketing, the latest trends from design, a nomenclature refactor from development - all of these can break dozens of UI tests at once. UI tests are also _slow_. They have to spin up some portion of the browser stack and wait for http responses, page loads, and all manner of things that make spinners turn slowly.

Also, while I've said this before, remember that **testing is about fixing bugs**. If you catch the bug with your UI layer tests that will likely result in the longest "time to bug fix" vs any other sort of test.

This is not to discourage you from writing UI tests. They provide the greatest level of confidence and are the only (automated) way to catch bugs that crop up _in the UI layer_. (They are also a good indicator of how you're doing at the other levels of testing. Regularly catching bugs at the UI layer means something is going wrong in the unit or service layers.)

#### Practice

I recommend thinking of UI tests in terms of "flows." If you're just starting out - test your "critical path." The most likely path from user hits your site to user provides you with value, ("converts") be that filling out a form, giving you money, or whatever else.

I've used [Watir](https://watir.com/) to write tests in Ruby, and for the demo below I tried out [capybara](https://github.com/teamcapybara/capybara) which partners nicely with [RSpec](https://github.com/teamcapybara/capybara#using-capybara-with-rspec). Whatever you use you'll need to spend some time understanding how XPaths work, and you may want to make changes to your front end to make elements more easy to find. This will make your UI tests more resilient - finding a page element by unique ID is more reliable than, "the forth row in the third column."

UI tests are often done by a different team than the team that wrote the code in the first place. This can be a frustrating communication interface, but it has the upside of providing a "second opinion." While code reviews provide a second opinion of sorts your fellow devs will likely share some of your blind spots. A QA Engineer will bring a fresh perspective to the application and may catch edge cases you missed.

**Example:** [Fizz Buzz App](https://github.com/lostphilosopher/unit_testing_fizz_buzz) and [capybara UI test](https://github.com/lostphilosopher/unit_testing_fizz_buzz/blob/master/spec/fizz_buzz_ui_spec.rb).

## Conclusion

As I said at the beginning, this is _a strategy_. Another approach might work better for your team and your circumstances, but I believe this is a good starting point for any team.

### Summary

- Use the Agile Test Pyramid.
- Make unit tests your priority.
- Your unit tests should have 1:1 relationships between files and test files, and methods and test methods.
- Unit test your M layer of MVC thoroughly and with solitary tests.
- Keep your classes skinny, especially your controller classes.
- Write sociable service layer tests for your controllers.
- Once your unit and service layer tests are solid write automated UI tests for your core flows.

---

1. Generally, a metric of how many lines of code are hit by the test vs how many lines of code are in project.
2. Tests that compare strings become out of date any time the string changes, which can be often depending on what the string conveys. There may be some value in making sure the string says what you think it says, but since most people write the string once and then copy it over that value is largely illusionary. With constants you can test the constant itself (generally for type) and then assume them to be verified externalities in your subsequent tests.
3. You may have heard of _"fat models and skinny controllers"_ that's certainly better than the reverse, but as [Jon Cairns points out here](http://blog.joncairns.com/2013/04/fat-model-skinny-controller-is-a-load-of-rubbish/), that's not the whole story. What you _really_ want is _everything skinny_ your objects should have a tight focus whether they're Controllers, Data Models, Service Objects, etc. A "fat" model is probably a model that is doing too much. Whatever framework you use probably has tools to help with this, and if it doesn't it's generally easy to make your own. As a bonus, the skinner things are the more reusable they are. You may even find opportunities to create a library that you'll use across projects, and if you Open Source it, maybe I can use it too!
