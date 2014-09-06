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

[Never Unprepared: The Complete Game Master’s Guide to Session Prep](http://www.enginepublishing.com/never-unprepared-the-complete-game-masters-guide-to-session-prep) by Phil Vecchione

## Modes that I can think of

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

### Reviewing

* Refactoring the first pass to a bearable solution
* Writing an off-hand commit message
* Reviewing a branch not yet ready for pull request review
* Reflection
