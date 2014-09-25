# Rails
\label{cha:rails}

## Fundamentals

Server processes a request and sends a response. Browser interprets the response and may:

* Issue a new request without user knowledge (i.e. follow a 302 response to its location)
* Render the response in the negotiated format

Static Pages vs. Application Processed vs. Forwarded

## Rails command

@TODO

### Rails generator

@TODO

### Rails engines

@TODO

## Rails application templates

## Effective Use of ActiveRecord

> Active Records are special forms of DTOs [Data Transfer Objects]. They are data structures with public variables; but they typically have navigational methods like *save* and *find*. Typically these Active Records are direct translations from database tables, or other data sources.
>
> Unfortunately we often find that developers try to treat these data structures as though they were objects by putting business rule methods in them.
> This is awkward because it creates a hybrid data structure and an object.
>
> The solution, of course, is to treat the Active Record as a data structure and to create separate objects that contain the business rules and that hide their internal data (which are probably just instance of the Active Record).
>
> -- Martin, Robert C. "Clean Code: A Handbook of Agile Software Craftsmanship (Robert C. Martin Series)"

Traditionally, Rails pushed ActiveRecord objects towards Fat Models.
I blame [Fat Models, Skinny Controllers](http://weblog.jamisbuck.org/2006/10/18/skinny-controller-fat-model).
But I am not without blame.
I jumped on the Fat Models train.

I remember early in Rails development having MVC related arguements about where things should go.
My coworker said "In the controller" and I said "In the model."

It turns out we were both wrong.
But we didn't have a noun to attach the behavior to.
We were talking about a Query object; Something that finds the objects that we need.
In other cases we needed a Command object; Something that transforms an object.

### Single Responsibility Principle

If your class inherits from another, you are signing a contract stating that when the ancestor changes, your class will also change.
In other words, your object, begins life with with one reason for changing.
And the Single Responsibility Principle says an object should have one reason to change.

## A Non-Exhaustive Curated Collection of Blogposts

[7 Patterns to Refactor Fat ActiveRecord Models](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/)
[Testing from the Outside In](http://robots.thoughtbot.com/testing-from-the-outsidein)
