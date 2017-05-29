# Perl Best Practices

Following best practices is a good way to create maintainable and readable code and should always be encouraged. However, learning what these best practices are and when they apply in the context of your code can be hard to determine. Luckily, there are several tools to help guide you on your way. 

## Literature

We have already mentioned [perldocs].

Damian Conway's book Perl Best Practices is a very good reference.


## Code standards

### Perl Critic

[Perlcritic] is a Perl source code analyzer. It is the executable front-end to the Perl::Critic engine, which attempts to identify awkward, hard to read, error-prone, or unconventional constructs in your code. Most of the rules are based on Damian Conway's book Perl Best Practices.

Perl critic also has [web interface] to instantly analyze your code. 


### Perl Tidy

[Perltidy] is a Perl script which indents and reformats Perl scripts to make them easier to read. If you write Perl scripts, or spend much time reading them, you will probably find it useful. Perltidy is an excellent way to automate the code standardisation with minimum of effort.  

[perldocs]: http://perldoc.perl.org/index.html
[Perlcritic]: http://search.cpan.org/~petdance/Perl-Critic/bin/perlcritic
[web interface]: http://perlcritic.com/
[Perltidy]: http://perltidy.sourceforge.net/
