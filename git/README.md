# Quick reference guide to Github

  * [Purpose](#1-purpose)
  * [Download and setup](#2-download-and-setup)
      * [Git for Linux](#21-download-and-install-git-for-linux)
      * [Git for OSX](#22-download-and-install-git-for-osx)
      * [Git under Windows](#23-download-and-install-git-under-windows)
  * [Configure username and email](#3-configure-username-and-email)
  * [Create a new repository](#4-create-a-new-repository)
     * [4.1 Create a new repository from scratch](#41-create-a-new-repository-from-scratch)
     * [4.2 Clone a repository from an existing project](#42-clone-a-repository-from-an-existing-project)
  * [Git data transport structure and commands](#5-git-data-transport-structure-and-commands)
  * [Keep your fork up to date](#6-keep-your-fork-up-to-date)
  * [Create a new branch or feature for your work](#7-create-a-new-branch-or-feature-for-your-work)
  * [Make changes and commit them to your local repository](#8-make-changes-and-commit-them-to-your-local-repository)
  * [Pushing changes to your remote repository](#9-pushing-changes-to-your-remote-repository)
  * [Create a pull request to the parent repository](#10-create-a-pull-request-to-the-parent-repository)
  * [Github usage references](#11-github-usage-references)
  * [How to write Github documentation](#12-how-to-write-github-documentation)
  * [gitignore](#13-gitignore)

## Purpose

This document offers an overview of the most important commands of git and it is intended to be a quick start guide to work with git repositories.

## Download and setup

### Download and install Git for Linux

If you are working on a Debian-based version of Linux you can install the basic Git tools via APT:

```bash
sudo apt-get install git-all
```

Here are instructions on how to [install Git under other Linux distributions.](https://git-scm.com/download/linux)

### Download and install Git for OSX

The latest version of Git for Mac can be downloaded [here](https://git-scm.com/download/mac), use this binary installer to get an up-to date version of he software.

If you are installing on a Mac with OS X 10.9 you can install Git from command line with Homebrew (get Homebrew [here](https://brew.sh/)) by typing:

```bash
brew install git
```

## Configure username and email

The first time you are using git from command line you should set up a username and a password. To ease the authentication for each action, go to your local repository and type in the following commands:

```bash
git config user.email "you@example.com"
git config user.name "YourUsername"
```

If you are working locally (your computer only), you could also add the `--global` flag to set these values for all your repositories.


## Create a new repository

There are several ways how one can create a new local repository

### Create a new repository from scratch

Create a directory with the name of the new repository and enter it from the command line. To initialize the repository type:

```bash
git init
```

This command will create a .git subfolder.

### Clone a repository from a project in the clinical-genomics GitHub organisation

```
git clone https://github.com/clinical-genomics/development.git
```

Where the url which can be obtained from the web page of your local fork, by clicking on the "clone or download" green button.
The git clone command then creates a folder with the project and pulls the latest data from your fork in it.

### Clone any other repository

When you are contributing to an existing repository, the first thing you should do is forking this repository to your github space. A fork is basically a copy of the original project, on which you can experiment as much as you want without changing the original project.

[how to fork a repository](https://guides.github.com/activities/forking/)).

Then clone your fork.

```
git clone https://github.com/<your user name>/development.git
```

## Git data transport structure and commands

The following image shows the structure of the git commands and spaces:

![Overview](http://images.osteele.com/2008/git-transport.png)

Your workspace is the folder that holds the actual working files while the "index" is the space is a staging area where you add your changes before committing them to the local repository or "head". To send the changes to your remote repository you use the "push" command.

Here is a link to a page explaining the common Git terminology: [https://help.github.com/articles/github-glossary/](https://help.github.com/articles/github-glossary/)

## 6. Keep your fork up to date

Before committing and pushing changes to your remote repository you should check that you are working on an updated version of it. To update your fork follow these instructions:

First you need to get the latest version of the original project you forked from.
To do so, from command line move to the main folder containing your project and type:

```bash
git remote add upstream path/to/repo/you/forked/from
git fetch upstream
git pull upstream master
git pull upstream develop
# develop is the version you start from for your work!
```

You don't have to call the remote "upstream" but you can chose any name for it. To visualize all remotes you are working with and their respective shortnames use the command:

```bash
git remote -v
```

To remove remotes instead, use the command "git remove rm":

```bash
git remote rm name_of_remote
```

After pulling data from the remote your local copy of the repo should be up-to-date with the upstream. Now you need to update your fork (the copy existing online, in GitHub) accordingly.

If you wish to update you master branch on your fork, for instance, you'd type these commands:

```bash
# be sure to place yourself in your master branch
git checkout master
git rebase upstream/master
git push
```

You use the same commands to update any other branch of your forked repository.

## Create a new branch or feature for your work
To create a new branch, from command line move to the main folder containing your project and type:

<pre>
<b>git checkout -b name_of_your_feature develop</b>
</pre>

If everything went fine than you'll get the following message: "Switched to a new branch name_of_your_feature". This means you are already inside the new feature. To make sure that you are in the right branch type:

<pre>
<b>git branch</b>
</pre>

Whenever you want to move to another branch/feature the command is:

<pre>
<b>git checkout [my-topic]</b>
</pre>

## Make changes and commit them to your local repository

Before committing any changes to your local repository, and finally to the remote repository, make sure you were working on the branch created.
After you are satisfied with your code you can start to commit to the remote repository.

To check that there are actually changes to add and commit, type:

<pre>
<b>git status</b>
</pre>

This command will give you info on the status of your working directory comparing it with the local and remote repositories.

To update the local repository to the latest status, by fetchin and merging remote changes, type:

<pre>
<b>git pull</b>
</pre>

The you can start adding your changes to the index with the command:

<pre>
<b>git add filename_to_send_to_index</b>
</pre>

The process of adding a file to the index is also called staging. Be sure to add all the files you want to include to the index.
Before merging the changes you can preview them with the command:

<pre>
<b>git diff source_branch target_branch</b>
</pre>

Calling the "diff" command without arguments will list all the differences between the index and your workspace, i.e. all the files that you could add to the index.

To commit changes from the index to the local repository (HEAD), type:

<pre>
<b>git commit</b>
</pre>

Alternatively you can add and commit the files to the local repository in only one command:

<pre>
<b>git commit -a</b>
</pre>

NOTE: Be very careful with the above command, since it gives you less control over the single steps of the workflow and the files you really want to commit.
Before using it, make sure everything is under control by using the "git status" and "git diff" commands. Prevent commiting tmp files your editor makes!

To include a description of the commit use the -m flag

<pre>
<b>git commit -m "Example of a commit message"</b>
</pre>

It is possible to close a GitHub issue by referencing it in a commit message or pull request. The issue will be closed when the code is merged to the default branch

<pre>
<b>git commit -m "Fixes #36"</b>
</pre>

For more examples on how to close issues using keywords see this [guide][issue-closing].

## Pushing changes to your remote repository

After "git add" and "git commit", or "commit -a", your changes are in the HEAD of your local repository. To send them to the remote repository use the command "push":

<pre>
<b>git push</b>
</pre>

## Create a pull request to the parent repository

You create a "pull request" when you want to propose the introduction of your changes to the repository where your project was cloned or forked from. Pull requests are created on github on the page of the github repository. By default pull requests are directed to the default branch (master). For a more detailed explanation of pull requests visit the Github help page.

Once the pull request is merged and closed you can safely remove the branch you've been working on.
To remove a generic branch both remotely and locally type:

<pre>
<b>git branch -d name_of_your_branch                #removes it locally</b>
<b>git push origin --delete name_of_your_branch     #removes it remotely</b>
</pre>

It is possible to close a GitHub issue by referencing it in a pull request title or description, e.g. "Fixes #46". The issue will be closed when the code is merged to the default branch. A more in-depth description can be found in this [guide][issue-closing].

## Github usage references

Github short guide: (https://guides.github.com/activities/hello-world/)<br>
Github book:        (https://git-scm.com/book/en/v2)<br>
GitHub help page:   (https://help.github.com/)<br>
Glossary:           (https://help.github.com/articles/github-glossary/)

## How to write Github documentation

**Markdown** is the documentation format of choice for code on GitHub. If you want to live-preview files in the format they will show up before pushing you can use the handy [Grip][grip] tool. It super easy to use! All you need to do is:

<pre>
<b>pip install grip
# cd to your project directory
grip
# open your web-browser at http://localhost:6419</b>
</pre>

## .gitignore

This is a special file that's usually part of every repo. Here you can tell git which files it should exclude from version control. Examples include private files with sensitive data, temporary log files, and large files used for testing.

GitHub hosts a [brief guide][gitignore] about the format. There's also a great resource for finding [templates][gitignore-templates] for every language to use as starting points.

[grip]: https://github.com/joeyespo/grip
[gitignore]: https://help.github.com/articles/ignoring-files/
[gitignore-templates]: https://www.gitignore.io/
[issue-closing]: https://help.github.com/articles/closing-issues-using-keywords/
