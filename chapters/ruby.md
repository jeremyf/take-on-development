# Ruby

First, write your obligatory Hello World program.
I'll help you out so we can proceed:

```console
$ ruby -e 'puts "Hello World"'
```

Done!

Now on to other things.

## Idioms

When I started in Ruby, there were three foreign concepts: blocks, modules mixins, and method missing behavior. I'll add regular expressions, as I was just starting to tinker with them.

### Blocks

### Module Mixins

### Method Missing

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

```ruby
obj = Object.new
obj.method(:method_name).source_location
=> ["/path/to/ruby/file.rb", "LINE_NUMBER"]
```
## Ri

@TODO

### My `\textasciitilde/.irbrc`

## Byebug

@TODO - A Ruby debugger

## Pry

> "Pry is a powerful alternative to the standard IRB shell for Ruby.
> It features syntax highlighting, a flexible plugin architecture, runtime invocation and source and documentation browsing." - *[pryrepl.org](http://pryrepl.org/)*

I don't have a lot of experience with Pry, but it looks powerful.