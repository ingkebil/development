# Conda conventions at Clinical Genomics

- Avoid installing anything in the conda default environment (base) if possible
- Naming conventions for conda environments: `[env_type]_[creation_date]_[logical_name]_[signature]`
   - [env_type]: Allowed environment types are **devel** or **prod**
   - [creation_date]: YYMMDD
   - [logical_name]: Whatever makes sense
   - [signature]: Something to show who created the environment. Use the two- or three letter name akronyms assigned to you.
- List your production environment and dependent processes at the bottom of this page.
- It is considered unpolite to change or delete someone elses environment without involving the person which created the environment.

## Move environments from devel to prod

When it is time to move your development environment to production - make a copy of it and rename it following the above conventions e.g.:
```Bash
$ conda create --name devel_180101_mip5.0.12_hs --clone prod_180129_mip6.0.0_hs
```

## Production conda environments

- base
   - Process: MIP
- mip_cnvnator
   - Process: MIP
- mip_peddy
   - Process: MIP
