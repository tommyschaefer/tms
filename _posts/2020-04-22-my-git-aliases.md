---
layout: post
title: My Git aliases
link: https://labs.teecom.com/2020/04/22/git-aliases.html
originally_posted_on: TEECOMlabs blog
---

I recently read a [blog post](https://www.codewithjason.com/my-git-aliases/) by
Jason Swett where he shared some of his Git aliases, and I was inspired to do
the same!

In my `~/.zshrc` file, I alias `git` to `g`:

```
alias g=hub
```

In my `~/.gitconfig` file, I have a number of aliases defined:

```
[alias]
  ; shortcuts
  l = log --pretty=oneline
  c = commit -v
  s = status
  a = add
  p = push
  co = checkout
  cob = checkout -b
  cp = cherry-pick
  fp = push --force-with-lease
  dc = diff-commits

  ; helpers
  branches = for-each-ref --sort=-committerdate --format=\"%(color:blue)%(authordate:relative)\t%(color:red)%(authorname)\t%(color:white)%(color:bold)%(refname:short)\" refs/remotes
  branch-name = !git rev-parse --abbrev-ref HEAD
  diff-commits = cherry -v

  ; workflows
  pub = !git push -u origin $(git branch-name)
  ppr = !git pub && gh pr create
  up = !git fetch origin && git rebase origin/$DEFAULT_BRANCH
  ir = !git rebase -i origin/$DEFAULT_BRANCH
  cleanup = !git remote prune origin && git gc && git clean -dfx && git stash clear
```

I find these aliases really handy, especially for two of my most common
workflows.

#### Opening a pull-request for a new feature

```
$ g cob new-feature
... do some work ...
$ g c
... do some work ...
$ g c
$ g ppr
```

#### Preparing a branch for final review

```
$ g up
$ g ir
... squash commits ...
$ g fp
```
