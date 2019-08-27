# MIP validation
This is a step-wise instruction on how to set-up and validate MIP.

   1. [Perl](#1-perl)
   1. [MIP](#2-mip)
       1. [Cpanm](#21-cpanm)   
       1. [Install cpanm modules](#22-install-cpanm-modules)
       1. [Test cpanm and mip_install](#23-test-cpanm-and-mip_install)
   1. [Installing MIP and prerequistes](#3-installing-mip-and-prerequistes)
       1. [Setting up MIP's config](#31-setting-up-mip's-config)
       1. [Downloading MIP's references](#32-downloading-mip's-references)
   1. [Developing and testing MIP](#4-developing-and-testing-mip)
   1. [Resources](#5-resources)

## 1. Perl
MIP requires perl 5.26.0 or above. We use perlbrew to handle different versions of perl and cpanm librarires. You can find installation instructions for perl and cpanm [here](https://github.com/Clinical-Genomics/development/blob/master/perl/installation/installation.md). Information on your current, perl version and cpanm libraries can be found with:
```Bash
$ perlbrew list
```
An asterix denotes your current settings.

If you already have the perl version you want installed and it is not the default perl version, run:
```Bash
$ perlbrew use perl-5.26.0
```

## 2. MIP
We need to clone the MIP github repo in a place where it does not affect production.
```Bash
$ cd /home/proj/development/rare-disease/git
$ git clone https://github.com/Clinical-Genomics/MIP.git
$ cd MIP
$ git checkout master
```

### 2.1 Cpanm
MIP uses several perl modules outside of the perl core distribution. These needs to be installed preferentially to a separate cpanm library tied to your perl version. To install a new cpanm library to a specific perl version, run:
```Bash
$ perlbrew lib create perl-5.26.0@D-MIP_<signature>
```
To switch default cpanm library for a specific perl version run:
```Bash
$ perlbrew switch perl-5.26.0@D-MIP_<signature>
```
To change only for your current session, run:
```Bash
$ perlbrew use perl-5.26.0@D-MIP_<signature>
```

### 2.2 Install cpanm modules
Update the cpanm library to take into account any updates in MIP prerequisites:
```Bash
$ cd definitions
$ cpanm --installdeps .
$ cd -
```

### 2.3 Test cpanm and mip_install
```Bash
$ cd t; prove mip_install.t
$ cd -
```

## 3. Installing MIP and prerequisites
Due to dependency conflicts MIP needs multiple conda environments to function properly. The names of these environments are set using the '--envn' flag.

Generate the install script and start installation:
```bash
$ perl mip install rd_dna --envn \
emip=D_mip<major.minor>_rd-dna_<signature> \
ecnvnator=D_mip<major.minor>_rd-dna_cnvnator_<signature> \
edelly=D_mip<major.minor>_rd-dna_delly_<signature> \
epeddy=D_mip<major.minor>_rd-dna_peddy_<signature> \
eperl5=D_mip<major.minor>_rd-dna_perl5_<signature> \
epy3=D_mip<major.minor>_rd-dna_py3_<signature> \
esvdb=D_mip<major.minor>_rd-dna_svdb_<signature> \
etiddit=D_mip<major.minor>_rd-dna_tiddit_<signature> \
evep=D_mip<major.minor>_rd-dna_vep_<signature>

$ bash mip.sh
```
Test the installation by running:
```Bash
$ prove t
$ perl t/mip_analyse_rd_dna.test
```
### 3.1 Setting up MIP's config
MIP provides a template, which can be found here in the MIP dir: `templates/mip_rd_dna_config.yaml`

Go to the load_env key and change the environment names (called `mip_travis_<package>` in the template) to the ones specified during the installation.

### 3.2 Downloading MIP's references
The programs supported by MIP requires several references. To save time it is usually a good idea to hard link reference from an already existing previous mip reference dir (if you have one).
```Bash
$ mkdir -p /home/proj/development/rare-disease/references_mip<major.minor>/
$ ln /home/proj/development/rare-disease/references/* /home/proj/stage/rare-disease/references_mip<major.minor>/
```
MIP's standard references are specified in `templates/mip_download_rd_dna_config_-1.0-.yaml`. MIP can automatically detect which references that has been changed between MIP versions and needs an update. First open the template file and change the environment name under the key load_env to MIP's conda environment (in our case D_mip<major-minor>_rd-dna).

```Bash
$ conda activate D_mip<major-minor>_rd-dna
$ mip download rd_dna -c templates/mip_download_rd_dna_config_-1.0-.yaml --reference_dir /home/proj/development/rare-disease/references_mip<major.minor>
```
This launches SLURM jobs that will download the missing references.

Some of MIP's references cannot be automatically downloaded. See the section [Private References](https://github.com/Clinical-Genomics/MIP/blob/master/documentation/Setup.md#private-references) on MIP's github repo.

## 4. Developing and testing MIP
Perform your changes and depending on the type of update (major, minor, patch) run the test suite and integration tests (prove t -r -j 9) as well as actual test data sets. These can be found in the test data directory - described below:

**WGS/WES**
- 643594-testset: Small dataset mainly used to test minor and patches updates. Execution time: ~ 1 h
- 643594-200M: Low coverage hapmap dataset. Execution time: ~ 24 h
- 643594-450M: High coverage hapmap dataset. Execution time: ~ 24-30 h

## 5. Resources
  - Test data directories: `/home/proj/development/rare-disease/mip<major-minor>_<signature>/`
  - Reference directories: `/home/proj/development/rare-disease/references`
  - MIP stage config directory: ` /home/proj/development/servers/config/hasta.scilifelab.se/`
  - MIP stage analysis directories: `/home/proj/development/rare-disease/cases/`
