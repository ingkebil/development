# How to push to production?

... and rollback if things go haywire!

## Snapshot!

Take a snapshot of the current conda env!

```$ savetheconda prod170926```

This will:
- create a list of installed conda and pip packages and version control it in the servers repo
- create a cloned conda env of the selected environment

e.g.  `savetheconda prod170926` will create a conda under the name *A_prod170926_180313082333_kenny.billiau*

with:
- A: archive
- prod170926: the name of the conda env
- 180313082333: archive timestamp
- kenny.billiau: name of person executing the savetheconda

## Install/Upgrade

You can now install/upgrade your package with pip

For package available on PiPY
```$ pip install -U --no-deps cg```

For packages only available on github
```$ pip install -U --no-deps git+https://github.com/Clinical-Genomics/cg.git```

We recommend to install with `--no-deps` as to avoid upgrading dependencies.
