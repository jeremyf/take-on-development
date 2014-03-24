# Command Line
\label{cha:command_line}

As an open source developer, I spend a fair amount of time on the command line.
I am by no means an expert, but there are tweaks that I've made to my development system that I find very helpful.

## My `dotfiles` project

The configuration files of my `$HOME` directory are as important as any code I write.
It is both the tools and toolbox that I carry with me to do my job.

After reviewing various [dotfile project's at dotfiles.github.io](https://dotfiles.github.io), [I forked](https://github.com/jeremyf/dotfiles/) [@holman](http://twitter.com/holman)'s [dotfile project](https://github.com/holman/dotfiles/). This meant switching the project from `zsh` to `bash`.

## My `\textasciitilde/.inputrc`

First I make sure that my command line navigation is up to snuff.
I export a custom [INPUTRC](http://www.gnu.org/software/bash/manual/html_node/Readline-Init-File.html) in my `\textasciitilde/.profile`.

```sh
if [ -f $HOME/.inputrc ]; then
  export INPUTRC="$HOME/.inputrc"
fi
```

<<(/Users/jfriesen/.inputrc, lang: sh)


## My `project` command

I [work on a lot of repositories](https://github.com/jeremyf) over the course of a week.
The vast majority of them are Ruby repositories.

As a matter of convention, all of my repositories are in `\textasciitilde/Repositories/`.
This convention and my `project` command means I can quickly access any project in the terminal.

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
