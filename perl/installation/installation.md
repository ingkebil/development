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

Use a specific perl version in your current shell, run:
```Bash
$ perlbrew use perl-5.26.1
``` 

### Cpanm
Is a lightweigth CPAN client, which facilitates installing CPAN perl modules. It is a good idea to install it together with Perlbrew to always make them available across each your perlbrew perl installations i.e the CPANM library will change with the perlbrew switch command. 
Installing CPANM with perlbrew is done by this command:
```Bash
$ perlbrew install-cpanm
``` 
Perlbrew makes it easy to create and switch between multiple libraries of CPAN modules. You can even have several libraries for the same distribution of perl.
Here are some examples:
``` Bash
## To create a library named Basil to perl version 5.26.0 
$ perlbrew lib create perl-5.26.0@Basil

## To switch library for that perl distribution permanently
$ perlbrew switch perl-5.26.0@Basil

## If you have another library that you want to use for your current session 
$ perlbrew use perl-5.26.0@Manuel

## To delete your Manuel library 
$ perlbrew lib delete perl-5.26.0@Manuel

## You can view your perl distributions and libraries by running:  
$ perlbrew list  
```
More information on perlbrew is available here:  
https://metacpan.org/pod/distribution/App-perlbrew/bin/perlbrew

[Perlbrew]: https://perlbrew.pl
