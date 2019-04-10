# GitLab and forking Veloren

By now, you should have both Rust and Git installed.

The following assumes you're using bash shell (on Windows git bash) or a similar one.

## Forking the project

To work on Veloren, you first need to create your own fork of the codebase on gitlab. To do that, login or register on gitlab, and head to the main gitlab page of repository you want to fork (for example <https://gitlab.com/veloren/book>). Next click the fork button. You may be taken to a page asking to select namespace you wish to fork the project to, just choose your account. You will get redirected to the page of the forked repository

## Local repository setup

0. Lets assume you want to modify <https://gitlab.com/veloren/veloren.git>.
Your fork is <https://gitlab.com/yourusername/veloren.git>
1. Clone your fork of the repository locally: `git clone git@gitlab.com:yourusername/veloren.git`  
2. Change your working directory to the cloned repository: `cd "veloren"`
3. Add `upstream` remote: `git remote add upstream git@gitlab.com:veloren/veloren.git`
