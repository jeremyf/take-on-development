# Modes of Development

For me, software development is a juggling act.
I jump from deep concentration to guiding another developer to answering an unrelated work email over to a chat with a remote developer then off to a meeting.

It is a challenge to remain focused.
But for me it is a requirement to get things done.

As I've transitioned into a mentor and lead role, I am also responsible for growing my teams capabilities.
This runs contrary to keeping focused.

Over the past year I've worked towards adopting explicit modes of operation.
I need to enter into different head spaces.

Look to the venerable and beloved `vi` and `vim`.

It has the concept of modes:

* Normal (Command)
* Insert
* Command-Line
* Replace
* Visual
* Select

[VIM Modes Transition Diagram](https://darkpan.com/files/vim.svg) by Marco Fontani

These modes focus on the tasks you are trying to accomplish.
Each mode has a single responsibility.

## Its Red, Green, Refactor

Red, Green, Refactor is a hallmark Test Driven Development.

* **Red:** Write a test that will verify something works, before you write the thing to make it work.
* **Green:** Write the thing to make your test pass.
* **Refactor:** Improve on your solution to the problem.

It is a powerful method for solving a problem.
But is incomplete.

Before I can get to Red I need to know what I am trying to solve.
A proposed solution is a response to an observation.
The proposed solution is a hypothetical solution to a real world problem.

Once I have a proposed solution, I forumalate how I will verify my solution.
Then I analyze the results of the tests and the solution.

This cleaves close to the [scientific method](http://en.wikipedia.org/wiki/Scientific_method)

* Observe
* Conjecture
* Predict
* Test
* Analyze

The Red, Green, Refactor is the manifestation of the Test and Analyze steps of the scientific process.

Important in the Red, Green, Refactor methodology, is my recognition of which mental state in which I am working.
There have been too many times where I've been in a Refactor mode and drifted towards writing new features.

What ends up happening is I end up with a very dirty working directory.
I have lots of changes and layers of abstraction that are comingled.
I end up spending a bit of time using git's interative shell to pick apart the larger ideas.

## Never Unprepared

I am an avid player and facilitator of table top role-playing games.
You've been warned.

> Take something complicated, break it up in to manageable parts, and then tackle them over time in order to achieve a goal. -- *Phil Vecchione*

In 2012 I picked up a copy of Phil Vecchione's [Never Unprepared: The Complete Game Master’s Guide to Session Prep](http://www.enginepublishing.com/never-unprepared-the-complete-game-masters-guide-to-session-prep). Phil is a gamer at heart, and a project manager by trade. "Never Unprepared" is the intersection of the time management skills of a professional project manager and his hobby.

Phil speaks about the five steps of preparation.

* Brainstorming - Spawn lots of ideas
* Selection - Winnow down the ideas
* Conceptualization - Expand on the selected ideas
* Documentation - Write down meaningful notes for the concepts
* Review - Reconcile the notes for consistency

In identifying the steps, Phil is creating boundaries for the types of tasks he does.
In creating these boundaries, he declares the constraints on the time he is working.

There is no place for rejecting ideas during the brainstorming nor documentation phase.
Selection is the time for doing so.

More than any software development book, Never Unprepared is a guide for my day to day professional life.

It also helped me think about the different mental modes that I might enter over the course of a work day.
What follows is a survey of the various modes that I enter.
As a junior developer some of these modes may not be applicable.
As a mid-level developer many of them may be applicable.

## Modes that I can think of

What follows is an inventory of the modes of thinking in which I find myself.

### Meeting Mode

* **Goal:** Capture group decisions, action items, keep things moving.
* **Method:** Have an agenda. Have a facilitator, note taker, and time keeper. Be quick to appoint small groups.

### Thinking on a Solution

* **Goal:** To arrive at a decision that can be acted on.
* **Method:** Go for a walk. Talk it over with someone. Draw and diagram. Prototype code.

### Writing an Isolated Test

* **Goal:** To build a supporting case for an integration test.
* **Method:** Use low-overhead collaborators; Mocks and stubs are great, production data structures are also great.

### Writing an Integration Test

* **Goal:** To formalize a method for asserting that a solution is acceptable.
* **Method:** Think not on the solution, but how the solution can be verified.

### Writing a First Pass Solution

* **Goal:** Get an integration test passing; Assert that something works.
* **Method:** Write a class that attempts to resolve the solution. Look towards collaborators necessary to solve the problem. Keep SOLID principles salient. Jump into isolated tests to flesh out the core class and its contributors.

### Refining How a Test Reads

* **Goal:** Create a document that can be used as a reference point into the system
* **Method:** Write the tests for clarity and expressiveness. Convey meaning and how things are assembled. In my experience this focusing on legible and digestable tests is stronger than any README documentation.
* **Caveat:** Documentation lies. Consider documentation that can assert it is correct. That documentation is an automated test.

### Documentation

* **Goal:** Convey high level concepts; Why things are being done, not how; The code describes how things are done.
* **Method:** Write brief descriptions. Bullet points are your friend. Write for the web.
* **Caveat:** See Refining How a Test Reads

### Writing a Commit Message

* **Goal:** To create a helpful message to future developers
* **Method:** Follow a well established pattern for commit messages; 50 character first line, references to issue tracker incidences, meaningful message body if the concept is complicated.
* **Caveat:** If I am working on a feature that will require multiple commits, I will make "disposable commits" along the way. These commits are mental placeholders. I will revisit them as I prepare a branch for merging.

### Preparing a Pull Request

* **Goal:** To present an atomic chunk of work for final review.
* **Method:** Squash commits into logical chunks. Expand on any terse commit messages. Take time to communicate the intentions of the code.

### Reviewing a Pull Request

* **Goal:** To make sure the code is doing the right thing (in the right way).
* **Method:** Reconcile the commit message, code comments, code, and associated tickets/stories. Ask questions of the developer.

### Word Smithing

* **Goal:** To write meaningful copy for patrons of the software I'm writing.
* **Method:** Stop and think about how the patron will encounter the copy. What needs to be said?

### Exploring an External Dependency

* **Goal:** To assess and determine the viability of an external solution.
* **Method:** Read the README. Check the test suite for existence, legibility, and clarity. Check other adopters (i.e. ruby-toolbox.com). Attempt to run the tests. Check code coverage and quality (i.e. coveralls and code climate). Check commit messages for clarity. Look at frequency of contributions. Look for similar solutions.

### Writing Blog Posts

* **Goal:** To assimilate lessons learned and convey those lessons in a digestible format.
* **Method:** Write concise posts. Build from previous posts. Explore ideas. Offer links to supporting evidence. Highlight lessons learned. Take a risk. Accept amendments.

### Refactoring

* **Goal:** To move the code to a more expressive state.
* **Method:** Create a new branch. Baby step commits, the messages are disposable. Craft the final commit message. If new ideas bubble up, create another branch and explore. A flurry of commits, sometimes spanning multiple branches. Each branch an atomic concept.
* **Caveat:** Once the refactor is complete, prepare a pull request.

### Reviewing a branch not yet ready for pull request review

* **Goal:** To help give shape to the solution as it is worked on by others
* **Method:** Ask lots of questions. Why this particular name? What do you mean here? Is there an abstraction you are wrestling with?

### Story Triage

* **Goal:** To expand user stories to more actionable developer tasks
* **Method:** Review the existing story and think about the impact on the existing system. Think about strange states. Ask about all the UI components; What should the copy be? What should the UI experience be? Think of other related things that could be abstracted.

### Unearth a Problem

* **Goal:** To identify a problem and how this problem manifests
* **Method:** Ask lots of questions. Poke and prod at assumptions. Review commit logs to see if there is churn on a particular constellation of files. Challenge each and every "We should do [better at]..." there is a problem in there, noodle on it. Roll it around.
