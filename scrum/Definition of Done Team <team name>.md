## Definition of Done Team \<team name>

### 1) defect fix/patch

Scope: 
* fixing something that used to work before, but not anymore. There are no changes to functionality.

1) unit tests have to be executed and passed
2) the change needs to be reviewed and approved through a pull request in Github
3) an end user should execute a validation test (acceptance test) in a production-like virtual environment to confirm the fix or patch behaves as expected. There's no need for a test specification.
4) after the validation test, the fix or patch should be merged into production
5) all relevant end users should be informed about the fix or patch

### 2) minor update

Scope: 
* adding functionality
* restructuring

1) see *defect fix/patch*, additionally:
2) automated unit tests for the new functiunality should be in place
3) integration tests (component or system) should be passed
4) the change(s) in functionality should be documented in Github or AM
5) a demo or workshop should be organized to inform all end users of the change(s)


### 3) major update

Scope:
* adding lots of functionality or breaking old functionality, 
* redefining interfaces

1) see *defect fix/patch* and *minor update*, additionally:
2) system or system integration tests should be passed
3) an validation/acceptance test specification should be added to AM-systems, for accreditation purposes
4) an implementation plan should be added to AM-systems, for accreditation purposes

