# Quick reference guide to Github

  * [1. Purpose](#1-purpose)
  * [2. Download and setup](#2-download-and-setup)
    + [2.1 Download and install Git for Linux.](#21-download-and-install-git-for-linux)
    + [2.2 Download and install Git for OSX.](#22-download-and-install-git-for-osx)
    + [2.3 Download and install Git under Windows.](#23-download-and-install-git-under-windows)
  * [3. Configure username and email.](#3-configure-username-and-email)
  * [4. Create a new repository.](#4-create-a-new-repository)
    + [4.1 Create a new repository from scratch.](#41-create-a-new-repository-from-scratch)
    + [4.2 Clone a repository from an existing project.](#42-clone-a-repository-from-an-existing-project)
  * [5. Git data transport structure and commands.](#5-git-data-transport-structure-and-commands)
  * [6. Keep your fork up to date.](#6-keep-your-fork-up-to-date)
  * [7. Create a new branch/feature for your work.](#7-create-a-new-branch-feature-for-your-work)
  * [8. Make changes and commit them to your local repository.](#8-make-changes-and-commit-them-to-your-local-repository)
  * [9. Pushing changes to your remote repository.](#9-pushing-changes-to-your-remote-repository)
  * [10. Create a pull request to the parent repository.](#10-create-a-pull-request-to-the-parent-repository)
  * [11. Github usage references](#11-github-usage-references)
  * [12. How to write Github documentation](#12-how-to-write-github-documentation)


## 1. Purpose
This document offers an overview of the most important commands of Github and it is intended to be a quick start guide to work with Github repositories.


## 2. Download and setup

### 2.1 Download and install Git for Linux.

If you are working on a Debian-based version of Linux you can install the basic Git tools via APT:

<pre>
<b>$ sudo apt-get install git-all</b>
</pre>

Here are instructions on how to [install Git under other Linux distributions.](https://git-scm.com/download/linux)

### 2.2 Download and install Git for OSX.

The latest version of Git for Mac can be downloaded [here](https://git-scm.com/download/mac), use this binary installer to get an up-to date version of he software.

If you are installing on a Mac with OS X 10.9 you can install Git from command line with Homebrew (get Homebrew [here](https://brew.sh/)) by typing:

<pre>
<b>brew install git
brew install git-flow</b>
</pre>

### 2.3 Download and install Git under Windows.

You can download an installer of Git for Windows from [here](https://git-scm.com/download/win) or one of the dedicated projects like this or [this](https://desktop.github.com/). 



## 3. Configure username and email.

The first time you are using git from command line you should set up a username and a password. Type in the following commands:

<pre>
<b>git config --global user.email "you@example.com"
git config --global user.name "YourUsername"</b>
</pre>

## 4. Create a new repository.

### 4.1 Create a new repository from scratch.
Create a directory with the name of the new repository and enter it from command line. To initialize the repository type:



<pre>
<b>git init</b>
</pre>


This command will create a .git subfolder containing all the necessary files for your project.

### 4.2 Clone a repository from an existing project.
When you are contributing to an existing repository, the first thing you should do is forking this repository to your space. A fork is basically a copy of the original project, on which you can experiment as much as you want without changing the original project.
After forking a repository from the internet ([how to fork a repository](https://guides.github.com/activities/forking/)) you can create a local copy of it from command line, by moving in the parent folder of your new repository, then typing:

<pre>
<b>git clone username@host:/path/to/repository</b>
</pre>

Where username@host:/path/to/repository is the url which can be obtained from the web page of your local fork, by clicking on the "clone or download" green button.
The git clone command then creates a folder with the project and pulls the latest data from your fork in it.

<pre>
  For instance, to clone this repository from your fork:
  git clone https://github.com/YourUsername/development.git
</pre>


## 5. Git data transport structure and commands.
The following image shows the structure of the git commands and spaces:

<p align="center">
  <img src="http://i.stack.imgur.com/MgaV9.png">
</p>
Your workspace is the folder that holds the actual working files while the "index" is the space is a staging area where you add your changes before committing them to the local repository or "head". To send the changes to your remote repository you use the "push" command.

Here is a link to a page explaining the common Git terminology: [https://help.github.com/articles/github-glossary/](https://help.github.com/articles/github-glossary/)

## 6. Keep your fork up to date.
Before committing and pushing changes to your remote repository you should check that you are working on an updated version of it. To update your fork follow these instructions:

First you need to get the latest version of the original project you forked from.
To do so, from command line move to the main folder containing your project and type:

<pre>
<b>git remote add upstream path/to/repo/you/forked/from
git fetch upstream
git pull upstream master
git pull upstream develop (develop it's the version you start from for your work!)</b>
</pre>

You don't have to call the remote "upstream" but you can chose any name for it. To visualize all remotes you are working with and their respective shortnames use the command:

<pre>
<b>git remote -v</b>
</pre>
   

To remove remotes instead, use the command "git remove rm":

<pre>
<b>git remote rm name_of_remote</b>
</pre>

After pulling data from the remote your local copy of the repo should be up-to-date with the upstream. Now you need to update your fork (the copy existing online, in GitHub) accordingly.

If you wish to update you master branch on your fork, sor instance, you'd type these commands:

<pre>
<b>git checkout master</b>		#be sure to place yourself in your master branch
<b>git rebase upstream/master
git push</b>
</pre>

You use the same commands to update any other branch of your forked repository.


## 7. Create a new branch/feature for your work.
To create a new branch, from command line move to the main folder containing your project and type:

<pre>
<b>git branch -b name_of_the_new_branch</b>
</pre>

To create a new feature instead, type:

<pre>
<b>git flow init
git flow feature start name_of_your_feature</b>
</pre>

If everything went fine than you'll get the following message: "Switched to a new branch Feature/NameOfYourFeature". This means you are already inside the new feature. To make sure that you are in the right branch type:

<pre>
<b>git branch</b>
</pre>

Whenever you want to move to another branch/feature the command is:


<pre>
<b>git checkout -b [my-topic]</b>
</pre>

## 8. Make changes and commit them to your local repository.
Before committing any changes to your local repository, and finally to the remote repository, make sure you were working on a feature created from an updated version of the develop branch (see point 6: Keep your fork up to date).
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
<b>git add fileName_to_send_to_index</b>
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
<b>git commit -a</b>*
</pre>

\* Be very careful with the above command, since it gives you less control over the single steps of the workflow and the files you really want to commit.
Before using it, make sure everything is under control by using the "git status" and "git diff" commands.


## 9. Pushing changes to your remote repository.
After "git add" and "git commit", or "commit -a", your changes are in the HEAD of your local repository. To send them to the remote repository use the command "push":

<pre>
<b>git push origin (or branch_you_want_to_push_to)</b>**
</pre>

\** If your remote, called origin, is configured and you're committing to master, you can omit the word "origin" and just type "git push".


## 10. Create a pull request to the parent repository.
You create a "pull request" when you want to propose the introduction of your changes to the repository where your project was forked from. Pull requests are created from the webpage of your remote repository. By default pull requests are directed to the default branch of the parent repository, so make sure to use properly the drop-down menu on the webpage to pull changes to the develop branch and not the master branch of the parent repository. For a more detailed explanation of pull requests visit the Github help page.

Once the pull request is merged and closed you can safely remove the branch you've been working on.
If you have been implementing a feature use this syntax:

<pre>
<b>git flow feature finish name_of_your_feature</b>
</pre>

Otherwise to remove a generic branch both remotely and locally type:

<pre>
<b>git branch -d name_of_your_branch                #removes it locally
git push origin --delete name_of_your_branch     #removes it remotely</b>
</pre>


## 11. Github usage references
Github short guide: (https://guides.github.com/activities/hello-world/)<br>
Github book:        (https://git-scm.com/book/en/v2)<br>
GitHub help page:   (https://help.github.com/)<br>
Glossary:           (https://help.github.com/articles/github-glossary/)



## 12. How to write Github documentation

**Markdown** is the documentation format of choice for code on GitHub. If you want to live-preview files in the format they will show up before pushing you can use the handy [Grip][grip] tool. It super easy to use! All you need to do is:

<pre>
<b>pip install grip
# cd to your project directory
grip
# open your web-browser at http://localhost:6419</b>
</pre>

[grip]: https://github.com/joeyespo/grip
