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

**NOTE:** *If this is your absolute first time creating a commit, `git` may have prompted you to enter a global name and email address to associate with your commit so that other collaborators can contact you if they need to.  For this you can simply follow the info that `git` provides in that message and proceed above as normal. You will only be asked to set this once.*

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

This will show us the unique hash for each commit (which can be used to look up the commit later), as well as the Author, Date, and Commit Message.  It also shows which commit is currently set as the local `HEAD`.  For this, think of a tape playing through a cassette player.  The head of that cassette can be at any point in the music track and can be rewound, or fast-forwarded to move around through the music.

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

**NOTE:** *The `.` selects all of the files in the current directory*

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

Branches in `git` can be thought of in many ways as branches of a tree, they can both `branch` out from one another, as well as `merge` back together again.  Another way to think of them is as named commits, and since every commit builds off of the previous commits they retain those commits in that branch's `log`.  Git commits can also exist across branches and in each other's history, again since every commit builds off of those prior. Git repositories can have thousands of branches with thousands of parallel tracks of work all existing simultaneously.  If you wanted to list the branches in a repository you can run the following command.

```bash
git branch
* master
```

As you can see we only have one branch, which happens to be the default `master` branch. Normally this branch is treated as a special branch that contains the canonical source of whatever you are creating, and normally you would not want to push breaking or draft changes directly to the `master` branch.

If you went ahead and took a look at our index.html page, you might notice that it looks slightly bland, but it is functional for the most part.  Let's add some styling to it, but create a branch so as to avoid making breaking changes to our page as we modify and commit changes to it.  In order to create a new branch, you can run the following command:

```bash
$ git branch css-test
```

Now you have a `css-test` branch (you can see it with `git branch`), but have not checked it out yet.  In order to do this, run the `checkout` command for the new `css-test` branch as you did with `master` before.

**NOTE:** *A shortcut to both create a branch and check it out is to use the `-b` switch on the checkout command as in `git checkout -b css-test`*

```bash
$ git checkout css-test
Switched to branch 'css-test'
```

Now if we run the `status` command, we will see that we are on the `css-test` branch.

```bash
$ git status
On branch css-test
nothing to commit, working tree clean
```

Now that we are on the right branch, we can bring over the `cover.css` file from this repository into yours as we did with the `index.html` file earlier.  Feel free to edit the file as you like, and then run the following commands to stage and commit the file:

```bash
$ git add .
$ git commit
```

If we were to run the `log` command at this point, we would see that our new commit is at the top of our `css-test` branch, and that our `HEAD` is set to the same, but that our `master` branch is now behind by one commit.


```bash
$ git log
commit 44066ba020e78edcaa8e740db0692ada548e5ab6 (HEAD -> css-test)
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 21:50:19 2019 -0700

    Adds styling to the cover page

commit 4ad7c47199abb9df0613a16828a0cdae0560628a (master)
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 21:05:51 2019 -0700

    Adds content to index.html page

commit dfbd01f915e535b6936693b43e297236a095f4bb
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 20:15:23 2019 -0700

    My first commit
```

Once we are done with our changes, we will need to `merge` our `css-test` branch back into `master` in order to bring it up to speed.  To do this, we will need to `checkout` the `master` branch again, and use the `merge` command to bring in the changes from our `css-test` branch.

```bash
$ git checkout master
Switched to branch 'master'
$ git merge css-test
Updating 4ad7c47..44066ba
Fast-forward
 cover.css | 110 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 1 file changed, 110 insertions(+)
 create mode 100644 cover.css
```

As you can see, `git` fast-forwarded our changes from `css-test` onto the `master`branch. It was able to do this without any user interaction because the changes on each branch did not conflict, and `git` was able to figure out how to splice the changes together on its own, if this was not the case, `git` would show a merge conflict which will be explained in the next section.  If we run `log` at this point, we will see that `master` and `css-test` are set to the same commit.

```bash
$ git log
commit 44066ba020e78edcaa8e740db0692ada548e5ab6 (HEAD -> master, css-test)
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 21:50:19 2019 -0700

    Adds styling to the cover page

commit 4ad7c47199abb9df0613a16828a0cdae0560628a
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 21:05:51 2019 -0700

    Adds content to index.html page

commit dfbd01f915e535b6936693b43e297236a095f4bb
Author: Your Name <youremail@emailland.com>
Date:   Thu Apr 18 20:15:23 2019 -0700

    My first commit
```

## Merge Conflicts

Merge conflicts arise when two branches are merged together that have changes that cover the same file(s) and line number(s).  Let's create a merge conflict so that we can resolve it and get back into a good state.  First we'll create a new branch to change the top nav bar to show our name instead of the generic `Cover`.

```bash
$ git checkout -b name-test
```

Once on the new branch, change the `index.html` page on line `27` to use your name instead of `Cover`.  Once you save the file, you can stage and commit to the `name-test` branch.


