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

Below you can see a sample of the output of the `status` command which will show you the `branch` you are on (in this case `master`, but more on that later), your current `commit` status (also more on that later), and some help text to guide you onto potential next steps.

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

Commits are the core way that `git` records changes in the repository, and they represent a snapshot of files in time.  Commits are made whenever you reach a state in your project that you would like to record, say if you were working on rewording a document or refactoring some code, but wanted to try a different path without deleting your current progress.  In order to create a commit, we need some changes first so let's run the following command to create an `index.html` file in the current directory.

```bash
$ touch index.html
```

Once this completes we can use the `status` command to see what effect this had on the `git` repository.

```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	index.html

nothing added to commit but untracked files present (use "git add" to track)
```

As you can see we still don't have any commits yet, but `git` has picked up the new `Untracked` file that we created above.  Files can be in one of four states (`Untracked`, `Unmodified`, `Modified`, and `Staged`) depending on where they are in the `git` process, but will always initially be `Untracked` when they are created (more on this in the [Pro Git Book](https://git-scm.com/book/en/v2)).  You can also see that the `status` command is trying to be helpful and is pointing us to the next command we want to run to create a commit, which is `add`.  The `add` command will move any `Untracked` or `Modified` file to the `Staged` state which will tell `git` to stage it to get ready for the next commit.  This allows you to be selective about which files go into each of your commits. The `add` command can be ran using the following command.

```bash
$ git add index.html
```

Once this completes we can again use the `status` command to see what effect this had on the `git` repository.

```bash
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   index.html

```

Now `status` shows that our `index.html` file is `Staged` and is ready to be committed along with showing us the `rm` command which will allow us to unstage the file if we would like. Now that we are ready to commit, we can simply run the following command.

```bash
$ git commit
```

This will open a [`vi`](http://www.lagmonster.org/docs/vi.html) window by default in which you can enter a message to describe your commit (you can bypass this and enter a message from the command line by using the `-m` option).  Git commit messages could be a topic in and of themselves (see [this page](https://chris.beams.io/posts/git-commit/) for things to keep in mind when writing them), but for now you can simply use the message `My first commit`.  Once you save the message you've successfully created your first commit!

**NOTE**: *If this is your absolute first time creating a commit, `git` may have prompted you to enter a global name and email address to associate with your commit so that other collaborators can contact you if they need to.  For this you can simply follow the info that `git` provides in that message and proceed above as normal. You will only be asked to set this once.*

Now if we run the `status` command again, we will see the output for a normal, `Unmodified` `git` repository.

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

And if we want to actually see the commit history we have created thus far, we can use the `log` command.

```bash
$ git log
commit dfbd01f915e535b6936693b43e297236a095f4bb (HEAD -> master)
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 20:15:23 2019 -0700

    My first commit
```

This will show us the unique hash for each commit (which can be used to look up the commit later), as well as the Author, Date, and Commit Message.  It also shows which commit is currently set as the `HEAD` for the current branch.  For this, think of a tape playing through a cassette player.  The head of that cassette can be at any point in the music track and can be rewound, or fast-forwarded to move around through the music.

## Making Changes

Now that we have one commit, let's add some content to our `index.html` page to spice it up a bit.  For this you can use `nano`, `vi`, `emacs` or any text editor of your choosing.

```bash
$ nano index.html
```

Once you have this open, paste the contents of the `index.html` page from this repository to act as a base for your `index.html` page.  When you are done, save it, and run the `status` command.

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```

As you can see , our `index.html` page is now in the `Modified` state.  To stage the file, and commit, simply run the same commands as before.

**NOTE**: *The `.` selects all of the files in the current directory*

```bash
$ git add .
$ git commit
```

From here you can again run the `status` and `log` commands to check in on what `git` did.

```bash
$ git status
On branch master
nothing to commit, working tree clean
$ git log
commit 4ad7c47199abb9df0613a16828a0cdae0560628a (HEAD -> master)
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 21:05:51 2019 -0700

    Adds content to index.html page

commit dfbd01f915e535b6936693b43e297236a095f4bb
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 20:15:23 2019 -0700

    My first commit
```

As you can see you now have a second commit on top of your previous commit which has become our new `HEAD` as well as now being at the new top of `master`.  New commits will always automatically advance the `HEAD`, but let's say we wanted to get back to our previous, blank `index.html` page.  In order to do this, we will use the `checkout` command followed by your first commit's hash.

```bash
$ git checkout dfbd01f915e535b6936693b43e297236a095f4bb
Note: checking out 'dfbd01f915e535b6936693b43e297236a095f4bb'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at dfbd01f My first commit
```

From the above, you can see that `git` is warning us about the state we are in because if we make changes at this point we will likely lose our changes (unless we create a branch off of this commit as described in the message, and as expanded on later on).  If we were to run `status` and `log` at this point we would see some warnings about our `HEAD` being detached, and see that we are actually no longer on a defined branch.

```bash
$ git status
HEAD detached at dfbd01f
nothing to commit, working tree clean
$ git log
commit dfbd01f915e535b6936693b43e297236a095f4bb (HEAD)
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 20:15:23 2019 -0700

    My first commit
```

In order to get out of this state after looking around, we can simply run the `checkout` command, but specify our branch `master` instead of a `git` hash.


```bash
$ git checkout master
Previous HEAD position was dfbd01f My first commit
Switched to branch 'master'
```

## Branching Out



## Using Remotes

```bash
$ git remote add origin <your-git-repo-url>
```

```bash
$ git push -u origin master
```
