# Bundler

> "Bundler maintains a consistent environment for ruby applications.
> It tracks an application's code and the rubygems it needs to run, so that an application will always have the exact gems (and versions) that it needs to run." *[bundler.io](http://bundler.io/)*

## Gemfile

A Gemfile lists the explicit dependencies of a Ruby project.
The Gemfile.lock[^gemfile_lock], if one exists, lists the resolved dependency graph, down to the specific version of each gem in the dependency graph.

If you have a Gemfile but not a Gemfile.lock, running `bundle` in the project's root directory will generate a Gemfile.lock for the project.
The resulting Gemfile.lock is the evaluated dependency graph *for your machine*.[^evaluated_dependency_graph_for_your_machine] If someone else were to run `bundle` against the same Gemfile their resulting Gemfile.lock might vary.

However, once the Gemfile.lock is established, running `bundle` will install effectively the same things[^gemfile_lock_variances].

## Bundle Show

```console
$ bundle help show

Show lists the names and versions of all gems that are required by your Gemfile.
Calling show with [GEM] will list the exact location of that gem on your machine.
```

Of the two options, I more often use `bundle show <name_of_gem>`.[^why_bundle_show]
I more often want to know where a gem was installed than see the list of gems that are referenced.

And I often follow with `bundle open <name_of_gem>`.

## Bundle Open

```console
$ bundle help open

Opens the source directory of the given bundled gem
```

When I want to dig around in the gem's executed code, I run `bundle open <name_of_gem>`.
My text editor pops open and begin the spelunking; All of the gem's code is there to review.[^well_not_all_of_it]

## Bundle Console

I learned about this command in 2013; Its been around longer than that, but I was a little dense in my failure to notice the command[^regularly_dash_help].

`bundle console`

## Bundle Outdated

`bundle outdated`

## Bundle Update

`bundle update`

<!-- footnotes  -->
[^gemfile_lock]: If you are working on your own gem, make sure to not checking in your local Gemfile.lock. [More from Yehuda Katz, creator of Bundler can be found at [http://yehudakatz.com/2010/12/16/clarifying-the-roles-of-the-gemspec-and-gemfile/](http://yehudakatz.com/2010/12/16/clarifying-the-roles-of-the-gemspec-and-gemfile/).

[^why_bundle_show]: When I do use `bundle show <gem_name>` it is almost always followed by `bundle open <gem_name>`. Other times I am verifying the file system location of a gem that was declared with a `:path` or `:github` option (i.e. `gem "orcid", path: "../orcid"` or `gem "mappy", github: "jeremyf/mappy"`).

[^well_not_all_of_it]: Well not all of it. Its possible via the gemspec declaration that not all files were declared. Some people don't include the test or spec directory in their gemspec. Not cool! Personally I expect anything and everything that may be relevant to the workings of the code (and is not generatable) to be included.

[^gemfile_lock_variances]: It is still possible that two machines with the same Gemfile.lock may have different dependency graphes. This is because Gemfile's can have imperatives for OS level differences.

[^evaluated_dependency_graph_for_your_machine]: Bundler evaluates each declared gem and its dependency restrictions (i.e. `gem "rails", ">= 4"`, `rspec, "\textasciitilde>1.2"`, etc.).

[^regularly_dash_help]: It would behoove you, as a developer, to on occassion request system help for the scripts you regularly run. Somewhat randomly reading through the output of `bundle -h` in 2013 brought the awesome `bundle console` to my attention. Consider other commands you might use a lot: `rails`, `rake`, `rspec`, `git`, etc. Its software and subject to change. Be aware of those changes and occassionally sharpen your understanding of your tools.