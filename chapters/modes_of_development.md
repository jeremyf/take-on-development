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

Goal: Capture group decisions, action items, keep things moving.
Method: Have an agenda. Have a facilitator, note taker, and time keeper. Be quick to appoint small groups.

### Thinking on a Solution

Goal: To arrive at a decision that can be acted on.
Method: Go for a walk. Talk it over with someone. Draw and diagram. Prototype code.

### Writing an Isolated Test

Goal: To build a supporting case for an integration test.
Method: Use low-overhead collaborators; Mocks and stubs are great, production data structures are also great.

### Writing an Integration Test

Goal: To formalize a method for asserting that a solution is acceptable.
Method: Think not on the solution, but how the solution can be verified.

* Writing the first pass of a solution
* Working on a feature as isolated tests begin passing but the integrated tests continue to fail
* Refining how a test reads
* Refactoring the first pass to a bearable solution
* Writing an off-hand commit message
* Preparing a branch for a pull request
* Reviewing a pull request
* Reviewing a branch not yet ready for pull request review
* Meetings - my goal is to get out of meetings as quick as possible with clear action items
* Reflection
* Word Smithing