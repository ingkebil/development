# Cg
This is a step-wise instruction on how to set-up cg for starting validation runs. 
   1. [Conda environment](#-1conda-environment)
   1. [MIP](#2-mip)
       1. [Check family info](#21-check-family-info)
       1. [Check sample info](#22-check-sample-info)
       1. [Stage-cg](#23-stage-cg)
       1. [Housekeeper](#24-Housekeeper)
   1. [Start analyses](#3-start-analyses)
       1. [Start analysis using separate commands](#31-start-analysis-using-separate-commands)
   1. [Check analysis progress](#4-check-analysis-progress)

## 1. Conda environment
This validation environment use the conda beta environment. When you `source activate beta`, a pre-activate script will source aliases before sourcing your environment, see [conda confinement](https://github.com/Clinical-Genomics/development/blob/master/conda/confinement.md). The pre-actviate script set-up cg and trailblazer aliases specific to your environment and points to config files:

```Bash
BETA_CONDA_BIN="/mnt/hds/proj/bioinfo/SERVER/miniconda/envs/beta/bin"
alias cg="${BETA_CONDA_BIN}/cg --config ${HOME}/servers/config/beta/cg.yaml"
alias trailblazer="${BETA_CONDA_BIN}/trailblazer --config ${HOME}/servers/config/beta/trailblazer.yaml"
```

All config files of cg, trailblazer and MIP should reside in the `${HOME}/servers/config/beta/` directory.

The config file `${HOME}/servers/config/beta/cg.yaml` list all other tools and databases needed to initiate different processes required by cg commands. These should point to test or the production databases depending on your needs. Update a copy of this config file for your particurlar test if you need to modify this to other requirements.

The trailblazer config uses a different root directory than production to not mix the validation cases with production cases.

In essence, we are allowing testing of new binaries, using production databases and/or development databases, but performing analyses separated from production.

When you are finished with your validation, run:

```Bash
$ source deactivate
``` 

To perform the deactivation script which will unalias your conda environment aliases: `cg` and `trailblazer`.

## 2. MIP
This is a step-wise instruction on how to set-up and validate starting a MIP run.

#### Check prerequisites 
NOTE: This guide will assume that you have installed all other tools in the cg config e.g. MIP, Trailblazer and housekeeper into the beta bin. Guides to install MIP and Trailblazer are available under validations on Clinical-Genomics/development.

NOTE: To enable use of trailblazer with cg add the mip [config.py] file from the trailblazer repo to your conda environment here:
```
[path_to_conda]/envs/[env_name]/lib/python3.6/site-packages/trailblazer/mip/config.py
```

This file is currently not included in the pip installation process for unclear reasons.

In the cg config file: `${HOME}/servers/config/beta/cg.yaml`- modify the "script"(=mip binary), "mip_config"(=mip config file) and "root"(=where to place analysis output) according to you need.

```Bash
# Activate the main MIP environment
$ source activate P_mip-6.0_YYMMDD
```

### 2.1 Check family info
```Bash
$ cg get family [family_petname]

# For external ids
$ cg get family -c [customer_id] -n [external_family_id]
```

### 2.2 Check sample info
```Bash
$ cg get sample [sample_id]

# Sample flow-cell info
$ cg get sample -f [sample_id]
```

#### Sample origin
If the sample does not belong to cust000, import it to the cg database using cg add:
```Bash
# This creates a new family petname id and associated the family to cust000 and sets a default panel
$ cg add family cust000 [original_family_id]-validation -p OMIM-AUTO

# This set the sample phenotype and associates the sample with the family
$ cg add relationship [petname_family_id] [sample_id] -s affected
```

### 2.3 Stage-cg
Make sure that the flowcell in stage-cg has the status: "ondisk". If the flowcell actually is on disk, run:
```bash
$ cg set flowcell -s ondisk
```
to set the status of the flowcell to ondisk.

### 2.4 Housekeeper
Check that the fastq files are in housekeeper
```Bash
$ housekeeper get -V [sample_id]
```

If not run,
```Bash
$ cg transfer flowcell [flowcell-id]
```

and check housekeeper again.

Create a housekeeper bundle
```Bash
$ housekeeper include [sample_id]
```

## 3 Start analyses
This will create all prerequisites for starting a MIP analysis and then launch the actual analysis.
```Bash
## Hapmap
$ cg analysis -f vitalmouse

## Customer validation (snv/indel)

$ cg analysis -f cuddlyoryx

$ cg analysis -f firstfawn

$ cg analysis -f topsrhino

$ cg analysis -f usablemarten

## Customer validation (Uniparental disomy, UPD)

$ cg analysis -f easybeetle

## Customer validation (sv)

$ cg analysis -f epicasp

$ cg analysis -f rightmacaw

$ cg analysis -f hotskink

```

### 3.1 Start analysis using separate commands
```Bash
# Link fastqc files
cg analysis link -f [family_id]

# Create pedigree file
cg analysis config [family_id]

# Create gene panel file
cg analysis panel [family_id]

# Start the analysis
cg analysis start [family_id]
```

## 4. Check analysis progress
Can be done using the trailblazer web page at: https://trailblazer.scilifelab.se. Here you can also find the trailblazer analysis id by clicking on a family and looking at the last part of the in the adress field. This is also availiable on the command line:
```Bash
$ trailblazer ls
```
where the analysis id is the first column of the output.

You can delete an analysis by:
```Bash
$ trailblazer delete [ANALYSIS_ID]
```

To follow the progress of your analysis you will also have to run:

```Bash
$ trailblazer scan
```

since you are most probably processing the sample in a different trailblazer root directory than production. Hence, the automated trailblazer scan in production will not include your analyses. 
