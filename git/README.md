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

## GitHub

**Markdown** is the documention format of choice for code on GitHub. If you want to live-preview files in the format they will show up before pushing you can use the handy [Grip][grip] tool. It super easy to use! All you need to do is:

```bash
pip install grip
# cd to your project directory
grip
# open your web-browser at http://localhost:6419
```

[grip]: https://github.com/joeyespo/grip
