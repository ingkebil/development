# Git

You can learn many thing by following the [guides][gh-guides] written by the GitHub team.

## Setting up this guide

```bash
git clone https://github.com/Clinical-Genomics/development
cd development
git branch [my-topic]
git checkout [my-topic]
```

> you can also write `git checkout -b [my-topic]`.

... and then you make some changes and add files to the repo. When you are ready:

```bash
git status   # check what you have updated
git add [files to commit]
git commit -m "[this is what I did]"
git push -u origin [my-topic]
```

Now you are ready to open a pull request which in done through the GitHub interface.

[gh-guides]: https://guides.github.com/
