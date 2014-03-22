# Command Line
\label{cha:command_line}

## Bash Completion

## My `project` command

I [work on a lot of repositories](https://github.com/jeremyf) over the course of a week.
The vast majority of them are Ruby repositories.

As a matter of convention, all of my repositories are in `\textasciitilde/Repositories/`.
This convention, along with my `project` command means that from anywhere on my terminal, I can type the following.

`$ project hydra`

If I hit `tab` then I get a list for autocompletion.

```console
hydra                        hydra-collections            hydra-jetty
hydra-account_manager        hydra-derivatives            hydra-jetty-cookbook
hydra-camp                   hydra-ezid                   hydra-migrate
hydra-camp-devise-testing    hydra-file_characterization  hydra-mods
hydra-remote_identifier      hydramata                    hydra-capybara-walkthrough
hydra-head                   hydra-object_viewer          hydramaton
```

If I hit `enter` for `$ project hydra` then I basically my text editor to that directory.
In reality, I create a Sublime project for that directory and then open that project.

Below are the three scripts that are necessary for the above behavior.

### Code Sample for `project`

In `\textasciitilde/bin/project`

```ruby
  #!/usr/bin/env ruby -w

  project_name = ARGV[0]
  if !project_name && ENV['PWD']
    project_name = ENV['PWD'].split("/").last
  end

  if project_name
    project_file_name = File.join(
      ENV['HOME'],
      'Projects',
      "#{project_name}.sublime-project"
    )
    repository_dirname = File.join(
      ENV['HOME'],
      'Repositories',
      project_name
    )

    unless File.exist?(repository_dirname)
      $stdout.puts %(Missing unable to find #{project_name.inspect})
      $stdout.puts %(  in #{File.dirname(repository_dirname)}")
      exit(-1)
    end
    unless File.exist?(project_file_name)
      File.open(project_file_name, 'w+') do |file|
        file.puts %({)
        file.puts %(  "folders":)
        file.puts %(  [)
        file.puts %(    {)
        file.puts %(      "path": "#{repository_dirname}",)
        file.puts %(      "folder_exclude_patterns": [".yardoc", "pkg", "tags", "doc",  "coverage","tmp","jetty", ".bundle", ".yardoc"],)
        file.puts %(      "file_exclude_patterns": [".tag*", "*.gif", "*.jpg", "tags", "*.png", ".tags", ".tags_sorted_by_file", "*.log", "*.sqlite3", "*.sql"])
        file.puts %(    })
        file.puts %(  ],)
        file.puts %(  "settings":)
        file.puts %(  {)
        file.puts %(    "tab_size": 2)
        file.puts %(  })
        file.puts %(})
      end
      sleep(1)
    end
    `subl #{project_file_name}`
    $stdout.puts repository_dirname
    exit(0)
  else
    $stdout.puts "Example `#{File.basename(__FILE__)} project_name`"
    exit(-1)
  end
```

In `\textasciitilde/.profile`

```sh
  if [ -d ~/bin ]; then
    echo "$PATH" | grep -q "$HOME/bin:" || export PATH="$HOME/bin:$PATH"
  fi

  if [ -f ~/bin/bash_completion.d/project ]; then source ~/bin/bash_completion.d/project; fi
```

In `\textasciitilde/bin/bash_completion.d/project`

```sh
  # project completion for Sublime projects by Jeremy Friesen <jeremy.n.friesen@gmail.com>
  function _project {
    local cur

    COMPREPLY=()
    _get_comp_words_by_ref cur
    COMPREPLY=( $(find $HOME/Repositories -type d -maxdepth 1 -mindepth 1 -exec basename {} \; | egrep "^$cur"))
  }

  complete -F _project -o default project
  complete -F _project -o default p

  # Assumes that $HOME/Repositories houses all of your project repositories.
  # Assumes `project` accepts one argument for a directory that is in the
  #   $HOME/Repositories directory
```