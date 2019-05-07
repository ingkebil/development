# Stage

## What is stage?

The environment in which we test our proposed solution before we push it to production is called stage. It should as closely as possible resemble production in terms of software dependencies, configuration, hardware, and data.

A staging environment can be destroyed and you cannot trust that the a previously set up stage is still fully reflecting production. Meaning one needs to be able to quickly setup stage again.

No development should happen in stage.

## Locations

All scripts are found in `~/servers/resources` on both rasta and clinical-db.

All staging websites are found on clinical-db in directory `~/STAGE/`.

All staging names, both packages and databases, have been named with -stage appended to the package name, e.g. trailblazer-stage.

## How to activate stage

Rasta and clinical-db
```
cd ~/servers/resources
. activate-stage.sh
```

## How to update stage

Each software package, or better, each component of a software package, be it frontend or cli, should have an `update-component.sh` script.
