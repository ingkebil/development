# MIP validation
This is a step-wise instruction on how to set-up and validate MIP.

   1. [Perl](#1-perl)
   1. [MIP](#2-mip)
       1. [Cpanm](#21-cpanm)   
       1. [Install cpanm modules](#22-install-cpanm-modules)
       1. [Test cpanm and mip_install](#23-test-cpanm-and-mip_install)
   1. [Installing MIP and prerequistes](#3-installing-mip-and-prerequistes)
       1. [Svdb](#31-svdb)
       1. [Python 3 tools](#32-python-3-tools)
       1. [Cnvnator](#33-cnvnator)
       1. [Vep](#34-vep)
       1. [MIP main environment](#35-mip-main-environment)
       1. [Test MIP](#36-test-mip)
   1.  [Resources](#4-resources)

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
$ cd /mnt/hds/proj/bioinfo/develop/modules
$ git clone https://github.com/Clinical-Genomics/MIP.git
$ cd MIP
$ git checkout master
```

### 2.1 Cpnam 
MIP uses several perl modules outside of the perl core distribution. These needs to be installed preferentially to a separate cpanm library tied to your perl version. To install a new cpanm library to a specific perl version, run:
```Bash
$ perlbrew lib create perl-5.26.0@MIP
```
To switch default cpanm library for a specific perl version run:
```Bash
$ perlbrew switch perl-5.26.0@MIP
```
To change only for your current session, run:
```Bash
$ perlbrew use perl-5.26.0@MIP
```

### 2.2 Install cpanm modules
Update the cpanm library to take into account any updates in MIP prerequistes:
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

## 3. Installing MIP and prerequistes
The programs supported by MIP requires several references. To save time it is usually a good idea to hard link reference from an already exsting previous mip reference dir (if you have one).
```Bash
$ mkdir -p /mnt/hds/proj/bioinfo/MIP_ANALYSIS/references_6.0
$ ln /mnt/hds/proj/bioinfo/MIP_ANALYSIS/references_5.0/* /mnt/hds/proj/bioinfo/MIP_ANALYSIS/references_6.0
```

If you supply the intended MIP reference directory using the `--reference_dir` flag the install script will try to download most of the supported reference that are required. Note that this is not all of the references as not all of them are available for download and that this process may take some time as some references are quite large. 

Some tools have conflicting dependencies. Therefore, it is required to place them in separate conda environments.

### 3.1 Svdb 
```Bash
$ perl mip_install.pl -env P_mip-svdb_180203_hs -sp svdb -sp vcfanno -sp vt -sp bcftools -sp htslib -sp picard
$ bash mip.sh
```
Add these lines to your mip config file:
```YAML
 - module_source_environment_command:
     psv_combinevariantcallsets: "source activate P_mip-svdb_180203_hs"
```

### 3.2 Python 3 tools
```Bash
$ perl mip_install.pl -env P_mip-pyv3.6_180203 --python_version 3.6 --select_program genmod --select_program chanjo --select_program variant_integrity --select_program multiqc
$ bash mip.sh
```
Add these lines to your mip config file:
```YAML
 - program_source_environment_command:
     pgenmod: "source activate P_mip-pyv3.6_180203"
 - module_source_environment_command:
     pfrequency_filter: "source activate P_mip-pyv3.6_180203"
     pchanjo_sexcheck: "source activate P_mip-pyv3.6_180203"
     pmultiqc: "source activate P_mip-pyv3.6_180203"
     prankvariant: "source activate P_mip-pyv3.6_180203"
     psv_rankvariant: "source activate P_mip-pyv3.6_180203"
```

### 3.3 Cnvnator
```Bash
$ perl mip_install.pl -env P_mip-cnvnator_180203 --select_program cnvnator
$ bash mip.sh
```
Add these lines to your mip config file:
```YAML
 - module_source_environment_command:
     pcnvnator: "LD_LIBRARY_PATH=/mnt/hds/proj/bioinfo/SERVER/miniconda/lib/:$LD_LIBRARY_PATH; export LD_LIBRARY_PATH; source /mnt/hds/proj/bioinfo/SERVER/miniconda/envs/mip_cnvnator/root/bin/thisroot.sh; source activate P_mip-cnvnator_180203"        
```

### 3.4 Vep
```Bash
$ perl mip_install.pl -env P_mip-6.0_180203 --sp vep
$ bash mip.sh
```
Add these lines to your mip config file:
```YAML
 - module_source_environment_command:
     pvarianteffectpredictor: "LD_LIBRARY_PATH=/mnt/hds/proj/bioinfo/SERVER/miniconda/envs/P_mip-vep_180203/lib/:$LD_LIBRARY_PATH; export LD_LIBRARY_PATH; source activate P_mip-vep_180203"
     psv_varianteffectpredictor: "LD_LIBRARY_PATH=/mnt/hds/proj/bioinfo/SERVER/miniconda/envs/P_mip-vep_180203/lib/:$LD_LIBRARY_PATH; export LD_LIBRARY_PATH; source activate P_mip-vep_180203"
```
### 3.5 MIP main environment
```Bash
$ perl mip_install.pl -env P_mip-6.0_180203 --skip svdb --skip vep
$ bash mip.sh
```
Add these lines to your mip config file:
```YAML
source_main_environment_commands:
  - source
  - activate
  - P_mip-6.0_180203
```

### 3.6 Test MIP
Now that all prerequisites have been installed, run:
```Bash
$ cd t; prove -r
$ cd -
```
to test the MIP installation.

Perform your changes and depending on the type of update (major, minor, patch) run the test suite and integration tests (run_tests.t) as well as actual test data sets. These can be found in the test data directory - described below:

**WGS/WES**
- 643594-testset: Small dataset mainly used to test minor and patches updates. Execution time: ~ 1 h
- 643594-200M: Low coverage hapmap dataset. Execution time: ~ 24 h
- 643594-450M: High coverage hapmap dataset. Execution time: ~ 24-30 h

## 4. Resources
  - Test data directories: `/mnt/hds/proj/cust000/validations/`
  - Reference directories: `/mnt/hds/proj/bioinfo/MIP_ANALYSIS/`
  - MIP develop config directory: `/mnt/hds/proj/bioinfo/develop/config/`
  - MIP develop analysis directories: `/mnt/hds/proj/bioinfo/develop/customers/cust000/` 
