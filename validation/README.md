# Validation

   1. [Purpose](#1-purpose)
   2. [Motivation](#2-motivation)
      * [Prerequisites](#21-prerequisites)
      * [Documentation](#22-documentation)
   3. [Testing](#3-testing)
      * [Setup](#31-setup)
      * [Installation](32-installation)
      * [Databases](#33-databases)
      * [Data](#34-data)
      * [Tests](#35-tests)
   4. [Validation](#4-validation)
      * [Patch](#41-patch)
      * [Minor](#42-minor)
      * [Major](#43-major)

## 1. Purpose
This document aims to outline a workflow for how we test new software before deploying to production.

## 2. Motivation
It is very rare that software systems stay frozen. In this way, software development is distinctly different from method development in the lab. When software goes stale they tend to accumulate issues that in the end snowball into big problems. This is why many companies adopt strategies to keep improving their code constantly in small increments. That way you can quickly act on small issues or respond to changes as soon as possible.

It becomes difficult then to follow the same validation workflow used for developing lab methods if you want to update tools and methods several times per week. Therefore we need a way to do this in a safe and clearly documented way.

## 2.1 Prerequisites
In order for this to work we need to streamline how new/updated code is deployed. This means we need to automate as much of the process as possible. We also need to trust that the new code will behave as expected. It’s therefore required to run tests continuously whenever we change some code. This also need to be as automated as possible.

## 2.2 Documentation
All the code in our system should be version controlled where every change to the codebase is time stamped, commented on, and can be tracked to a specific Git commit. This is the most granular level of documentation but will suffice for most of the small updates.

We also provide a structured versioning of the individual tools following [semantic versioning](https://semver.org/) conventions. Every tool is accompanied by a “change log” that summarises the most significant changes between two versions.

## 3 Testing
There’s multiple levels of testing software. You need small, quick, and directed tests (unit tests) to make sure that you cover edge cases and stay clear of obvious coding errors (e.g. misspelling a variable). These tests can be run constantly and on any computer/server.

Then there’s a layer on top of the small tests that combine multiple tools and tests e.g. the entire workflow on a high level (integration tests). These tests don’t concern themselves so much with edge cases and are perhaps run in a production-like environment only once before new code is deployed to the system.

### 3.1 Setup
Unit tests are setup for each package/tool separately. They tend to use the py.test test-runner or a test anything protocol (TAP) and are automated using TravisCI. This makes it possible to track each result in the GitHub interface.

It’s important that the environment used to run the integration tests behave as close to the production environment as possible. We achieve this by running the development code on the same hardware alongside the production code, but in isolated test environments.

### 3.2 Installation
All production code is installed in a conda environments following this naming [convention](http://localhost:4000/conda/conda_conventions.html):

`[P]_[main-process]_[creation-date(YYMMDD)]`

Development packages are installed in the conda environments and named as follows:

`[D]_[main-process]_[creation-date(YYMMDD)]_[signature_of_creator]`

When it is time to move your development environment to production - make a copy of it using conda and rename it following the above conventions.

As for configs and supporting infrastructure we use the same structure as for production but using the alternate root:

`/mnt/hds/proj/bioinfo/develop/SERVER`

`/mnt/hds/proj/bioinfo/develop/customers`

### 3.3 Databases
Many tools use databases to store data. Even with daily backups, losing this information would cause many problems. We are therefore using a separate database-instances for development tools.

   * MySQL (AWS)
   * MongoDB (clinical-db)
   * MySQL (clinical-db)

### 3.4 Data
Test data should exist to start the integration tests from some key entry points:

   * Demultiplexing from the BCL output of a flowcell
   * Data analysis from linked FASTQ-files

### 3.5 Tests
This dependent on how each tool or method is set-up. There should be adequate tests, data, environements to cover major, minor and patch updates. In the end, it should report if everything proceeded according to expectations or not. All tests need to pass so a simple check; “yes” or “no” will suffice. 

## 4 Validation

The validation needs to be documented in an automated way. Only for major updates or completely new methods do we intend to manually document using the test specification + implementation plan approach.

For the rest of the updates it should be possible to track the information required through a combination of Git commits, TravisCI statuses, and an overall log that summaries results from each integration test run 

### 4.1 Patch

A patch version update can be pushed to production if it passed the relevant unit tests. The change should be so small that the function of the software will be completely covered by the automated unit tests.

### 4.2 Minor

A minor version update can be pushed to production if it passed the relevant unit tests and integration tests, if applicable, and manual curation of relevant test data output if not completely covered by the automated tests.

### 4.3 Major

A major version updated can be pushed to production if it passed the relevant unit tests and integration tests, and manual curation of relevant test data output if not completely covered by the automated tests as well as approved test specification and implementation plan.
