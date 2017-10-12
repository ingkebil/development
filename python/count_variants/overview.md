# Creating a Python package

To be able to reuse code it is important to package things we are doing in a way that makes them easy to install and operate.
There are of course a number of ways to handle this and we will describe our prefered way to do it here.
I will use an example as we go along; we are going to create a package called `count_variants` that is used to count variants with different selection criteria in a [VCF][vcf] file.

In this example we will tie together many of the topics described in this guide, like [testing](../testing.md), [conventions](../conventions.md), [git](../../git/README.md), [logging](../logging.md) and perhaps some more.

## Overview

* [1. Start a structure](./structure.md)
	* [1.1 Basics](./structure.md#11-Basics)
	* [1.2 README](./structure.md#12-README)
	* [1.3 LICENSE etc](./structure.md#license)
	* [1.4 First commit](./structure.md#first_commit)
* [2. setup.py](./setup_py.md)
* [3. First Module](./count_module.md)
	* [3.1 first function](./count_module.md#first_function)
	* [3.2 cli](./count_module.md#cli)
	* [3.3 missing modules](./count_module.md#33-Missing-modules)
* [3. Installing](./installing.md)

[next](./structure.md)

[vcf]: https://en.wikipedia.org/wiki/Variant_Call_Format
