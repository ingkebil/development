# 3. First module {#first_module}

Ok so finally we can start to write some actual python code! In this section we will learn about file structure, imports and a little bit about command line interfaces.
When we finish this section we should have a small program that counts the number of variants in a vcf.
We will try to keep the code separated inside our projekt as described [here](../conventions.md), we store the counting code in a submodule called utils and the cli code in a module called cli. So run:

```bash
mkdir count_variants/cli count_variants/utils
touch count_variants/cli/__init__.py
touch count_variants/utils/__init__.py
touch count_variants/cli/root.py
touch count_variants/utils/count.py
```

Ok a lot of files created here, the `__init__.py` files we know from before, they are there to tell that this is a module.
`count_variants/cli/root.py` will include the command line interface to our program and `count_variants/utils/count.py` will include the code that counts vcf variants.

## 3.1 Writing the first function {#first_function}

Open `count_variants/utils/count.py` and write the following

```python
def count_variants(vcf):
    """Count the number of variants in a vcf file

    Args:
        vcf(iterable): An iterable with variants

    Returns:
        nr_variants(int): Number of variants in file
    """
    nr_variants = 0
    for variant in vcf:
        nr_variants += 1

    return nr_variants

```

The text within quotation marks is a docstring, **EVERY** function you write should have a docstring that at least explains what the intention of the function is and input and output.

## 3.2 Writing the CLI {#cli}

Now open `count_variants/cli/root.py` and write:

```python
import logging

import click
import coloredlogs

from cyvcf2 import VCF

from count_variants.utils.count import count_variants

LOG = logging.getLogger(__name__)

@click.command()
@click.argument('vcf', type=click.Path(exists=True))
def cli(vcf):
    """Count the variants in a vcf"""
    coloredlogs.install(level='INFO')
    LOG.info("Reading vcf file: %s", vcf)

    vcf_obj = VCF(vcf)

    nr_variants = count_variants(vcf_obj)

    click.echo("Nr variants in vcf: %s" % nr_variants)
```

It is a good convention to import modules from standard library first, then third party modules and finally local imports.

In this case we will go through the code line by line.

 - `logging` is the standard library solution for logging in python.
 - `click` is our prefered package to build command line interfaces.
 - `coloredlogs` is a wrapper for `logging` that makes logging look good and super easy.
 - `cyvcf2` is a reliable and fast parser for VCF files
 - `count_variants.utils.count` on this line we import the function that we wrote in the previous section
 - `LOG = logging.getLogger(__name__)` here we create a logging object and name it `LOG`
 - `@click.command()` is a [decorator][decorators], you do not need to understand the concept right now. It basically give the following function some properties
 - `@click.argument()` this is how an argument is defined in click

Then comes the function definition, the docstring and some code that should be rather straight forward.

## 3.3 Missing modules

The modules in standard library follow with the python distribution so there is no need to install those. As you may have noticed there are some modules used here that are missing in our `requirements.txt` file. It can be a bit hard to know what third party modules that will be used when starting a project. So lets add `coloredlogs` and `cyvcf2` to `requirements.txt`, when you are done it should look like:

```bash
$ cat requirements.txt
click
coloredlogs
cyvcf2
```

--------------------------

If everything is done correct the folder structure should look like this now:

```bash
count_variants/
├── LICENSE
├── README.md
├── MANIFEST.in
├── .gitignore
├── setup.py
├── count_variants/
    ├── __init__.py
    ├── __version__.py
    ├── cli/
        ├── __init__.py
        ├── root.py
    ├── utils/
        ├── __init__.py
        ├── count.py
```

If you haven't done so already, stage all the files and commit them!

[decorators]: https://en.wikipedia.org/wiki/Python_syntax_and_semantics#Decorators
