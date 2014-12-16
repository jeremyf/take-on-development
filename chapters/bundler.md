# Bundler
\label{cha:bundler}

> "Bundler maintains a consistent environment for ruby applications.
> It tracks an application's code and the rubygems it needs to run, so that an application will always have the exact gems (and versions) that it needs to run." *[bundler.io](http://bundler.io/)*

Once upon a time, in the dark days of yore, I was working on two Rails projects at the same time.
Bundler did not yet exist. The pain of dependency management was intense. Gems were a shared jumbled mess.

Synchronizing gems amongst different developers was one challenge.
Another was ensuring the gem setup was correct on the various production related environments.

If I were to develop just one project on my machine I wouldn't need bundler.
But it is a part of the Ruby ecosystem now.
Even if you work on one project, Bundler is easy enough to use to be worth the overhead.
And I can assure you that you will work on more than one project on your machine.

## Gemfile

A Gemfile lists the explicit dependencies of a Ruby project.
The Gemfile.lock[^gemfile_lock], if one exists, lists the resolved dependency graph, down to the specific version of each gem in the dependency graph.

If you have a Gemfile but not a Gemfile.lock, running `bundle` in the project's root directory will generate a Gemfile.lock for the project.
The resulting Gemfile.lock is the evaluated dependency graph *for your machine*.[^evaluated_dependency_graph_for_your_machine] If someone else were to run `bundle` against the same Gemfile their resulting Gemfile.lock might vary.

However, once the Gemfile.lock is created, running `bundle` will install the same things[^gemfile_lock_variances].

Your Gemfile can reference gems that are:

* Up on Rubygems.org
* Are a particular branch on Github
* Located on your local file system
* Or any other gem source that you register

## Bundle Show

```console
$ bundle help show

Show lists the names and versions of all gems that are required by your Gemfile.
Calling show with [GEM] will list the exact location of that gem on your machine.
```

Of the two options – with or without a gem name - I more often use `bundle show <name_of_gem>`.[^why_bundle_show]
I want to know where a gem was installed more often than I want to see the gem list.

And I often follow with `bundle open <name_of_gem>`.

## Bundle Open

```console
$ bundle help open

Opens the source directory of the given bundled gem
```

When I want to dig around in the gem's executed code, I run `bundle open <name_of_gem>`.
My text editor pops open and I begin the spelunking; All of the gem's code is there to review.[^well_not_all_of_it]

Sometimes I'll bring a pickaxe to the excavation and start modifying the code;
Insert a debugger statement in one place[^dont_forget_to_clean_up];
Log parameters and collaborators in another location.

All of which is made easy by `bundle open <name_of_gem>`.

## Bundle Console

```console
$ bundle help console

Opens an IRB session with the bundle pre-loaded
```

I learned about this command late in 2013; Its been around longer than that, but I was a little dense in my failure to notice the command[^regularly_dash_help].

I prefer to stay out of the console and instead rely on tests, but it is another tool for exploring how your code is behaving.[^if_you_type_it_in_console_once_consider_a_test]

## Bundle Outdated

```console
$ bundle help outdated

Outdated lists the names and versions of gems that have a newer version
available in the given source. Calling outdated with [GEM [GEM]] will only check
for newer versions of the given gems. Prerelease gems are ignored by default.
If your gems are up to date, Bundler will exit with a status of 0. Otherwise,
it will exit 1.
```

As an Open Source Developer, your dependency landscape is shifting beneath you.
Pay attention to changes in your dependencies.[^if_its_volitale_be_careful]

## Bundle Update

```console
$ bundle help update

Update  the  gems  specified  (all  gems,  if  none  are  specified), ignoring
the previously installed gems specified in the Gemfile.lock. In general, you
should use `bundle install` to install the same exact gems and versions across
machines. You would use bundle update to explicitly update the version of a gem.
```

This removes the Gemfile.lock and generates a new one.
It may create an identical Gemfile.lock (if you run `bundle update` back to back it has a high probability of being identical).
If a lot of time has elasped between updates at least one dependency will have changed.

Before I run `bundle update` I do my best to make sure:

* that my tests are all passing
* that I have a clean working directory

After I've run `bundle update` I again do my best to make sure:

* that my tests are all passing
* that I understand what has changed amongst the dependencies

Assuming I am satisfied with my preliminary inspection I then stage and commit only the Gemfile.lock, commenting that I ran `bundle update`.[^run_a_script_then_commit].
I rely on git and the focused commit to ensure that I can revert my Gemfile.lock; Passing tests never guarantee that something works.
This is most evident I update a Gemfile.lock and issues are found a day or so later.

Also consider the more targeted `bundle update <gem_name(s)>`. This command will keep all explicit locks except for the named gem(s). The named gem(s) will be updated along with those gem's dependencies.

## Bundle Gem
\label{sec:bundle-gem}

<!-- footnotes  -->
[^gemfile_lock]: If you are working on your own gem, make sure to not checking in your local Gemfile.lock. [More from Yehuda Katz, creator of Bundler can be found at [http://yehudakatz.com/2010/12/16/clarifying-the-roles-of-the-gemspec-and-gemfile/](http://yehudakatz.com/2010/12/16/clarifying-the-roles-of-the-gemspec-and-gemfile/).

[^if_you_type_it_in_console_once_consider_a_test]: If you find yourself in a console "exploring things" please consider codifying that exploration into a test. Please capture your ad hoc exploration's "notes" for future spelunkers and code delvers. Once you have the test make sure your commit message explains what was happening. Trust me, your future self and those working on your project later will appreciate your carefully considered notes.

[^why_bundle_show]: When I do use `bundle show <gem_name>` it is almost always followed by `bundle open <gem_name>`. Other times I am verifying the file system location of a gem that was declared with a `:path` or `:github` option (i.e. `gem "orcid", path: "../orcid"` or `gem "mappy", github: "jeremyf/mappy"`).

[^well_not_all_of_it]: Well not all of it. Its possible via the gemspec declaration that not all files were declared. Some people don't include the test or spec directory in their gemspec. Not cool! Personally I expect anything and everything that may be relevant to the workings of the code (and is not generatable) to be included.

[^dont_forget_to_clean_up]: There have been a few times when I've altered my installed Gem and forgotten to clean it up. Usually this means I spend a bit of time re-opening the project and restoring things. A smarter person might wrap the `bundle open` command in initializing a git repository for the gem. Having waited for the close response from the editor, when `bundle open` quits reverting any changes. That may be magical overkill, so for now I'll settle on my error prone human ways.

[^gemfile_lock_variances]: It is still possible that two machines with the same Gemfile.lock may have different dependency graphes. This is because Gemfile's can have imperatives for OS level differences.

[^evaluated_dependency_graph_for_your_machine]: Bundler evaluates each declared gem and its dependency restrictions (i.e. `gem "rails", ">= 4"`, `rspec, "\textasciitilde>1.2"`, etc.).

[^regularly_dash_help]: It would behoove you, as a developer, to on occassion request system help for the scripts you regularly run. Somewhat randomly reading through the output of `bundle -h` in 2013 brought the awesome `bundle console` to my attention. Consider other commands you might use a lot: `rails`, `rake`, `rspec`, `git`, etc. Its software and subject to change. Be aware of those changes and occassionally sharpen your understanding of your tools.

[^if_its_volitale_be_careful]: Within a given gem, if a particular file has lots of churn over time, that is indicative of instability and volatility of the understanding of that file. Perhaps it is a misunderstood object, or an object that encapsulates changing business logic, etc. Regardless, you should be mindful of that. It is a larger liability than a stable file. My conjecture extends this from a file to a gem. If the gem is rapidly incrementing versions, you have a more volitale gem and should consider the ramifications. And yes, I'm guilty of rapidly versioning objects. @CITATION_DESIRED

[^run_a_script_then_commit]: Someone, I don't recall who, recommended that when I run a script that alters the working directory (i.e. `bundle update` or `rails generate model ChickenPie`) that I should 1) make sure the working directory is clean before I run the script. 2) commit the changes made by the script. 3) For the commit message I should record the exact command(s) and options that was run. In following this procedure you are being a good citizen as you introduce code. A generator can create a tremendous amount of code. Keeping the scope of the commit to a single concept is being a good steward of your source control.