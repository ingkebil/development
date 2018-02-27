# Confinement

It is possible to truely compartimentalize your conda env with the inclusion of bash functions, bash env variables, and aliases!

## Use case: aliases

So, you want to have your aliases available in your conda env only?

Solution? create a pre-activate script and post-deactivate script!

```bash
cd ${CONDA_BIN}
mkdir -p ./etc/conda/activate.d
mkdir -p ./etc/conda/deactivate.d
touch ./etc/conda/activate.d/alias.sh
touch ./etc/conda/deactivate.d/unalias.sh
```

The `./etc/conda/activate.d/alias.sh` is the pre-activate script and will be run before your conda env becomes active.
The `./etc/conda/deactivate.d/unalias.sh` is the post-deactivate script and will be run after your conda env is deactivated.

```bash
cat ./etc/conda/activate.d/alias.sh
alias lol='ls -ltr'
```

```bash
cat ./etc/conda/deactivate.d/unalias.sh
unalias lol
```

## Sources
https://conda.io/docs/user-guide/tasks/manage-environments.html#saving-environment-variables
