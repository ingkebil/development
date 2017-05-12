# Workflows

## Local development environment

We develop almost exclusively in Python so this guide will focus on setting up a working Python development environment and a project: `cglims`.

### Prerequisites

We are going to assume the following:

1. You have full access to the GitHub organization [Clinical-Genomics][gh-org]
2. You have access to `clinical-lims-stage.scilifelab.se` (either by cable or VPN)
3. You have a working Git installation

### Steps

1. Install [Miniconda][miniconda]. Download the correct file for your system and either double-click or execute the file with Bash. Follow the on-screen instructions, answer "Yes" when prompted if the installer should modify your `.bashrc`. Finally either source `.bashrc` or start a new session.

2. You should now be able to run `conda`. Start by creating a new environment. We recommend that you setup a new conda environment for every project.

    ```bash
    conda create -n cglims python=3
    source activate cglims
    ```

    > FYI: [As specified](../python/README.md) we are using Python 3 for all new development.

3. Get the code from GitHub. We recommend you setup a `~/projects` folder where you keep all your code for development.

    ```bash
    cd ~/projects
    git clone https://github.com/Clinical-Genomics/cglims
    cd cglims
    ```

4. Install the package for development.

    ```bash
    pip install --editable .
    ```

[gh-org]: https://github.com/Clinical-Genomics/
[miniconda]: https://conda.io/miniconda.html
