# Security

One of the most important and often overlooked topic.

## Passwords

Passwords are everywhere. It's still the prefered way to authenticate across a broad set of areas from databases, online sites, servers, tools etc. What makes a strong password is usually correlated with how difficult it is for a human to remember and deal with. This is why we have...

### Password managers

A password manager is a piece of software that takes much of the complications out of storing and accessing passwords and other "secrets". They can usually help you fill in web forms automatically and some even have accompanying command line tools.

Here is a great introduction from [The Verge](https://www.youtube.com/watch?v=Q0GeMSFGIgI&feature=share).

The great thing with using such tools is that you can afford to make your passwords _really_ secure, unique for each site/app/database, and change them without problem e.g. if you suspect they might have been compromised.

## Databases

All production databases should be password protected. It's okey to have a "root" or "admin" user with universal access, however, credentials used for web services and command line interfaces should be as limited as possible. It's a good idea to setup one user per database to avoid accidentally deleting tables e.g.

It also goes almost without saying that you need a separate user with ONLY access to test/stage databases.

## Two-factor authentication

If your password is compromised you are usually in trouble unless you manage to detect the leak and issue a password-reset on your account. A smart way of adding a second layer of protection is to use a secondary authentication method. A common pattern is to dispatch temporary codes which can only be accessed on _your_ cell-phone. By using this authentication method and a password you have _two factors of authentication_. Either one can be compromised while keeping your account safe.

It's highly recommended to enable 2-factor authentication on (mission critial) accounts.

## Authentication vs. authorization

There's an important distinctions between these two topics. **Authentication** happens when you verify that you are who you are; by logging into your Google account, providing your fingerprint, etc.

**Authorization** on the other hand is the process of determining what your user in a given context has access to. Perhaps your email needs to be associated with an "admin" role to be granted access to delete a record from a database. Another email might only be granted read-access to the same database.
