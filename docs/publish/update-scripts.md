# How to easily update your tool?

You will want to create two scripts, at least:

- one to update your tool on stage
- one to update your tool on prod

Yes, I just wrote that out in full. It's that important!

## Stage CLI update script

How does such a script look like. Well, let's have a look at one that closest resembles a template, `update-trailblazer-stage.sh`

```bash
#!/usr/bin/env bash

# exit on error
set -e

# to be able to log the deploy of this tool, we need to know the organisation/user and the tool name 
TOOL='clinical-genomics/trailblazer'

# determine where this script is located ...
SCRIPTPATH=$(dirname $(readlink -nm $0))

# ... because we execute scripts relatively to this script. Leave this assert out if this script can be executed by anyone
sh ${SCRIPTPATH}/../assert_user.sh hiseq.clinical

# make sure we run on rasta. Leave this assert out if this script can be run on all servers
sh ${SCRIPTPATH}/../assert_host.sh hasta.scilifelab.se

# One optional argument
BRANCH=${1}

# make sure we can have access to aliases
shopt -s expand_aliases

# make sure we are closely resembling production
source ${HOME}/.bashrc

# go to stage. Yes, this conda env should already exist
source activate S_main

# get the current version of the tool for logging purposes
CURRENT_VERSION=$(trailblazer --version)

# install with latest changes on "master"
pip install -U git+https://github.com/Clinical-Genomics/trailblazer@$BRANCH

# get the updated version of the tool for logging purposes
UPDATE_VERSION=$(trailblazer --version)

# log the deploy - for stage this will only output the command it would have run
bash "${SCRIPTPATH}/../log-deploy.sh" "$TOOL" "$CURRENT_VERSION" "$UPDATED_VERSION"

# make sure nothing in stage broke
exec ${SCRIPTPATH}/../test_version_command.sh
```

You run it:
```bash
cd ${PRODUCTION_HOME}/servers/resources
bash update-trailblazer-stage.sh
```

Or you update stage to a specific branch:
```bash
cd ${PRODUCTION_HOME}/servers/resources
bash update-trailblazer-stage.sh beta
```

`${PRODUCTION_HOME}` is not set on clinical-db and clinical-preproc. Instead, use hiseq.clinical's home directory.

### Web update script

For web frontend, one can add everything you need to update a staging env:

```bash
#!/usr/bin/env bash

# exit on error
set -e

# to be able to log the deploy of this tool, we need to know the organisation/user and the tool name 
TOOL='clinical-genomics/trailblazer'

# determine where this script is located ...
SCRIPTPATH=$(dirname $(readlink -nm $0))

# ... because we execute scripts relatively to this script. Leave this assert out if this script can be executed by anyone
sh ${SCRIPTPATH}/../assert_user.sh hiseq.clinical

# make sure we run on rasta. Leave this assert out if this script can be run on all servers
sh ${SCRIPTPATH}/../assert_host.sh clinical-db.scilifelab.se

# One optional argument, prefilled
BRANCH=${1-master}

# make sure we can have access to aliases
shopt -s expand_aliases

# make sure we are closely resembling production
source ${HOME}/.bashrc

# go to stage. Yes, this conda env should already exist
source activate stage

# get the current version of the tool for logging purposes
CURRENT_VERSION=$(trailblazer --version)

# install with latest changes on "master"
pip install -U git+https://github.com/Clinical-Genomics/trailblazer@${BRANCH}

# get the updated version of the tool for logging purposes
UPDATE_VERSION=$(trailblazer --version)

# install
cd ~/STAGE/trailblazer/nuxt
git pull
echo ${BRANCH} > current_version.txt
git rev-parse HEAD >> current_version.txt
yarn

GOOGLE_OAUTH_CLIENT_ID="apps.googleusercontent.com" \
API_URL="http://localhost:7076/api/v1" \
API_URL_BROWSER="https://trailblazer-api-stage.scilifelab.se/api/v1" \
yarn build --universal

# restart the Flask service
supervisorctl restart trailblazer-stage
supervisorctl restart trailblazer-api-stage

# Drop you back to the initial directory
cd -
```

## Naming of scripts

The suggestion is to name your script: `update-$tool-stage.sh`

with `$tool` the name of your component, be it `trailblazer` for the cli or `trailblazer-ui` for the web.

## What about config files?

Premade config files for all packages used in production and stage have been made in the `config` dir of the servers repo. This can be found on:

```
cd ${PRODUCTION_HOME}/servers/config
```

All config files point to the stage location of the package, if any, to lims-stage, and to the staging databases.

## What about databases?

### MySQL

All databases are located on clinical-db. To make sure you have the latest uncorrupted data, you can make a copy of one or all databases like this:

On clinical-db, copying all databases:
```
cd ${PRODUCTION_HOME}/servers/resources
bash dbcopy-prod-to-stage.sh
```

On clinical-db, copy one database:
```
cd ${PRODUCTION_HOME}/servers/resources
bash dbcopy-prod-to-stage.sh trailblazer
```

The credentials to the stage databases have already been set in the stage configs.

### Mongo

All mongodbs are located on clinical-db. To copy both scout and loqusdb, you can issue:

```
cd ${PRODUCTION_HOME}/servers/resources
bash dbcopy-mongoprod-to-stage.sh
```

This will reinstate a backuped version of scout (dated: 2018-05-18) and a fresh copy of loqusdb.

Please be aware that this process takes several days to complete!

The mongo-stage server is not running by default. To start the mongo-stage run:

```
cd ${PRODUCTION_HOME}/servers/resources
bash start-mongo-stage.sh &
```
