---
title: Forking with Github
date: 2014-09-14
author: philmikejones
categories:
  - Code
---

## Why Fork?

I collaborate on a couple of projects with a friend of mine using Github. Generally he creates most of the content but asks me to check or test it before using it in teaching. We've found using forks to be the simplest way to collaborate in this way, because:

- It allows me to create my own copy of his work, so any changes I make to my version don't affect his original (unless we want them to).
- I can always download the most up to date version of his repository so I know I'm always checking the right material.
- I can track my own changes in my local copy of the repository and submit them when I'm ready.

## To Fork a Repository

  1. Make sure you're logged in to your github account.
  2. Browse github to the original repository, in my case I look for my friend's original code.
  3. Press &#8216;Fork' along the top left of the browser screen.
  4. Once the github servers finished the procedure you're presented with your own forked repository (check the breadcrumb trail and it should say &#8216;forked from&#8230;')
  5. Copy the SSH or HTTPS link to your (forked!) repository to your clipboard.
  6. Open terminal and navigate to the folder you want your local copy of your repository to be stored. For example, I place all my local git repositories in gits/local-repo-name
  7. Type git clone and paste your SSH or HTTPS link, so for example: git clone git@github.com:philmikejones/my-forked-repo.git

## Set Upstream

Next you need to tell github where the upstream repository is. The upstream is the original repository owned by your friend or colleague that you forked above. By specifying the upstream location this means you can suggest changes you make to your fork back to the original author, so it's kinda essential.

  1. Navigate to the original repository (click &#8216;forked from&#8230;' at the top of your forked repository).
  2. Copy the SSH or HTTPS link as before.
  3. Back in terminal, make sure you're in the correct folder (i.e. for me it's gits/my-local-forked-repo). To do this you'll probably need to navigate to the folder your fork just created.
  4. Type git remote add upstream and paste the link, so for example: git remote add upstream git@github.com:original-author/upstream-repository.git
  5. If you get an error saying &#8216;fatal: Not a git repository' then you're in the wrong folder in your terminal.
  6. To check this worked type git remote -v. You should have both an origin (your fork) and an upstream (the original).
  7. Finally, type git merge upstream/master so git knows which branches relate to each other across the fork.