# Cg
This is a step-wise instruction on how to set-up cg for starting validation runs. 
   1. [Conda environment](#-1conda-environment)
   1. [Starting MIP using Cg](#2-starting-mip-using-cg)
       1. [Start vitalmouse](#21-start-vitalmouse)
       1. [Start cuddlyoryx](#22-start-cuddlyoryx)
       1. [Start firstfawn](#23-start-firstfawn)
       1. [Start topshrino](#24-start-topshrino)
       1. [Start usablemarten](#25-start-usablemarten)

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

As you can see, this actually points to the production binary for cg, but has a seperate configuration file for other tool binaries and databases. This is due to the fact that the cg installation is currently broken and we need to use the production code of cg already installed. The config file `${HOME}/servers/config/beta/cg.yaml` list all other tools and databases needed to initiate different processes required by cg commands. Update a copy of this config file for your particurlar test.

## 2. Starting MIP using Cg
This is a step-wise instruction on how to set-up and validate starting a MIP run.

NOTE: This guide will assume that you have installed all other tools in the cg config e.g. MIP, Trailblazer and housekeeper into the beta bin. Guides to install MIP and Trailblazer are available under validations on Clinical-Genomics/development.

NOTE: To enable use of trailblazer with cg add the mip [config.py] file from the trailblazer repo to your conda environment here:
```
[path_to_conda]/envs/[env_name]/lib/python3.6/site-packages/trailblazer/mip/config.py
```

This file is currently not included in the pip installation process.

In the cg config file: `${HOME}/servers/config/beta/cg.yaml`- modify the "script"(=mip binary), "mip_config"(=mip config file) and "root"(=where to place analysis output) according to you need.

```Bash
# Activate the main MIP environment
$ source activate P_mip-6.0_18020
```

## 2.1 Start vitalmouse
This will create all prerequisites for starting a MIP analysis and then launch the actual analysis.
```Bash
$ beta-cg analysis -f vitalmouse
```

## 2.2 Start cuddlyoryx
The `beta-cg analysis -f cuddlyoryx` cannot currently find the flow-cells and will fail. However, running each prerequisite command sequentially will work:
```Bash
# Link fastqc files
beta-cg analysis link -f cuddlyoryx

# Create pedigree file
beta-cg analysis config cuddlyoryx

# Create gene panel file
beta-cg analysis panel cuddlyoryx

# Start the analysis
beta-cg analysis start cuddlyoryx
```

## 2.3 Start firstfawn
The `beta-cg analysis -f firstfawn` cannot currently find the flow-cells and will fail. However, running each prerequisite command sequentially will work:
```Bash
# Link fastqc files
beta-cg analysis link -f firstfawn

# Create pedigree file
beta-cg analysis config firstfawn

# Create gene panel file
beta-cg analysis panel firstfawn

# Start the analysis
beta-cg analysis start firstfawn
```

## 2.4 Start topshrino
The `beta-cg analysis -f topsrhino` cannot currently find the flow-cells and will fail. However, running each prerequisite command sequentially will work:
```Bash
# Link fastqc files
beta-cg analysis link -f topsrhino

# Create pedigree file
beta-cg analysis config topsrhino

# Create gene panel file
beta-cg analysis panel topsrhino

# Start the analysis
beta-cg analysis start topsrhino
```

## 2.5 Start usablemarten
The `beta-cg analysis -f usablemarten` cannot currently find the flow-cells and will fail. However, running each prerequisite command sequentially will work:
```Bash
# Link fastqc files
beta-cg analysis link -f usablemarten

# Create pedigree file
beta-cg analysis config usablemarten

# Create gene panel file
beta-cg analysis panel usablemarten

# Start the analysis
beta-cg analysis start usablemarten
```

