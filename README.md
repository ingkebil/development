# Introduction

This is a software development guide.

## Setup

This section described how to setup the repo for development. To preview changes in the finished format you need the [GitBook CLI][gb-cli-repo]. To run it you need to install Node.js and NPM. If you are using [conda][conda] you should be able to run:

```bash
conda install -c conda-forge nodejs
# that line installs both `node` and `npm`
npm install -g gitbook-cli
# now you should be able to run
gitbook help
# to preview changes in a browser, navigate to the repo and run:
gitbook serve
```

You can read more in the official [GitBook Toolchain documentation][gb-toolchain].

[gb-cli-repo]: https://github.com/GitbookIO/gitbook-cli
[gb-toolchain]: https://toolchain.gitbook.com/setup.html
[conda]: https://conda.io/docs/

