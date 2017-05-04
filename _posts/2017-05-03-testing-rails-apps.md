---
layout: blog
comments: true
title:  "Testing Rails Applications"
date:   2017-05-03
categories: development, testing
blurb: "Testing strategies serve one purpose - to prevent and fix bugs earlier in the development process. Here's some bullet points on achieving that in Rails."
---

# Testing Rails Applications

## General

One size does not fit all. Testing strategies serve one purpose - to prevent and fix bugs earlier in the development process. While they can also document your code and provide other additional benefits - **fixing and preventing bugs must be their number one goal**. Whatever strategy fits your project, your team, and your code base - _and fulfills that goal_ - is a good strategy. The core of any good Rails testing strategy is [Better Specs](http://betterspecs.org/) and [The Agile Test Pyramid](https://martinfowler.com/bliki/TestPyramid.html).

Finally, **tests must be written to be re-written**. Business requirements will change. Code architecture will change. Variables will be renamed. Your tests should enable and embolden these changes, not prohibit and prevent them.

> "All is flux." - Heraclitus

## Unit Testing

1. For every file, there is a test file.

        app/models/foo.rb

        spec/models/foo_spec.rb


    For inherited files like application_controller.rb or composed files like app/models/concerns/foo.rb, if there is logic in the file there should be a test file that creates a dummy object to use for testing. Auto-generated files, static files (like .yml or .json), and other configuration files do not need testing.

2. For every method, there is a test method.

        def foo
        end

        describe '#foo' do
        end

        def self.bar
        end

        describe '.bar' do
        end


    > "Be clear about what method you are describing. For instance, use the Ruby documentation convention of . (or ::) when referring to a class method's name and # when referring to an instance method's name. " - [Better Specs](http://betterspecs.org/#describe)

3. Unit tests are [solitary](http://blog.jayfields.com/2014/07/solitary-unit-test.html). If the method touches an object other than itself or its parent(s) that object should be [doubled](https://github.com/rspec/rspec-mocks).

4. Use contexts to test branch conditions.

        # method:
        if x == y
        else
        end
        # test:
        context 'when x equals y' do
        end
        context 'when x does not equal y' do
        end

    If testing branch conditions becomes difficult or your tests are hard to read/follow your method is doing too much or you need to "[flatten your arrow code](https://blog.codinghorror.com/flattening-arrow-code/)" - or both.

5. Don't test strings. You can test against variables that hold stings, or objects that return strings, but never test a string directly. When testing against a variable, name it such that it's clear what is significant about that string - `valid_user_id`, `name_with_too_many_characters`, etc.

    Using constants can help with this. If your object keeps its strings in constants you can test the constant itself directly and then use it as an expected result. This approach is "impure," but the the pragmatic upside is worth it.

    Don't forget to use [let()](https://www.relishapp.com/rspec/rspec-core/v/2-5/docs/helper-methods/let-and-let).

    > "When you have to assign a variable instead of using a before block to create an instance variable, use let. Using let the variable lazy loads only when it is used the first time in the test and get cached until that specific test is finished." - (http://betterspecs.org/#let)[Better Specs]

6. Don't Repeat Yourself ([DRY](https://en.wikipedia.org/wiki/Don't_repeat_yourself)) applies in tests much like it does in application logic. [Factories](https://github.com/thoughtbot/factory_girl), [shared-examples](https://www.relishapp.com/rspec/rspec-core/v/2-11/docs/example-groups/shared-examples), [before statements](https://www.relishapp.com/rspec/rspec-core/v/2-2/docs/hooks/before-and-after-hooks), and high level let() statements are all tools to help make this possible.

    > "Every piece of knowledge must have a single, unambiguous, and authoritative representation within a system." - [The Pragmatic Programmer](https://www.amazon.com/Pragmatic-Programmer-Journeyman-Master/dp/020161622X)

7. Trust your code. If you write a method in an object, test that method. If another method in that object calls that method - trust that it does its job. If a method returns a bool you don't need to test what would happen if it returns a sting. Just make sure when you test the bool returning method to ensure that it indeed returns a bool. If you do this and are suspicious of your code - take that as a sign that your code is too complex (interconnected).

## Service Testing

1. Service Tests in Rails are "feature tests" (or [Subcutaneous tests](https://martinfowler.com/bliki/SubcutaneousTest.html)).

    > "I use subcutaneous test to mean a test that operates just under the UI of an application. This is particularly valuable when doing functional testing of an application: when you want to test end-to-end behavior, but it's difficult to test through the UI itself." - [Martin Fowler](https://martinfowler.com/bliki/SubcutaneousTest.html)

2. Feature tests test core flows. Don't test every possible flow. Flows will change - flows _need_ to change. Tests shouldn't inhibit this. Instead, Feature Tests should provide confidence that whatever else may be be broken or may have changed - sign up, sign in, payment, or other absolutely crucial functions **work**.

## UI Testing

1. UI Tests are about user experience (at the "can use" vs. the "joy to use" level). This means that in Rails load testing / performance testing, and UI testing are all deeply intertwined. There are times when they should be approached separately, but often they can be handled at once.
