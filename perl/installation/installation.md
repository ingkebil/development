# Installing Perl
It is usually a good idea to have an admin-free installation of perl. This can be done in several ways. Here we will use [Perlbrew] for a linux installation.

## Perlbrew
Perlbrew is a tool to manage multiple perl installations in your `$HOME` directory. Allowing for testing your production code against different perl versions, while leaving the vendor perl alone. You can even run your programs against all installations of perl. 
1. Disable all previous perl related exports and initiations in bashrc and bash_profile if you have any
1. Log out and in again to initilize a fresh shell
1. Follow the instructions at [Perlbrew] for Installing Perlbrew using curl or wget.
1. Append the following piece of code to the end of your `~/.bash_profile`:
```Bash
    source ~/perl5/perlbrew/etc/bashrc
```
Start a new shell and perlbrew should be up and fully functional from there.

### Perl
Install a specific perl version and use it as default.
```Bash
$ perlbrew install perl-5.26.0
$ perlbrew switch perl-5.26.0
```

### Cpanm
Is a lightweigth CPAN client, which facilitates installing CPAN perl modules. It is a good idea to install it together with Perlbrew to always make them available across each your perlbrew perl installations i.e the CPANM library will change with the perlbrew switch command. You can even have multiple CPANM libraries for each perl version.
Installing CPANM with perlbrew is done by this command:
```Bash
$ perlbrew install-cpanm
```

[Perlbrew]: https://perlbrew.pl
