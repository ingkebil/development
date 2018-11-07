# Activate conda envs

After you have created a conda environment, conda tells you the following:

```
#
# To activate this environment, use:
# > source activate D_mkdocs
#
# To deactivate this environment, use:
# > source deactivate D_mkdocs
#
```

## Production and stage

We have two special conda environments with special configurations: `prod` and `stage`.

`prod` is the main environment in which not surprisingly, our production tools are running. `stage` is a recent copy of `prod` used for testing of your latest finished branch and to test deployment.

What is so special about `prod` or `stage`? They come with all tools already pointing to their configurations and need to be activated using a shell script.

To activate `prod` environment, type:
```
up
```
or
```
useprod
```

To activate `stage` environment, type:
```
us
```
or
```
usestage
```

### I want to know more

`us` and `usestage` are aliases pointing to a script:

```
alias usestage='source ${HOME}/servers/resources/activate-stage.sh'
```

That script will activate the correct environment(s) and set the aliases for the environment.
