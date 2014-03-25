# Git

One of the best tooling changes that I've experienced was transitioning from centralized version control to distributed version control.

At first it was the change to a tool that allowed fast branching and merging - a mandatory killer feature.
Now it is the collaborative nature of the tool.

\begin{aside}
\heading{I Merged Branches in SVN Once. Once!}
\label{aside:merged_in_svn_once}

Back in the early days of my Rails projects, I was working on a project managed in SVN.
I was working on an extended feature and decided to create a branch.
Work proceeded both branches.

Then came the reckoning.

We attempted to merge the code.
And everything fell apart.

We ended up spending 8 hours merging things.
And I don't think we got things right.
That day we decided we needed to move to git.

Did I mention we didn't have automated tests?
\end{aside}


## Bash Completion

I recommend that you enable `git`'s tab completion.
Git has a large suite of commands.
I've stumbled upon a few unknown commands and options as I've tabbed on the command line.

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

In your `\textasciitilde/.profile` add the following. *Or make use of my dotfiles repository~\ref{sec:my_dotfiles_repository}*.

```console
if [ -f /path/to/your/git-completion.bash ]; then
  source /path/to/your/git-completion.bash;
fi
```

Find out more about [Git's bash completion](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash).

## Command Line Status
\label{cha:command_line}

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

* \* - My repository is in a "dirty state".
* \$ - I have "stashed" something.
* \= - My branch is up-to-date with 'origin/master'.

*For more information you can review [git's bash completion script](https://github.com/git/git/blob/master/contrib/completion/git-prompt.sh).*

```console
2.0.0-p353
```

Display the current Ruby version. *This was particularly helpful a few years ago when I had a mix of 1.8.x projects and 1.9.x projects.*

\begin{aside}
\heading{My PS1 Script}
\label{aside:custom_ps1_with_git}

This is a recent change to my PS1 script.
I had different information, but I opted to instead use a community maintained set of scripts.

Working on lots of projects in various Ruby versions, I find this PS1 information vital.
In fact, when I look at other people's PS1 and don't see git information, I am left wondering how they have room in their head to keep track of that information.

<<(/Users/jfriesen/Repositories/dotfiles/system/ps1.bash, lang: sh)
\end{aside}

## Branching

## Bisect
