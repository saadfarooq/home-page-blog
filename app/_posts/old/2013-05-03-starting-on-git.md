---
layout: post 
title: "Starting on Git" 
description: "Git tutorial" 
category: development
tags: ['tutorial','development']
---

# Getting started with Git
## Assumptions
- You know what version control is
- You know how to install software on whatever platform you are using
- You know how to set PATH environments etc. if you can't get `git` to respond
  on your command line

## Where we start
Go to your console and do the following

      $ git --version 
      git version 1.7.9

If you don't get that something went wrong and you need to figure out how to
get `git` on your path.

## Initializing your repo
So a `git` repository is basically like a directory that is mirrored somewhere
on a server. To initialize a directory as a `git` repository, do :
    
    $ mkdir test 
    $ cd test 
    $ git init 
    Initialized empty Git repository in /home/Saad/workspace/test/.git/

Notice the `.git` at the end there. That's where all the settings are kept.
Once you are a master guru of this stuff, you might actually end up editing
config files in the directory to change stuff. In the mean time, it is
sufficient to know that this is what defines the repository. If you delete
this, your repo becomes a normal directory again.

## Setting up remotes
Now that you have a local repository, you may want to connect it to a 'remote'
`git` server like [Bitbucket](http://www.bitbucket.org) or
[GitHub](http://www.github.com). These are called your `remotes` and,
understandably, all the manipulation of the remotes is done using the `git
remote` series of commands. Once you make a repo on either Github or
Bitbucket, it will have a URL. This will either be in HTTP form
(*https://...*) or SSH form (*git@github.com:...*). You can look up how to set
up your SSH key on the server if you want to use the SSH form URL. Once you
have this URL, from your local `git` repo do:

    $ git remote add origin ssh://git@bitbucket.org/saadfarooq/test.git

Of course, this should tell you that you can more than one remote to a single
repository. It's convention to call the remote as *origin*. So now your local
repository is connected to the remote repository *origin*. Good work !

## Branches
The other important concept here is branching. Consider that you and your
friend are working on your research project. You friend comes up with this
wonderful idea to so something clever but you don't quit trust it and don't
want him to be messing with your code until you are sure that it works (this
isn't the only possible scenario of course). What do you do ? That's where
branching comes in. Branching allowing you to take pick up on progress at a
particular point and start from that snapshot of code onwards in some other
direction. Of course they can be "merged" later but we'll get to that. All you
really need to know about branching at this point is that when you start a
repo, it is always on branch *master*.

## Staging changes
Now for the real stuff. So the reason we have the version control system is to
save changes. `git` is different from `subversion` in that it has two levels
of staging i.e. you "commit" you changes to the local repository before
"push"ing them to the remote repo. That is a concept you should grasp well.
What this means is that you could have just the local repository and have it
track your changes without connecting it to the remote repo at all. The local
repository is essentially the same as the remote one, thus making up a
"staging" area. So, make a change to your local repository. I just make a new
file on my linux distro. Then check the status of your repository using the
`git status` command.

      $ touch newfile $ git status
      # On branch master
      #
      # Initial commit
      #
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      # newfile nothing added to commit but untracked files present (use "git
        add" to track)

You can see that the file `newfile` shows up in *Untracked files* (also notice
that it is on branch master and it's called the "Initial commit"). This means
that `git` will not look for changes in these files and not care about them.
`git` also tells you how to add them. So :

    $ git add newfile $ git status
    # On branch master
    #
    # Initial commit
    #
    # Changes to be committed:
    #   (use "git rm --cached <file>..." to unstage)
    #
    # new file:   newfile
    #

Now there are not untracked changes and `git` tells you how to unstage the
changes you have made. It also defines what kind of changes it is with the
*"new file:"* tag. This could be *"modified"* if this was not a new file but a
modification. Now to the serious stuff.

## Committing Changes
Committing is the mechanism by which you save some changes to the repo. A
"commit" is essentially a snapshot of the repo at some point in time. You can
use these to revert back to a state that you want to be if, for instance, you
made a mistake somewhere. Commits are identified in `git` by messages and
hashes. We have the one change we can commit. So here goes:

    $ git commit -m "Initial commit" 
    [master (root-commit) a2cdecf] Initalcommit 
    0 files changed create mode 100644 newfile

Notice I use the `-m` argument. This is the commit message (thus the m). If
you don't provide this argument, `git` will open up the default system editor
where you can put in the message. Generally, I find it easier to just type it
out on the console. You must provide a message. `git` aborts the commit if no
message if provided. Now your local repo has a commit, if you want to look at
the history you can use the `git log` command. Now make a change to the file
and see what happens when you do `git status`. Finally, this is all fine but
all this is still on your machine. How can we get this up to the server? That
is where the "push" command comes.

## Pushing commits
So this should be easy now. You have already set up a remote server at
*"origin"*. However, you need to link up your local brances with the remote
server stuff. Simply use the following command:

    $ git push origin master

But, you don't want to be doing that everytime. You can do something like this
for the first commit.

    $ git push -u origin --all

What this does is, it takes all you local brances and maps them to the same
names on the remote `git` server at *"origin"* and also sets the "upstream" of
you local repo to *"origin"*. So all you have to do from now onwards is:

    $ git push 
    Counting objects: 3, done. 
    Writing objects: 100% (3/3), 207 bytes, done. 
    Total 3 (delta 0), reused 0 (delta 0) To ssh://git@bitbucket.org/saadfarooq/test.git
    * [new branch]      master -> master

And it will know the repo and branch to push your commits to.

## Cloning
Cloning is a way to get a copy of a remote repo on to your local machine. The
command is pretty simple and most sites provide you with the entire command
when you go to the repos page.

      $ git clone <repository url>

When you do a clone, it connects all the local and remote branches
automatically. One of the reasons I bring this in late is because that is how
I started with `git` and I find that you don't end up learning enough about
the workings of the system if you do it this way and it therefore takes you
longer to build expertise with the system.

# Coming soon....
We'll look at getting other peoples commits from the remote repo on to your
local machine so we can start using this for collaborating on code instead of
just backing up stuff.
