# Ruby

First, write your obligatory Hello World program.
I'll help you out so we can proceed:

```console
$ ruby -e 'puts "Hello World"'
```

Done!

Now on to other things.

## Idioms

When I started in Ruby, there were three foreign concepts: blocks, modules mixins, and method missing behavior.
I'll add regular expressions, as I was just starting to tinker with them.

### Instance Method vs. Class Method Annotation

Consider the following class. You want to write about that class in a commit message, email, or IRC.

```ruby
class MyClass
  def self.a_method
    'class method'
  end
  def a_method
    'instance method'
  end
end
```

To write about the class method, use `MyClass.a_method`. To write about the instance method, use `MyClass#a_method`.

### Blocks

With the rise of Javascript, the idea of blocks is less obtuse.
They can be thought of as [anonymous functions](http://en.wikipedia.org/wiki/Anonymous_function).

In other words, when you pass a block as part of your message, the receiver decides how to handle the block.
It could:

* Ignore it
* Call it 1000 times
* Pass it on as lambda to another method invocation

As with all functions, blocks take parameters.
The `#each` method is a common receiver of a block, yielding one parameter.

```ruby
[1,2,3,4].each do |index|
  puts index
end
```

The above Ruby code will write to STDOUT 1,2,3, and 4; Each separated by a new line.

You can also capture the block, storing it in an instance variable, and later executing that block.
This is a very powerful tool for configuration management.
More on that in the [Rails](/rails#cha-rails) section.

**Warning** Every method can take a block. But not every method will yield to the block it received.
There have been plenty of times where I've typed the equivalent of `[1,2,3,4] {|i| puts i }` and never seen any output.
You have been warned.

Then again, it can be helpful to not yield for every block. Or yield multiple times. Its up to the receiver of the block to determine what to do with it.

Consider the following example:

```ruby
request { |response|
  response.success { send_report }
  response.failure { retry }
}
```

We do not want both `send_report` and `retry` to be executed each time a request is made.

### Module Mixins

Module Mixins are a powerful tool for object composition.
But be careful, as you can craft a nightmare object by mixing in so many modules.

Module Mixins trample on encapsulation.
As I've worked with Ruby I've started associating Module Mixins as an intermediary step in refactoring.

I find common behavior amongst two or more objects.
I tease apart the common behavior, putting that behavior in a module.

I test the module in isolation.
Then mix the module back into the associated parent classes.

Often, I will stop there.
But the decision to stop does not come without cost.

Modules are horrible at encapsulation.
They can trample on other methods of the containing class.
And it is difficult to keep the module isolated from other aspects of the containing class.

But they are powerful. And pervasive in the Ruby (on Rails) ecosystem.

### Method Missing

Ruby exposes a powerful, yet easy to abuse tool: `method_missing`.

If you implement `method_missing` don't forget to:

* implement the corresponding `respond_to_missing?`.
* capture the method arguements
* capture any block that might be associated with the call

Failure to account for the above caveats can result in very difficult code to test.

At one point in 2011, I found a nasty [bug in ActiveRecord::Base#method_missing](https://github.com/rails/rails/commit/f2a0dfc2985c008a618e1616f6cf9a4c54098c33).
I ended up spending several hours tracking it down. Then nursing a monkey patch in our application until my pull request was part of a released version of Rails.

### Regular Expressions

## Interactive Ruby Shell (irb)

```console
$ man irb

irb is the REPL(read-eval-print loop) environment for Ruby programs.
```

Back to the Hello World example.

```console
$ irb
>> puts 'Hello World'
Hello World
=> nil
>>
```

### Source Location

This is a helfpul trick:

```ruby
obj = Object.new
obj.method(:method_name).source_location
=> ["/path/to/ruby/file.rb", "LINE_NUMBER"]
```

### My `\textasciitilde/.irbrc`

A few helpful tweaks for IRB:

<<(/Users/jfriesen/Repositories/dotfiles/ruby/irbrc.symlink, lang: ruby)

Or if you prefer, replace the default IRB behavior with Pry.

```ruby
require 'rubygems'
require 'pry'
Pry.start
exit
```

## Pry

> "Pry is a powerful alternative to the standard IRB shell for Ruby.
> It features syntax highlighting, a flexible plugin architecture, runtime invocation and source and documentation browsing." - *[pryrepl.org](http://pryrepl.org/)*

I started using Pry in the summer of 2014.
I had trouble rebuilding Byebug for my debugger.
I opted to give Pry a try.

Based on how I had used Byebug, out of the box Pry had enough features for me to hobble along.
Then I installed `pry-debugger` and I found myself no longer needing `byebug`.

It is a compelling replacement for IRB and Byebug.
I am making a comittment to practice using Pry and exploring more of it.

Launch `pry` from the command line then walk along:

```ruby

# See the methods for the current context
pry(main)> ls

self.methods: inspect  to_s
locals: _  __  _dir_  _ex_  _file_  _in_  _out_  _pry_

# Show information about in FileUtils
pry(main)> ls FileUtils
constants: DryRun  Entry_  LOW_METHODS  LowMethods  METHODS  NoWrite  OPT_TABLE  StreamUtils_  Verbose
FileUtils.methods:
  cd       chown           commands        copy_entry   cp_r          install
  ...(And more methods)
instance variables: @fileutils_label  @fileutils_output

# Change context to the FileUtils module
pry(main)> cd FileUtils
pry(FileUtiles)> show-method rm

From: /Users/jfriesen/.rvm/rubies/ruby-2.1.2/lib/ruby/2.1.0/fileutils.rb @ line 562:
Owner: #<Class:FileUtils>
Visibility: public
Number of lines: 10

def rm(list, options = {})
  fu_check_options options, OPT_TABLE['rm']
  list = fu_list(list)
  fu_output_message "rm#{options[:force] ? ' -f' : ''} #{list.join ' '}" if options[:verbose]
  return if options[:noop]

  list.each do |path|
    remove_file path, options[:force]
  end
end
```

Great stuff. And `pry-debugger` introduces setting dynamic breakpoints and other such goodies.

## Byebug

@TODO - A Ruby debugger
