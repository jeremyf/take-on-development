# Git

One of the best tooling changes that I've experienced was transitioning from centralized version control to distributed version control.

At first it was the change to a tool that allowed fast branching and merging - a mandatory killer feature.
Now it is the collaborative nature of the tool.

\begin{aside}
\label{aside:merged_in_svn_once}
\heading{I Merged Branches in SVN Once. Once.}

Back in the early days of my Rails projects, I was working on a project managed in SVN.
I was working on an extended feature and decided to create a branch.
Work proceeded on both branches.

Then came the reckoning.

We attempted to merge the code.
And everything fell apart.

We ended up spending 8 hours merging things.
And I don't think we got it right.
That day we decided we needed to move to git.

Did I mention we had minimal automated tests?

\end{aside}

## Bash Completion

I recommend that you enable `git`'s tab completion.
Git has a large suite of commands.
With tab completion installed, I've stumbled upon a few unknown commands and options.

Either the command:

```console
$ git che<tab>

checkout      cherry        cherry-pick
```

Or the command's options:

```console
$ git checkout --<tab>

--conflict=  --merge      --no-track   --orphan     --ours
--patch      --quiet      --theirs     --track
```

In your `\textasciitilde/.profile` add the following. *Or make use of my dotfiles repository~\ref{sec:my_dotfiles_repository}.*

```sh
if [ -f /path/to/your/git-completion.bash ]; then
  source /path/to/your/git-completion.bash;
fi
```

Find out more about [Git's bash completion](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash).

## Command Line Status

```console
~/Repositories/take_on_rails (master *=) 2.0.0-p353 $
```

First is the path to the current directory (i.e. `pwd`).

```console
~/Repositories/project
```

Then, if I am in a directory that is part of a Git project, the command prompt
includes the current branch and repository status information.

```console
(master *=$)
```

| Output | What is going on?
|--------|-----------------------------------------------
| `*`   | My repository is in a "dirty state".
| `$`   | I have "stashed" something.
| `=`   | My branch is up-to-date with 'origin/master'.
| `<`   | My branch is behind 'origin/master'.
| `>`   | My branch is ahead of 'origin/master'.
| `<>`  | My branch is ahead of 'origin/master'.

I enabled these indicators by setting the following in my `\textasciitilde/.profile`:

```console
GIT_PS1_SHOWDIRTYSTATE=true
GIT_PS1_SHOWSTASHSTATE=true
GIT_PS1_SHOWUNTRACKEDFILES=true
GIT_PS1_SHOWUPSTREAM="auto"
```

*For more information you can review [git's bash completion script](https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh).*

```console
2.0.0-p353
```

Display the current Ruby version. *This was more helpful a few years ago when I had a mix of 1.8.x projects and 1.9.x projects.*

\begin{aside}
\label{aside:custom_ps_with_git}
\heading{About My PS1}

Below is a recent change to my PS1 script.
I had different information, but I opted to instead use a community maintained set of scripts.

Working on lots of projects in various Ruby versions, I find this PS1 information vital.
In fact, when I look at other people's PS1 and don't see git information, I am left wondering how they have room in their head to keep track of that information.

\end{aside}

<<(/Users/jfriesen/Repositories/dotfiles/system/ps1.bash, lang: sh)

## Git Config

I make extensive use of git aliases, to help encapsulate common behavior for my workflow.
In my `~/.gitconfig` I've added a several aliases. And when using Bash Completion, these alias will also tab complete. Here are a few of them:

### Show Very Verbose Branch Details

Compare the three examples:

Local branches with little information:

```console
$ git branch
* chore-verify-isolation-tests
  master
```

Local branches only but with tracking information:

```console
$ git branch -vv
* chore                   402150b [jeremyf/chore: ahead 1] Adding documentation
  master                  a7dda4a [origin/master] Merge pull request #1 from jeremyf/dltp-123
```

All branches with tracking information:

```console
$ git branch -avv
* chore                   402150b [jeremyf/chore: ahead 1] Adding documentation
  master                  a7dda4a [origin/master] Merge pull request #1 from jeremyf/dltp-123
  remotes/jeremyf/chore   402150b Verifying specs run in isolation
  remotes/jeremyf/master  4cef983 Updating README with badges [skip ci]
  remotes/origin/master   a7dda4a Merge pull request #1 from jeremyf/dltp-123
```

At a glance, `git branch -avv` gives me the best perspective of what is happening.

I use `git branch -avv` all of the time, and went ahead and made `git ba` an alias.
To do this, I added the following to my `.gitconfig`:

```console
[alias]
        ba = branch -a -vv
```

@TODO

## Bisect

From `git-bisect`'s [man page](https://www.kernel.org/pub/software/scm/git/docs/git-bisect.html).

> git-bisect – Find by binary search the change that introduced a bug

This is one of many killer features for `git`.

*This is updated from a [previous blog post](http://blogs.nd.edu/jeremyfriesen/2012/10/08/using-git-bisect-for-finding-when-a-bug-was-introduced/).*

### Prepare Your Bisect

```console
$ git bisect start
$ git bisect bad
$ git bisect good 3f5ee0d32dd2a13c9274655de825d31c6a12313f
```

* Tell git we are starting a bisect.
* Then tell git at what point we found the bug - in this case HEAD.
* And finally tell git at what point we were bug free – in this case at commit 3f5ee0d32dd2a13c9274655de825d31c6a12313f.

### Run Your Test

We've told git-bisect the good and bad commits.

```console
$ git bisect run ./path/to/test-script
```

And now we step through history and run `./path/to/test-script`.

What is `./path/to/test-script`?
It is any executable file that exits with a 0 status (i.e. success) or a non-0 status (i.e. failure).
[Learn more about git-bisect run](https://www.kernel.org/pub/software/scm/git/docs/git-bisect.html#_bisect_run).

If `./path/to/test-script` is successful, the current commit is good.
Otherwise it is bad.
Git-bisect will converge on the commit that introduced the bad result and report the bad commit log entry.

### Script Use Cases

What is this `./path/to/test-script`?

I've used `rake` for my Rails project.
But that was overkill - my `rake` test suite was very slow.

I've also ran bisect on a test file in the repository (i.e. `ruby ./test/unit/page_test.rb`).
In these cases the test was in my the repository.
This meant the test was subject to changes over the commit time range.

I have found using a script not in the repository to be the best option.
I can answer the very specific question by using a custom script.

This was useful when my manager asked “When did this strange behavior get introduced?”

I wrote a Capybara test that automated the steps my manager reported.
Reproducing the error and creating an assertion of the expected behavior.

A few weeks prior, I had introduced the odd behavior as a side-effect.
At the time I didn't have test coverage for that particular behavior.

I patched the error, answered my managers question, and had an automated test that I could drop into my repository to make sure I didn't reintroduce that behavior.

## When to Commit

I like to commit early and often.
One trick I've used is to create a feature branch then make numerous commits, often times with terse messages.
By doing this I have an excellent "undo" buffer.

Once I'm ready to share these changes, I will use an interactive rebase to amend the commit messages.
This way I can focus on two distinct modes of concentration:

* Writing supporting specs and code
* Writing commit messages

For me, the mental state for those two modes is different.
So I use the rebase trick to force my brain into writing more details concerning any of the changes.
This may mean that two or more commits are squashed together as they might make sense together.

## Git Immersion

@TODO - go through gitimmersion to speak authoritively

> "Git immersion is a guided tour that walks through the fundamentals of git, inspired by the premise that to know a thing is to do it." - *[gitimmersion.com](http://gitimmersion.com/)*