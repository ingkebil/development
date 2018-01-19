# Trouble reports

The aim of the trouble report is to describe a trouble as concisely and clearly as possible.
A suggested minimum description:

Title:

- Steps to reproduce
- Expected outcome
- Actual outcome

## Title

Describe the trouble in a sentence that summarises the trouble
- Example: Clinical-Genomics - Missing feedback on failed login 

## Steps to reproduce

Describe the steps that are needed to provoke the encountered trouble so that a developer can reproduce the trouble 
oneself. 
Any special circumstances that you think is affecting the outcome should be described (e.g. environment/browser etc.) 
Example: 
1. Go to Clinical-Genomics in production environment (https://clinical.scilifelab.se) with a web browser
1. Press "Sign in with Google"
1. Select any of your accounts that don't have access to the system

The aim is to guide the developer towards the problem without having to spending any time on figuring out how or 
having to communicate with anyone on what to do to provoke the system in order to reproduce the trouble. 

## Expected outcome

Describe the expected output so that is clear what the goal state is. The aim is to know when development is done.

- Example: A red toast message saying: This account is not whitelisted

## Actual outcome

Describe what happened when the Steps to reproduce where followed. The aim is to guide the developer towards the root of
the problem. (Is it something that relates to this specific user or something general).

- Example: There is no message at all about what happened when I tried to login

> A screenshot of the outcome can often be of great help for the developer to understand what you see 
