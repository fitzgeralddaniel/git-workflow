# Git Workflow Introduction

## So what is this repository?

This repository serves as an introduction to the basic `git` workflow that walks through setting up a `git` repository that will be used to create your own `GitHub Pages` website.  While this should provide a good introduction to `git` and its various uses, it is strongly recommended to follow up with the [Pro Git Book](https://git-scm.com/book/en/v2) written by Scott Chacon and Ben Straub from which parts of this guide are derived.  The [`git` reference documentation](https://git-scm.com/docs) is also another great place to find tips, tricks, and other guides to getting the most out of `git`.

## What is `git`?

`git` (not to be confused with `GitHub`) is a distributed version control system that is designed to allow multiple collaborators to share and keep track of project files and versions across all of their computers.  It was originally created in 2005 as a tool to help the Linux kernel development community keep track of changes made through their ever growing non-linear development process.

## Getting Started



```bash
$ git init
```

```bash
$ git status
```

```bash
$ ls -la
```

```bash
$ cd .git
```

## First Commit

```bash
$ touch index.html
```

```
$ git status
```

```bash
$ git add index.html
```

```bash
$ git commit
```

## Making Changes

```
$ nano index.html
```

```
$ git status
```

```bash
$ git add .
$ git commit
```

## Using Remotes

```bash
$ git remote add origin <your-git-repo-url>
```

```bash
$ git push -u origin master
```

## Branching Out


