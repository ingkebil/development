# Crontab

[Cron][cron] is a unix tool to run programs at certain times. Automatically! How great is that?
Cron saves this information into a file called `crontab`. Sometimes, cron and crontab are used interchangeably.

This document outlines how to write the perfect crontab entry.

## TL;DR

```
SHELL=/bin/bash
MAILTO=clinical-logwatch@scilifelab.se
CRONIC=~/server/resources/cronic

0 0 * * * $CRONIC your_awesome_program >> your_awesome.log 2> >(tee -a your_awesome.log >&2)
```

## Errors!

You really want to be notified when your automation goes wrong. This line will add an email address to the crontab:

```MAILTO=clinical-logwatch@scilifelab.se```

This will mail any output made by a crontab started program to the above mentioned email address.

## Only errors!

You don't want to be spammed with _all_ output of your programs. You only want to be notified when something goes wrong.

What does it mean "to go wrong"?

On the highest level, this mean when a program exits with a non-zero exit code. To make sure we only get emailed with the full output of our program when the program exits with a non-zero exit code, we make use of [cronic][cronic].
Cronic will capture all output of your program, including everything printed to stderr. If all goes well, all that captured output will be printed to stdout, including everything that was caught from stderr. Only when the program exits with a non-zero exit status will everything be printed to stderr.

## Cronic 

How can we make use of this nifty feature?

Like this:

```cronic your_awesome_program >> your_awesome.log```

All output to stdout will be caught by your log (all went well!). All output to stderr will be caught by crontab which will send it by email if `MAILTO` is set (program exited with non-zeo exit code).

## Logging

What if you also want to log all output, even when something goes wrong?

Then comes in some bash magic!

```
SHELL=/bin/bash
cronic your_awesome_program >> your_awesome.log 2> >(tee -a your_awesome.log >&2)
```

Here we add a stderr redirect (`2>`) to the program [tee][tee]. Tee captures all stdin (through `>(tee ...)` [process substitution][process substitution]), appends it to your_awesome.log, and prints stdin back to stdout. Stdout gets redirected to stderr (`>&2`). And remember: stderr is sent to crontab, which will mail the content to `MAILTO` if set.

## $CRONIC

Lastly, you do not want to write the full path to `cronic` for each crontab entry. Create a bash variable at the start of the crontab, which you then can use in your crontab entry:

```
CRONIC=~/server/resources/cronic
0 0 * * * $CRONIC your_awesome_program >> your_awesome.log 2> >(tee -a your_awesome.log >&2)
```

[cron]: https://en.wikipedia.org/wiki/Cron
[cronic]: https://github.com/Clinical-Genomics/servers/blob/master/resources/cronic
[tee]: https://en.wikipedia.org/wiki/Tee_(command)
[process substitution]: http://tldp.org/LDP/abs/html/process-sub.html
