---
title: Managing your Git Fork
date: 2014-09-15
author: philmikejones
categories:
  - Code
---

In the post [forking with github](../2014-09-14-forking-with-github/) I described how to fork a repository and have it point back to the original. In this post I describe how I manage my fork and ultimately how I suggest changes to the original author that they may (or may not) make in their original.

## Tracking Changes in Your Forked Version

Your fork behaves like a normal repository, so you can make changes to your code as often as you like, commit changes, and then push these commits to the server version of your repository.

What it took me a long way to realise, and revolutionised how I use git(hub), is that the changes are tracked _locally_ on your machine unless you choose to push them back to the server. This means you can commit as many changes as you like, and only push when you're satisfied.

So, before I begin working on my fork I make sure it's up to date with its upstream (that is the repository I originally forked). Do this by:

  1. Opening terminal (command line if you're on Windows)
  2. Navigate to the folder where your git repository is.
  3. Type: git fetch upstream

Now you can make as many changes as you like to your local version. When you're ready to commit a change (remember, this is only locally at this point) go back to your terminal and type:

<pre class="brush: bash; title: ; notranslate" title="">git status</pre>

This will highlight any files that you've changed or modified. Check this list carefully. If there are any files you don't want to commit (and ultimately push to the remote server) you can tell git to ignore them by adding them to .gitignore. Open this with a text editor like TextEdit or Notepad (not Word or LibreOffice!) and add one file per line. Type git status again in terminal to check the .gitignore worked.

Once you're happy with the files you want to commit, and everything else is safely ignored, you can complete the commit. Do this by typing:

<pre class="brush: bash; title: ; notranslate" title="">git commit -a</pre>

This adds all listed modified files to the commit and allows you to type a git commit message. This message is mandatory, although not everyone follows good practice by typing a descriptive change message, see [Git Commit](http://xkcd.com/1296/). In Mac, this opens Vim by default, so start typing your commit message.

- Once you've entered your (descriptive) git commit message, press Esc. This leaves insert mode.
- Type `:x` to save and exit.
- You'll be returned to the terminal and a confirmation message will say your commit was successful.

Remember this commits are local, and are not reflected on the server version of your repository. You can make as many commits as you like, but one you're ready to update your server repository you need to use push.

## Updating the Server to Reflect Local Changes

At this point you've made local changes to your repository that you've tracked with one or more commits. You now want to push these to your server so you have a backup and this reflects the most recent changes.

The command to do this is push. Back in your terminal, type:

<pre class="brush: bash; title: ; notranslate" title="">git push</pre>

That really is it. As of September 2014 git reminds you that there will be a change in the default push behaviour, but you can ignore this or choose a default behaviour. That's it, the last line should give you a hash of the changes and tell you which branch was updated (probably master -> master). You can check to see if the changes are online if you like.
