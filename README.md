# Git Workflow Introduction

## So what is this repository?

This repository serves as an introduction to the basic `git` workflow that walks through setting up a `git` repository that will be used to create your own `GitHub Pages` website.  While this should provide a good introduction to `git` and its various uses, it is strongly recommended to follow up with the [Pro Git Book](https://git-scm.com/book/en/v2) written by Scott Chacon and Ben Straub from which parts of this guide are derived.  The `git` [reference documentation](https://git-scm.com/docs) is also another great place to find tips, tricks, and other guides to getting the most out of `git`.

## What is `git`?

`git` (not to be confused with `GitHub`) is a distributed version control system that is designed to allow multiple collaborators to share and keep track of project files and versions across all of their computers.  It was originally created in 2005 as a tool to help the Linux kernel development community keep track of changes made through their ever growing non-linear development process.  Though it was originally created for software development it can be used in a variety of different ways for any project that requires versioning of files across multiple people/computers.  Examples of this are standards like [OWASP ASVS](https://github.com/OWASP/ASVS) or proposals such as [Git Law](https://blog.abevoelker.com/gitlaw-github-for-laws-and-legal-documents-a-tourniquet-for-american-liberty/).


## Getting Started

All changes that `git` tracks are stored in a **repository** which acts as a versioned warehouse for all of your project's files.  The following command will initialize a brand new `git` repository inside the current directory.

```bash
$ git init
```

Once this command completes, you have your first `git` repository! You can inspect its current status using the `status` command which is very useful when you get into trouble.  We will be using this one a lot throughout the rest of this guide to show some of the various states that a `git` repository can be in.

```bash
$ git status
```

Below you can see a sample of the output of the `status` command which will show you the `branch` you are on (more on that later), your current `commit` status (also more on that later), and some help text to guide you onto potential next steps.

```
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

If you inspect your local file structure at this point, you will also see that `git` has created a hidden `.git` folder inside of your current directory.

```bash
$ ls -la
total 0
drwxr-xr-x   3 starr  staff   96 Apr 18 18:09 .
drwxr-xr-x  17 starr  staff  544 Apr 18 18:09 ..
drwxr-xr-x   9 starr  staff  288 Apr 18 18:09 .git
```
And if you navigate into that directory, you will see the various files and folders that `git` uses to track changes and maintain its configuration.  If you are curious what these files do, and what they are for most of it is explained in the [Pro Git Book](https://git-scm.com/book/en/v2) mentioned above.

```bash
$ cd .git
$ ls -la
total 24
drwxr-xr-x   9 starr  staff  288 Apr 18 18:09 .
drwxr-xr-x   3 starr  staff   96 Apr 18 18:09 ..
-rw-r--r--   1 starr  staff   23 Apr 18 18:09 HEAD
-rw-r--r--   1 starr  staff  137 Apr 18 18:09 config
-rw-r--r--   1 starr  staff   73 Apr 18 18:09 description
drwxr-xr-x  13 starr  staff  416 Apr 18 18:09 hooks
drwxr-xr-x   3 starr  staff   96 Apr 18 18:09 info
drwxr-xr-x   4 starr  staff  128 Apr 18 18:09 objects
drwxr-xr-x   4 starr  staff  128 Apr 18 18:09 refs
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

```
$ git status
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


