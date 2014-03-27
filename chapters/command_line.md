# Command Line
\label{cha:command_line}

As an open source developer, I spend a fair amount of time on the command line.
I am by no means an expert, but there are tweaks that I've made to my development system that I find very helpful.

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
$ project hydra

hydra                        hydra-collections            hydra-jetty
hydra-account_manager        hydra-derivatives            hydra-jetty-cookbook
hydra-camp                   hydra-ezid                   hydra-migrate
hydra-camp-devise-testing    hydra-file_characterization  hydra-mods
hydra-remote_identifier      hydramata                    hydra-capybara-walkthrough
hydra-head                   hydra-object_viewer          hydramaton
```

Or, if I type `project hydra`, then hit `enter` my text editor opens that directory.
In reality, I create a Sublime project for that directory and then open that project; but to many it might look like I'm just opening the project.

Below are the three scripts that are necessary for the above behavior.

### Code Sample for `project`

In `\textasciitilde/Repositories/dotfiles/bin/project`

<<(/Users/jfriesen/Repositories/dotfiles/bin/project, lang: ruby)

In `\textasciitilde/Repositories/dotfiles/project/completion.bash`

<<(/Users/jfriesen/Repositories/dotfiles/project/completion.bash, lang: sh)

## Useful Shell Commands

When I'm not writing code in my text editor, I'm often on the command line.
If you are new to the Linux/Unix ecosystem it may be intimidating.

I am comfortable on the command line, but am not an expert.
In fact one of the reasons I like Ruby so much is that it integrates quite nicely with the command line.[^ruby_command_line_resources]

This is a small primer of only a handful of functions.
For more detail, I'd recommend seeking out other resources.

### grep

```console
$ man grep

The grep utility searches any given input files, selecting lines that match one
or more patterns. By default, a pattern matches an input line if the regular
expression (RE) in the pattern matches the input line without its trailing
newline. An empty expression matches every line. Each input line that matches at
least one of the patterns is written to the standard output.
```

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

### awk

### cut

### xargs

```console
$ man xargs

The xargs utility reads space, tab, newline and end-of-file delimited strings
from the standard input and executes utility with the strings as arguments.
```

A silly example, but one to illustrate the potential of `xargs`.
The following command `echo "hello.txt" | xargs touch` is analogous to `touch hello.txt`.
Both commands will create an empty file named "hello.txt".

The following script:

1. Finds all files with filenames that contain "hello"
1. Replacing the "hello" portion of the filename with "world"
1. Moving the files with filenames that contain "hello" to the replaced "world" filename.

`find . -name *hello* | sed -e "p;s/hello/world/" | xargs -n2 mv`

<!-- footnotes -->

[^ruby_command_line_resources]: One of the things I love about Ruby is how seamlessly it integrates with the command line. David Copeland's [Build Awesome Command-Line Applications in Ruby 2](http://pragprog.com/book/dccar2/build-awesome-command-line-applications-in-ruby-2) is one resource.

[^tell_me_about_a_tree_parser]: The tree parser's available at the time required that the entire XML document be read in one gulp. Each XML element would then be represented as one or more objects. So 30,000 top-level elements, and 30 or so child elements meant at least 900,000 XML specific objects would need to be created to represent that document, as well as the text and attributes. That is a ridiculous amount of objects to hold in memory.

[^tell_me_about_a_stream_listener]: A stream listener reads the XML document character by character and essentially notifies the listener when you are opening a tag, closing a tag, encountering cdata, etc. Needless to say, to use a listener a developer must potentially track a lot of state.