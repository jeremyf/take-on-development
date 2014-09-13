# Acceptance Testing

I have maintained that a software developer is analogous to an author.
And the production application is the book.
Few people would consider publishing a book without first having an editor.

In 2014, I began working with my first editor.
His name is Chris.
He is our Lead Quality Assurance Developer.

His job is to try to break the systems that I make.
And I am thankful for his dedication to the task.

He helps me drag features across the "mostly done" line and into the coveted "done done" area.
He bring closure to a task.
Ensuring that the nuances of a feature of fleshed out and not a half-baked solution.

We have had several discussions about our acceptance test tooling.
What follows is our attempt to distill those conversations.

## Understand your audience for the acceptance tests

Who will be reading these tests?

* Non-technical peole
* Technical-minded people
* Programmers

What is the purpose and scope of the software?

* Command line tools
* Web-based APIs
* Web-based UI in all its glorious CSS and Javascript
* An application
* A framework for building an application

Who will assist in writing the acceptance tests?

* Programmers
* Project Managers
* Patrons

How much effort will you place on automating the acceptance tests?

* Minimal effort, as we will click around the system
* Infinite effort, automate all the things
* Somewhere in between, most tasks will be automated yet we acknowledge a precision in language is required

## Address the Ecosystem

For the past two years I've worked under the following pattern:

* A Rails::Engine for defining the abstract application, and teasing apart isolated concerns.
* A Rails application that leverages the Rails::Engine, providing configuration and modifications.

It is much more of an art than science, but what I've found is the following:

Gems and Rails::Engines have an audience of programmers.
Make sure the acceptance tests are meaningful and expressive to them.
I prefer to write well-considered RSpec scenarios[^why_rspec] or Capybara scenarios if I have a UI.

The Rails applications that I work on have a varied audience.
Asking them to read RSpec scenarios or even Capybara scenarios is too much.
Instead we are pushing to use Fitnesse as our acceptance test methodology.

Fitnesse has one killer feature.
Anyone can write the documentation of how the system "is doing things."[^remember_the_documentation_lies]
And the documentation can be written such that it is verified by test code.

## Methodology

For acceptance tests, focus on writing clear examples.
This means a tight focus on the input parameters, the expected output, and function call that turns input into output.

## Tools of the Trade

### Capybara

This is my goto tool for testing UI features.
It uses a familiar syntax - ruby code - to express the tests.

If you find yourself in a position with lots of Capybara tests, take some time to craft Page Objects to help keep your Capybara CSS selectors tame. [SitePrism](https://github.com/natritmeyer/site_prism) is a gem that is an implementaiton of a Page Object Model.

If you write capybara tests, you can go so far as to run the tests in a browser.
Need to show your team what its doing, fire up the test using a Webkit or Firefox driver and let Capybara click through everything; Though you may want to add some sleep timers.

### Cucumber

Is it worth the effort?

### Fitnesse

[^why_rspec]: I contribute to ProjectHydra, and prior to my participation, it was agreed that ProjectHydra would use RSpec. It can be very powerful for writing expressive tests, with a focus on "natural" language. But in its accomodation for natural language, RSpec provides many different ways of saying the same thing. In other words, it can be very confusing to get started.

[^remember_the_documentation_lies]: Remember, [the documentation lies](/testing#sec-the_documentation_lies)