```bash
$ git add .
$ git commit
```

After that, let's checkout `master` again so we can edit the same line in the same file on a different branch.

```bash
$ git checkout master
```

Now edit your `index.html` page on line `27` to be something different than `Cover`, and different from the name you put in before.

**NOTE:** *`git` can be smart sometimes if the exact same change is made in the exact same way, so make sure it is different than before.*

Once saved, stage and commit the file as before.

```bash
$ git add .
$ git commit
```

**NOTE:** *If we run the `log` command at this point we will see that our `name-test` commit is not visible because it is not part of the history of `master`*

We are now ready to create our merge conflict.  Since we are already on the `master` branch, run the following command to `merge` `name-test` into `master`:

```bash
$ git merge name-test
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

Oh no, a merge conflict! If we run the `status` command now, we will see what we would expect, that both branches edited the `index.html` page as well as some helpful tips to get out of the current state that we are in.

```bash
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

	both modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
```


And if we look at our `index.html` file, we will see that `git` has helpfully segmented the changes for our review so that we can manually merge the two changes together.

```html
<div class="inner">
<<<<<<< HEAD
<h3 class="masthead-brand">My Dog</h3>
=======
<h3 class="masthead-brand">Your Name</h3>
>>>>>>> name-test
<nav class="nav nav-masthead justify-content-center">
```

In this case, we can simply delete the `<<<<<<< HEAD`, `=======`, and `>>>>>>> name-test` lines and choose which `<h3>` tag to accept, either the one from our current `HEAD` or from the `name-test` branch.  Once these edits are made, we can save the file, but aren't out of the woods yet.  In order to fully resolve the conflicts and finalize our changes, we need to stage and commit the `index.html` file to the current branch.

```bash
$ git add .
$ git commit
```

Once this is done, we can run `status` again, and see that we are on a clean `master` branch again.

```bash
$ git status
On branch master
nothing to commit, working tree clean
```

## Using Remotes

**NOTE:** *From here on out, this guide assumes that you have a GitHub account. GitLab, and other git remote hosts provide similar features but differ in their implementation.*

Now that you have learned the basics of using `git` locally, it's time to add a `remote` to your project.  A `remote` is simply a named server that you `push` your commits to so that others can `pull` them back down.  For this we will create a GitHub repository by creating a GitHub account, and selecting the `+` button in the top right, then `New Repository`, and filling out the form with the information it requests.  Once this is done, we can copy the remote's `.git` URL and proceed with adding a remote on the command line.

To add a remote for your GitHub repository named `origin` (the default name for most single-remote `git` projects), run the following command:

**NOTE:** *For simplicities sake it may be easier to use an `https` remote URL instead of an `ssh` URL.  If you are unfamiliar with creating SSH keys, I would recommend using the `https` version.*

```bash
$ git remote add origin <your-git-remote-url>
```

Once this is done, you simply need to use the `push` command to push your local commits to the remote.

```bash
$ git push -u origin master
Enumerating objects: 16, done.
Counting objects: 100% (16/16), done.
Delta compression using up to 8 threads
Compressing objects: 100% (13/13), done.
Writing objects: 100% (16/16), 3.22 KiB | 3.22 MiB/s, done.
Total 16 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), done.
To github.com:<your-username>/<your-repo>
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

**NOTE:** *The -u in the command sets up the remote to use for a given branch.  Any new branches will use the `origin` remote by default, and after running this command `master` now will as well.  Because of this, from here on out you can simply use the `git push` command without any switches.*

One of the great things about remotes is that changes can be made on other machines or by other people and be synced to your local machine.  To test this out let's add a `README.md` file through the GitHub page for your repository by clicking the "Create new file" button and naming the file `README.md`. Place whatever text you want in the file, and when you have committed that from the web UI, run the following command to pull it down to your local machine:

```bash
$ git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:<your-username>/<your-repo>
   b28e0de..422c12a  master     -> origin/master
Updating b28e0de..422c12a
Fast-forward
 README | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README
```

Once this runs, you should be able to see the file you created populate in your local filesystem.

## GitHub Pages

Other great thing about remote's are the custom extensions that they have built around the `git` infrastructure, such as issue tracking, collaboration management, and even website hosting.  GitHub supports a feature called `GitHub Pages` that we can use to get the website we have been building hosted on GitHub.  To enable GitHub pages, go to your project's settings in GitHub, scroll to the GitHub Pages section, and set the Source to your `master` branch.

Once that's done, your site is published!  From here feel free to edit the site as you wish, and customize it to make it your own, all within your newfound `git` workflow!  You can also add collaborators to your site if you wish, and they canget an exactcopy of the repository on their devices using the `clone` command:

```bash
$ git clone <your-git-remote-url>
```

This will create a new folder with the same name as your `git` repository for them to collaborate with you on!
