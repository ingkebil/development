# Conda

  1. [Introduction](#1-introduction)
  1. [Environments](#2-environments)
  1. [Packages](#3-packages)
      1. [Version](31#-versions)

## 1. Introduction

[Conda] is a package, dependency and environment manager for any language. Conda actually consists of Anaconda and a smaller version called Miniconda. Miniconda is usually sufficient most of the time, but you can also install anaconda from miniconda using:
```Bash
$ conda create -n test_ananconda anaconda
```

The `conda` command is the primary interface for managing installations of various packages and environments.

## 2. Environments

A conda environment is a directory that contains a specific collection of conda packages that you have installed. If you change one environment, your other environments are not affected.
Condas default environment is called base or root.

To create an environment, run:
```Bash
$ conda create --name [environment]
```

You can easily activate or deactivate environments, which is how you switch between them.

To activate an environment, run:
```Bash
$ source activate [environment]
```

Conda puts an asterisk (*) in front of the active environment. You can view your environments with:
```Bash
$ conda info --envs
```
or
```Bash
$ conda env list
```

Your active environment will also show in front of your prompt:
```Bash
(my_env) $
```

To deactivate your current environment:
```Bash
$ source deactivate
```

You can copy your environment by:
```Bash
$ conda create --name [environment] --clone [copy_of_environment]
```

You can also share your environment with someone by giving them a copy of your environment.yaml file.

To remove an environment, run:
```Bash
$ conda remove --name [environment] --all
```

## 3. Packages
A conda package is a compressed tarball file that contains system-level libraries, Python or other modules, executable programs and other components. Conda keeps track of the dependencies between packages and platforms. Conda packages are downloaded from remote channels, which are URLs to directories containing conda packages. The conda command searches a default set of channels, and packages are automatically downloaded and updated from a central repository.

To install conda packages in your active environment (default or other), run:
```Bash
$ conda install [packagename_1] [packagename_2]
```

To install conda packages in an environment, run:
```Bash
$ conda install --name [environemnt] [packagename_1] [packagename_2]
```

It is also possible to create a new environment and install packages at the same time
```Bash
$ conda create --name [environment] [packagename]
```

To list all packages in a conda environment, run: 
```Bash
$ conda list --name [environment]
```

To remove a package, run:
```Bash
$ conda remove --name [packagename]
```

### 3.1 Versions
To install or change a specific version of a package use the syntax [packagename]=[version].
```Bash
$ conda install samtools=1.6.0 vt=170135
```


[Conda]: https://conda.io/docs/index.html
