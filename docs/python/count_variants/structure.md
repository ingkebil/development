# 1. Setup a structure

To start with let's create a environment and a directory for our package.
Assuming you have conda installed, run the following:

## 1.1 Basics

```bash
conda create -n count_variants python=3
source activate count_variants
mkdir count_variants
cd count_variants
```

We wan't to do version handling with git, to make this a git repository do 

```bash
git init
touch .gitignore
```

The `.gitignore` file is explained in the [git section](../../git/README.md), for now we only need to know that this file tells git what to care and not care about. 

## 1.2 README

Every decent python package should at least include a README file that describes the intention of the writer.
Let's create a `README.md` file, this will be updated as we go along. For now do

```bash
touch README.md
```

open the file with an [editor](../../editors/README.md) of your choice and write the following:

```markdown
# count_variants
A package to count variants in VCF files based on different criterias.
```

> You might recognize this as "markdown", a markup language for formatting text. You can read more about it under [Documentation](../../documentation/README.md).

## 1.3 LICENSE, MANIFEST.in, requirements.txt  {#license}

Next step is to include a `LICENSE` file, every project should have one. There are many different licenses, you can read more [here][licenses]. For now we will choose a [MIT license][mit].
Open a file called LICENSE and copy paste the [MIT License][mit] and fill in year and name.

`MANIFEST.in` is a file that explains what non python static files should be included in the distribution. For now we will leave that one empty. Just do:

```bash
touch MANIFEST.in
```

`requirements.txt` is for declaring which third party software our package depends on. Right now we only know that we will be using [Click][click] to build a cli, so run:

```bash
echo click > requirements.txt
```

## 1.4 First commit {#first_commit}

Save the changes. It is now time to do our first commit! Run:

```bash
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
	README.md
	LICENSE
	MANIFEST.in
	requirements.txt

nothing added to commit but untracked files present (use "git add" to track)
$ git add .gitignore README.md LICENSE MANIFEST.in requirements.txt
$ git commit -m "First commit"
$ git status
On branch master
nothing to commit, working tree clean
```

[licenses]: https://help.github.com/articles/licensing-a-repository/
[mit]: https://choosealicense.com/licenses/mit/
[click]: http://click.pocoo.org/5/
