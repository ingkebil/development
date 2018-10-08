# Installing

So it is time to install our package and see that everything works, exciting! 😃

There is only one thing missing; tell `setup.py` how to use the command line interface that we wrote earlier.
Open `setup.py` and look for `entry_points` section. Change it to look like:

```python
    entry_points={
        'console_scripts': [
            'count_variants = count_variants.cli.root:cli'
        ],
    },
```

We are telling `setup.py` that if someone write `count_variants` on the command line run the function `cli()` in the file `count_variants.cli.root`.

------------------------------------

Now we are going to run the command that installs all dependencies and the package itself:

```bash
pip install --editable .
```

Watch the magic happen! 🔮

When you are done you should be able to write:

```bash
$ count_variants
Usage: count_variants [OPTIONS] VCF

Error: Missing argument "vcf".
```

Great job!!!
If you have a vcf file lying around you could try and feed that to the program and see if it works.

In the following sections we will add some complexity, write tests and push the code to GitHub so others can see it.
