# Introduction

This is a software development guide.

## Getting started

If you are new to this repository we want to get you started right away! Please have a look at one of the [assignments](assignments/README.md).

## Setup

This section described how to setup the repo for development. To preview changes in the finished format you need [mkdocs][mkdocs]. If you are using [conda][conda] you should be able to run the following locally:

```bash
# create an active conda environment
conda create -n D_mkdocs
source activate D_mkdocs
# install our only dependency
pip install mkdocs
# now you should be able to run
mkdocs --help
# to preview changes in a browser, navigate to the repo and run:
mkdocs serve
# content is now served on http://127.0.0.1:8000 !
```



[mkdocs]: https://www.mkdocs.org/#getting-started
[conda]: https://conda.io/docs/
