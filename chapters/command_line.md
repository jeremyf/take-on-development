# Command Line
\label{cha:command_line}

When I'm not writing code in my text editor, I'm often on the command line.
If you are new to the Linux/Unix ecosystem it may be intimidating.
I encourage you to spend time getting to know your command line.

## Useful Shell Commands

I am comfortable on the command line, but am not an expert.
In fact one of the reasons I like Ruby so much is that it integrates quite nicely with the command line.[^ruby_command_line_resources]

Below is a small primer of only a handful of functions.
For more detail, I'd recommend seeking out other resources.
[An excellent Bash cheatsheet can be found at learncodethehardway.org](http://cli.learncodethehardway.org/bash_cheat_sheet.pdf)

### Getting your bearings

The command line can be an initially disorienting location.
The following three commands are the basics for navigation: `pwd`, `ls`, and `cd`.

#### pwd - where am I at?

```console
$ man pwd

The pwd utility writes the absolute pathname of the current working directory to
the standard output.
```

#### cd - change where I am at

```console
$ cd path/to/another/directory
```

Change directory.

#### ls - see what is around me

```console
$ man ls

List directory contents
```

If you want to see information about files in your working directory, a quick `ls` will tell you.
You can provide an alternate directory.

#### which - where is the program file that is executing

```console
$ man which

The which utility takes a list of command names and searches the path for each executable file that would be run had these commands actually been invoked.
```

Out of the box your machine will come with lots of commands.
You may configure your $PATH to prepend a directory for custom installs.
After awhile you may not know which file is being call. `which` is here to help.

### man

```console
$ man man

format and display the on-line manual pages
```

If you have questions about any of the commands, try typing `man` and the name of the function.
This brings up the manual for that command.

Some manuals are better than others.

### grep

```console
$ man grep

The grep utility searches any given input files, selecting lines that match one
or more patterns. By default, a pattern matches an input line if the regular
expression (RE) in the pattern matches the input line without its trailing
newline. An empty expression matches every line. Each input line that matches at
least one of the patterns is written to the standard output.
```

When I first started open source programming, I had never heard of Regular Expressions.
The `grep` command changed that.

It is often the first tool I use for sifting through lots of files.
There are lots of flavors of `grep` that I have barely explored (`grep`, `egrep`, `fgrep`, `zgrep`, `zegrep`, `zfgrep`).

Good luck, and tell me what you find out.

#### ack

```console
$ man ack

Ack is designed as a replacement for 99% of the uses of grep.

Ack searches the named input FILEs (or standard input if no files are named, or
the file name - is given) for lines containing a match to the given PATTERN.
By default, ack prints the matching lines.
```

If you are using Mac OS X, you'll likely need to install ack or ag.

I haven't trained myself to use ack, but by many accounts it is more useful for current work.

### sed

```console
$ man sed

The sed utility reads the specified files, or the standard input if no files are
specified, modifying the input as specified by a list of commands.  The input is
then written to the standard output.
```

One of my early Rails projects was working with a massive XML document.
There were approximately 30,000 top level nodes each with 30 or so child/grand-child nodes.
It was impossible to load into a tree parser.[^tell_me_about_a_tree_parser]

I ended up writing a `sed` script that split the document into 30,000 lines.
Each line representing a single top level node and its child nodes.

From there I was able to read each line, and use a tree parser to individually parse each top-level node.
This solution was better than writing a [REXML::StreamListener](http://www.germane-software.com/software/rexml_doc/classes/REXML/StreamListener.html) and worrying about tracking tag open and tag end.[^tell_me_about_a_stream_listener]

### find

```console
$ man find

The find utility recursively descends the directory tree for each path listed,
evaluating an expression (composed of the `primaries' and `operands' listed
below) in terms of each file in the tree.
```

A powerful command which I most often use for listing filenames that match a textual pattern.

```console
$ find . -name my_ruby_file.rb
```

But wait, it can do so much more!
Consider the following example provided in `find`'s man page.

```console
# Delete all broken symbolic links in /usr/ports/packages

$ find -L /usr/ports/packages -type l -exec rm -- {} +
```

### xargs

```console
$ man xargs

The xargs utility reads space, tab, newline and end-of-file delimited strings
from the standard input and executes utility with the strings as arguments.
```

A simple example is perhaps best for explaining `xargs`.
The following command `echo "hello.txt" | xargs touch` is analogous to `touch hello.txt`.
Both commands will create an empty file named "hello.txt".

The following script:

```console
$ find . -name *hello* | sed -e "p;s/hello/world/" | xargs -n2 mv
```

1. Finds all files and directories with names that contain "hello"
1. Replacing the "hello" portion of the name with "world"
1. Move the files and directories with names that contain "hello" to files (or directories) with the "hello" portion of the name replaced with "world".

I haven't tested the above script for all scenarios, but it has served me well when used in conjunction with source control.

### Miscellaneous Commands

What follows are a handful of commands that I have stitched together.
There are likely other ways of doing these things, but they are the solutions that I have found.

#### Change directory into the parent directory of an executable file

```console
$ cd `which ruby`/..
```

The above command will find where your `ruby` executable is, then change into the containing directory of that executable. The backticks are for [command substition](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_04.html#sect_03_04_04). The `which ruby` is executed and the returned value is used in the context of the containing command. That is if `which ruby` returned `/path/to/ruby` then the above command would be equivalent to `cd /path/to/ruby/..`)

#### Kill every instance of Jetty

For some reason, Jetty doesn't always stop. I went ahead and created a `kill-jetty` alias that executes the following:

```console
$ ps ax | grep jetty | grep -v grep | sed "s/^ *//g" | cut -f1 -d " " | xargs kill -9
```

In writing this book, I learned that I could do the above with the very concise command:

```console
$ pkill -f jetty
```

The above string of commands highlights how simple Unix commands can be sewn together to do powerful things.

#### Commits since master

Within a git repository, count the number of commits that your current branch is ahead of the master branch.

```console
$ git log master..`git rev-parse --symbolic-full-name --abbrev-ref HEAD` --oneline | wc -l | tr -d " "
```

## My `dotfiles` repository
\label{sec:my_dotfiles_repository}

The configuration files of my `$HOME` directory are as important as any code I write.
It is both the tools and toolbox that I carry with me to do my job.

After reviewing various [dotfile project's at dotfiles.github.io](https://dotfiles.github.io), [I forked](https://github.com/jeremyf/dotfiles/) [@holman](http://twitter.com/holman)'s [dotfile project](https://github.com/holman/dotfiles/). This meant switching the project from `zsh` to `bash`.

## My `\textasciitilde/.inputrc`

First I make sure that my command line navigation is up to snuff.
I export the following custom [INPUTRC](http://www.gnu.org/software/bash/manual/html_node/Readline-Init-File.html).

<<(/Users/jfriesen/.inputrc, lang: sh)

To enable your `INPUTRC` add the following lines to your `\textasciitilde/.profile`.

```sh
if [ -f $HOME/.inputrc ]; then
  export INPUTRC="$HOME/.inputrc"
fi
```

*The dotfiles project handles this as part of its `script/bootstrap`.*

## My `project` command

I [work on a lot of repositories](https://github.com/jeremyf) over the course of a week.
The vast majority of them are Ruby repositories.

As a matter of convention, all of my repositories are in `\textasciitilde/Repositories/`.
This convention and my `project` command means I can open my projects with minimal typing.

On the command line, if I type `project hydra`, then hit `tab` I get an tab completion list of matching directories in the `\textasciitilde/Repositories/` directory.

```console
$ project hydra<tab>

hydra                        hydra-collections            hydra-jetty
hydra-account_manager        hydra-derivatives            hydra-jetty-cookbook
hydra-camp                   hydra-ezid                   hydra-migrate
hydra-camp-devise-testing    hydra-file_characterization  hydra-mods
hydra-remote_identifier      hydramata                    hydra-head
hydra-object_viewer          hydramaton
```

Or, if I type `project hydra`, then hit `enter` my text editor opens that directory.
In reality, I create a Sublime project for that directory and then open that project; but to many it might look like I'm just opening the project.

Below are the three scripts that are necessary for the above behavior.

### Code Sample for `project`

In `\textasciitilde/Repositories/dotfiles/bin/project`

@TODO - This is a rather lengthy file. A URL might be better served. Or an appendix entry?
<<(/Users/jfriesen/Repositories/dotfiles/bin/project, lang: ruby)

In `\textasciitilde/Repositories/dotfiles/project/completion.bash`

<<(/Users/jfriesen/Repositories/dotfiles/project/completion.bash, lang: sh)

<!-- footnotes -->

[^ruby_command_line_resources]: One of the things I love about Ruby is how seamlessly it integrates with the command line. David Copeland's [Build Awesome Command-Line Applications in Ruby 2](http://pragprog.com/book/dccar2/build-awesome-command-line-applications-in-ruby-2) is one resource.

[^tell_me_about_a_tree_parser]: The tree parser's available at the time required that the entire XML document be read in one gulp. Each XML element would then be represented as one or more objects. So 30,000 top-level elements, and 30 or so child elements meant at least 900,000 XML specific objects would need to be created to represent that document, as well as the text and attributes. That is a ridiculous amount of objects to hold in memory.

[^tell_me_about_a_stream_listener]: A stream listener reads the XML document character by character and essentially notifies the listener when you are opening a tag, closing a tag, encountering cdata, etc. Needless to say, to use a listener a developer must potentially track a lot of state.