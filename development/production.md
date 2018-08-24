# How to push to production?

... and rollback if things go haywire!

## Snapshot!

Take a snapshot of the current conda env! Go to `~/servers/resources`:

```bash savetheconda prod170926```

This will:
- create a list of installed conda and pip packages and version control it in the servers repo
- create a cloned conda env of the selected environment
- create a conda environment file from following template: `A_${CONDA_ENV}_$(date)_${SUDO_USER}`

with:

- $(hostname): the name of the server you're running the command on
- A: archived
- ${CONDA_ENV}: the name of the given conda environment
- $(date): current datetime
- ${SUDO_USER}: the name of the user executing the command determined from the bash environment, if possible.

So executing `bash savetheconda prod170926` will create a conda environment file named `A_prod170926_180824103445_kenny.billiau`.

# How to restore a conda-backup

When things go wrong, you can restore a backup by running:

```conda env create -n prod170926 -f `~/servers/conda/$(hostname)/A_prod170926_180313082333_kenny.billiau```

Use the `--force` for the creation  of  environment (removing a previously existing environment of the same name).

See [conda create](https://conda.io/docs/commands/env/conda-env-create.html)
