# GitLab and forking Veloren

By now, you should have both Rust and Git installed.

The following assumes you're using bash (on Windows git bash) or something similar.

## Forking the project

To work on Veloren, you first need to create your own fork of the codebase on GitLab. To do that, login or register on GitLab, and head to the main GitLab page of repository you want to fork (for example <https://gitlab.com/veloren/book>). Next click the fork button. You may be taken to a page asking to select a namespace you wish to fork the project to, just choose your account. You will get redirected to the page of the forked repository.

## Local repository setup

Lets assume you want to modify <https://gitlab.com/veloren/veloren.git>.
And your fork is <https://gitlab.com/yourusername/veloren.git>
```bash
#1 Clone your fork of the repository locally
git clone git@gitlab.com:yourusername/veloren.git
#2 Change your working directory to the cloned repository
cd veloren
#3 Add `upstream` remote to point to the main repository
git remote add upstream git@gitlab.com:veloren/veloren.git
```
