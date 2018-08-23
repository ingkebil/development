# How to push to production?

... and rollback if things go haywire!

## Snapshot!

Take a snapshot of the current conda env!

```savetheconda prod170926```

This will:
- create a list of installed conda and pip packages and version control it in the servers repo
- create a cloned conda env of the selected environment

e.g.  `savetheconda prod170926` will create a conda under the name *A_prod170926_180313082333_kenny.billiau*

with:
- A: archive
- prod170926: the name of the conda env
- 180313082333: archive timestamp
- kenny.billiau: name of person executing the savetheconda

# How to restore a conda-backup

When things go wrong, you can restore a backup by running:

```conda env create -n prod170926 -f A_prod170926_180313082333_kenny.billiau```

Use the `--force` for the creation  of  environment (removing a previously existing environment of the same name).
