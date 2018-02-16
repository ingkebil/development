# Trailblazer
This is a step-wise instruction on how to set-up and validate Trailblazer

   1. [Python](#1-python)
   2. [Validation environment](#2-validation-environment)
   3. [Trailblazer](#3-trailblazer)

## 1. Python
Trailblazer requires python 3.6 or above. Use conda to handle different versions of python and pip to handle python packages. You can find installation instructions for [conda](https://github.com/Clinical-Genomics/development/tree/master/conda) and [python and pip](https://github.com/Clinical-Genomics/development/tree/master/python) by following the links.

## 2. Validation environment
Follow the conda conventions in the [conda guide](https://github.com/Clinical-Genomics/development/tree/master/conda).
```bash
$ conda create --name D_180214_hs python=3.6 pip
```

## 3. Trailblazer
We need to clone the Trailblazer repo in a place where it does not affect production for instance under `/mnt/hds/proj/bioinfo/develop/modules`.
```Bash
$ cd /mnt/hds/proj/bioinfo/develop/modules
$ git clone https://github.com/Clinical-Genomics/trailblazer
$ cd trailblazer
$ pip install --editable .
```

## 3.1 Test Trailblazer
First we need to create a new database, run:
```Bash
$ trailblazer --database "sqlite:///tb.sqlite3" init --reset
```
This will create an sqlite databse calles tb.sqlite3 in your working directory.

The test needs a database URL to use in the testing phase:
```Bash
SQLALCHEMY_DATABASE_URI=[dir_path_to_your_db]/tb.sqlite3;
export SQLALCHEMY_DATABASE_URI
```


Run the test suite
```Bash
$ pytest tests/mip
$ pytest tests/cli
$ pytest tests/store
$ pytest tests/server
```

Clean up
```Bash
$ unset SQLALCHEMY_DATABASE_URI
```

## 4. Setup config file
It is convient to set up a config file for trailblazer pointing to your trailblazer database, the mip binary and a mip global config. The config file is in yaml format:
```YAML
---
database: mysql+pymysql://userName:passWord@domain.com/database
script: /path/to/MIP/mip.pl
mip_config: /path/to/global/MIP_config.yaml
```
An existing config to use for development can be copied for development use from:

`/mnt/hds/proj/bioinfo/develop/config/trailblazer.yaml`
 
## 5. Starting MIP via Trailblazer
It is convient to add an alias to your .bashrc. **NOTE**: Currently this is required for testing as the production setting with the use of the word trailblazer is aliased.
Add this to your .bashrc:
```
alias dtb="/mnt/hds/proj/bioinfo/SERVER/miniconda/envs/D_tb_180214_hs/bin/trailblazer -c /mnt/hds/proj/bioinfo/develop/config/trailblazer.yaml"
```

```
source activate [mip_env]
dtb start --command 643594-testset
```

