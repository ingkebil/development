# Issue reports

The aim of the issue report is to describe an issue as concisely and clearly as possible.
A suggested minimum description:

Title:

- Steps to reproduce
- Expected outcome
- Actual outcome

## Title

Describe the issue in a sentence that summarises the issue
- Example: Clinical-Genomics - Missing feedback on failed login 

## Steps to reproduce

Describe the steps that are needed to provoke the encountered issue so that anyone can reproduce the issue. 
Any special circumstances that you think is affecting the outcome should be described (e.g. environment/browser etc.) 
Example: 
1. Go to Clinical-Genomics in production environment (https://clinical.scilifelab.se) with a web browser
1. Press "Sign in with Google"
1. Select any of your accounts that don't have access to the system

The aim is to guide the reader towards the problem without having to spend any time on figuring out how or 
having to communicate with the issue reporter on what to do to provoke the system in order to reproduce the issue. 

## Expected outcome

Describe the expected output so that is clear what the goal state is. The aim is to know when issue is resolved.

- Example: A red toast message saying: This account is not whitelisted

## Actual outcome

Describe what happened when the Steps to reproduce where followed. The aim is to guide the reader towards the root of
the problem. (E.g. Is it something that relates to this specific user or something general).

- Example: There is no message at all about what went wrong when I tried to login

> A screenshot of the outcome can often be of great help for the reader to understand what you see 
