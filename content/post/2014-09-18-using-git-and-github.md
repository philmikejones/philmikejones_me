---
title: Using Git and Github
date: 2014-09-18
author: philmikejones
categories:
  - Code
---

Git is a powerful way to manage your code. It's main advantage for working with code of any kind are:

- You can commit (or bookmark) your code as you go along. That way, you can easily undo any mistakes you may make.
- You can track your code changes locally on your computer, and upload these changes to a server (like Github) to keep a backup. This is especially useful, for example, if you work without an internet connection on a laptop: you can make and track changes and then upload them when you're back online without fear of losing anything.
- You can collaborate easily on code with others.

Convinced? You should probably set aside about half a day to install and get to grips with git and github for your version controlling. I think it's a worthwhile investment of time, but ultimately it depends on both how frequently you write code, and on its complexity.

## Installation

Probably the most straightforward way to get started is to install the Github GUI for [Windows](https://windows.github.com/ "") or [Mac](https://mac.github.com/ ""). This installs both git (which manages all the underlying code management) and a GUI to make your commits and pushes.

To set up github you need to register with a username and password, and [set up git with your credentials in the terminal or command line](https://help.github.com/articles/set-up-git "").

## Creating or Copying a Repository

Github maintains excellent [manual pages on creating a repository](https://help.github.com/articles/create-a-repo "") if you want to start a new project from scratch.

If you want to work on a repository that someone else has started, for example the [spatial microsimulation in R](https://github.com/Robinlovelace/spatial-microsim-book "") repo, you can copy it (a process called _forking_) and work on your fork. When correctly set up, you can keep your fork up to date with the original (called the _upstream_), and quite easily pass changes back to the original repository once you're satisfied with your work. My previous post on [setting up a fork](http://philmikejones.wordpress.com/2014/09/14/forking-with-github/ "") (using terminal or command line), and [managing your fork](http://philmikejones.wordpress.com/2014/09/15/managing-your-git-fork/ "")  as well as the [github fork manual pages](https://help.github.com/articles/fork-a-repo ""), are a good starting point.

## Tracking Code

There are two stages involved in tracking your code (although this can be condensed in to one process in github if you prefer). When you modify code in a repository, git monitors these changes. At any time you can make a _commit_. This makes a bookmark of your code at this point. You can easily roll back to any commit (or bookmark) at any time, for example if you make a mistake. Again, the [github manpage helps with reviewing and, if necessary, reverting commits](https://help.github.com/articles/viewing-previous-commits "").

Such commits are made locally, on your local computer. This is incredibly useful if you don't have internet connection temporarily. You can then choose when to copy your commits to the server, called _pushing_ (as previously mentioned this can be completed in one step called _commit + sync_ in github; it's really up to you).

## Submitting Code to the Original Project

If your repository is a fork of another project, you can easily submit code back to the original repository. You do this with a _pull request_. Commit your changes as normal and push these to github. Then, from within the github page for your forked project, simply click 'Pull Request.' You will need to provide the original author some information about your updates, and submit. More details are available on my [managing your git fork page](http://philmikejones.wordpress.com/2014/09/15/managing-your-git-fork/ ""), and on the [pull request manual page](https://help.github.com/articles/using-pull-requests "").

## Further Resources

Some good additional resources for gitting (if that's even a verb) are:

- [Gun IO guide to git](https://gun.io/blog/how-to-github-fork-branch-and-pull-request/ "")
- [Pro Git ebook version](http://git-scm.com/book "") and [Pro Git dead-tree version](http://www.amazon.co.uk/Pro-Experts-Voice-Software-Development/dp/1430218339 "")
- [Git documentation](http://git-scm.com/doc "")