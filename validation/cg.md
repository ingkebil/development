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
In the `.bashrc` file there is an alias for the BETA binaries.
```
BETA_CONDA_BIN="/mnt/hds/proj/bioinfo/SERVER/miniconda/envs/beta/bin"
```

together with a sourcing of an alias dotfile:

```
source ~/servers/dotfiles/aliases.sh
```

which holds both alias for production under the `## Production` header and testing aliases under the `## Beta` header. Specifically for beta:
```
## beta
alias beta-cg="${CONDA_BIN}/cg --config ${HOME}/servers/config/beta/cg.yaml"
```

As you can see, this actually points to the production binary for cg, but has a seperate configuration file for other tool binaries and databases. This is due to the fact we want to mimick the actual production setting as much as possible. Therefore, we need to use the production code of cg already installed. The config file `${HOME}/servers/config/beta/cg.yaml` list all other tools and databases needed to initiate different processes required by cg commands. These should point to test or the production databases depending on your needs. Update a copy of this config file for your particurlar test if you need to modify this to other requirements.

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
$ beta-cg analysis -f vitalmouse

## Customer validation (snv/indel)

$ beta-cg analysis -f cuddlyoryx

$ beta-cg analysis -f firstfawn

$ beta-cg analysis -f topsrhino

$ beta-cg analysis -f usablemarten

## Customer validation (Uniparental disomy, UPD)

$ beta-cg analysis -f easybeetle

## Customer validation (sv)

$ beta-cg analysis -f epicasp

$ beta-cg analysis -f rightmacaw

$ beta-cg analysis -f hotskink

```

### 3.1 Start analysis using separate commands
```Bash
# Link fastqc files
beta-cg analysis link -f [family_id]

# Create pedigree file
beta-cg analysis config [family_id]

# Create gene panel file
beta-cg analysis panel [family_id]

# Start the analysis
beta-cg analysis start [family_id]
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
