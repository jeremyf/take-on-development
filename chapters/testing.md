# Testing
\label{cha:testing}

> We write tests first because we find that it helps us write better code.
> Writing a test first forces us to clarify our intentions, and we don’t start the next piece of work until we have an unambiguous description of what it should do.
> –- Kent Beck's forward for "Growing Object-Oriented Software, Guided by Tests" by Steve Freeman and Nat Pryce.

## Wisdom is Learning from Other People's Mistakes

My first Rails project started December 2005.
I dove in and began writing the production code.
I was learning Rails for the first time.[^learning_rails_for_the_first_time]
It was a volitale period in which Rails and its echo system were rapidly evolving.

So much was changing, and I was working at learning it all, that I didn’t feel I could add "writing tests" to the list of things I could do.

And I learned this was the path of pain.
I was writing bugs – every developer does this – and the ecosystem was changing from beneath me.
Everything was in motion.

My code was sloshing around, collapsing in on itself.
And my dependencies were being updated, mangling what I had done.[^a_commitment_to_semantic_versioning]

It was a nightmare of fragility.
Had I been writing tests, the nightmare would have been real, but there would have been at least one more thing verifying that what I did yesterday worked today.

Today, I write tests.
When I am thinking about a solution, I also ask myself "How will I go about verifying the solution?"
I capture the answer to the form in my "production" code and the latter in my "test" code.
Both are important.

## Types of Tests

As you are exploring testing you may hear about all sorts of tests: Unit, Functional, Integration, Component, System, Exploratory, Feature, Acceptance, etc.

You may hear about Test-Driven Development and Behavior-Driven Development.

There is a lot of discussion regarding tests. At this point, I would recommend thinking about tests as belonging to two categories:

* Isolated
* Integrated

[Dr. Alan Kay](http://en.wikipedia.org/wiki/Alan_Kay), an author of Smalltalk, coined the term object-oriented. Dr. Kay posited that objects are similar to biological cells that send each other messages.

Think of isolated tests as testing a single cell. This is where you make sure the cell is operating in a well-structured manner. *Isolated tests make sure I'm writing code the right way.*

Think of integrated tests as tests that coordinate the interaction of multiple cells. This is where you make sure your organism is operating as expected. *Integrated tests make sure I'm writing the right thing.*

I recommend reading [“The Clean Coder: A Code of Conduct for Professional Programmers”](http://www.amazon.com/The-Clean-Coder-Professional-Programmers/dp/0137081073) by Robert C. Martin. In chapter 8 he explains the various tests, as well as the ratio of each type of test.

## The Documentation Lies
\label{sec:the_documentation_lies}

I maintain that the first tattoo I get will be the words "The Documentation Lies."
I have seen well intentioned efforts to write documentation come up short.
Effort is spent describing how the system should be working; Or how the system interacts with other systems.

And three months after a documentation push, the documentation is out of date.
It provides incorrect instructions.
Or does not reflect the current and changing reality.

Part of the cure for lying documentation is to write tests.
Tests explain how things are working.
And what the system interactions are.

Write tests that have clear examples of input and output.
Draw attention to those tests.
Steer your adopters to those tests.
Place an effort on making these tests understandable with minimal up front domain knowledge.

For recent projects, [Hydramata::Works](https://github.com/ndlib/hydramata-works) and its sibling [Hydra Connect Demo](https://github.com/ndlib/hydra_connect_demo), I have made a commitment to grooming a "Getting Your Bearings" section of the README.
This section points to tests that document what the system is doing.

And [Travis CI](http://travis-ci.org) asserts the documentation on each commit.

## Writing Tests

Practice writing tests.

If you don't do it, pick something and practice.
Take a look at the [Bowling Game Kata](http://butunclebob.com/ArticleS.UncleBob.TheBowlingGameKata) or [Conway's Game of Life](http://en.wikipedia.org/wiki/Conway's_Game_of_Life).

If you do it, but only after you have written your production code, then try your next problem by first writing the test you would use to verify the behavior. It is a different way of thinking, but you will


[^learning_rails_for_the_first_time]: According to David Heinemeier Hansson, ["Rails itself is a carefully curated collection of APIs and DSLs."](http://david.heinemeierhansson.com/2012/the-parley-letter.html).
It is an active curation process. And as understanding grows and changes, so to does the system. I've learned Rails 0.x, 1.x, 2.x, 3.x, and 4.x. From 2.x to 3.x it was as though I had to learn Rails again.

[^a_commitment_to_semantic_versioning] This was in the day of aparrent arbitrary versioning. [Semantic Versioning](http://semver.org/) may have been the goal, but the reality was a hellish landscape. Please take some time to read up on [Semantic Versioning](http://semver.org/) and commit to abiding by that discipline.