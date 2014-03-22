# Command Line
\label{cha:command_line}

## Bash Completion

## Brew

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

In `\textasciitilde/bin/project`

<<(/Users/jfriesen/bin/project, lang: ruby)

In `\textasciitilde/.profile`

```sh
  if [ -d ~/bin ]; then
    echo "$PATH" | grep -q "$HOME/bin:" || export PATH="$HOME/bin:$PATH"
  fi

  if [ -f ~/bin/bash_completion.d/project ]; then source ~/bin/bash_completion.d/project; fi
```

In `\textasciitilde/bin/bash_completion.d/project`

<<(/Users/jfriesen/bin/bash_completion.d/project, lang: sh)
