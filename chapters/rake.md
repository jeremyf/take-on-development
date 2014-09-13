> Status: @READY_FOR_QA

# Rake

One of the late [Jim Weirich](http://en.wikipedia.org/wiki/Jim_Weirich)'s pervasive contributions to the Ruby community.
For many it is synonimous with "the script that run's my Rails project's tests."

It is more than that.
It is a powerful build program.

```console
$ man rake

Rake is a simple ruby(1) build program with capabilities similar to the regular make(1) command.

Rake has the following features:

o   Rakefiles (Rake's version of Makefiles) are completely defined in standard Ruby syntax.  No XML files to edit. No quirky Makefile syntax to worry about (is that a tab or a space?).
o   Users can specify tasks with prerequisites.
o   Rake supports rule patterns to synthesize implicit tasks.
o   Flexible FileLists that act like arrays but know about manipulating file names and paths.
o   A library of prepackaged tasks to make building rakefiles easier.
```

## rake -w

Invoke rake with the `-w` option to see where each task is defined.

```console
$ rake -w

rake install    ./bundler-1.5.2/lib/bundler/gem_helper.rb:43:in `install'
rake load_app   ./railties-4.0.3/lib/rails/tasks/engine.rake:1:in `<top (required)>'
rake release    ./bundler-1.5.2/lib/bundler/gem_helper.rb:48:in `install'
```

## The Rake Field Manual

My appreciation for Rake continues to grow.
Fanned ever higher by [Avdi Grim's "Learn advanced Rake in 7 episode"](http://devblog.avdi.org/2014/04/30/learn-advanced-rake-in-7-episodes/) and his upcoming ["Rake Field Manual"](http://www.rakefieldmanual.com/).

I'm not going to dive any further into this than to say, take a look at Avdi Grim's resources.
He's built [Quarto - an ebook generation toolchain powered by Rake](https://github.com/avdi/quarto).