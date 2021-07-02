# Before you contribute

In case you want to contribute code (or added the assets yourself to the game) continue reading.
If you do not want to add your assets yourself skip to [Contributing Assets](#contributing-assets).

## Git Workflow

There are two main options how contributions can be made to the game.
Regardless of how you decide to make your commits, make sure to follow our commit guidelines mentioned below.

### Option #1: the collaboration repository

This is our suggested way of contributing to the project.

This is a public repository where anyone can make branches (after following the steps below),
it's synced with the changes from the main repo on an hourly basis and regular branches
are not shared between the two (the only exception is the master branch).
Having a branch without forking can be more convenient for contributors
as you can avoid all the shortcomings of having a fork.

To make your **first contribution**, follow these steps to gain access to our development repository:
1. Join our collaboration group: https://gitlab.com/veloren/dev.
2. Ping either Core Developers or Admins on [our Discord](https://veloren.net/joinus/) in the #general channel (or whichever channel seems suitable).
   Let us know of your GitLab username and we'll be able to give you developer permissions.
3. Head over to https://gitlab.com/veloren/dev/veloren and clone the repository to your computer.
4. Create a **feature branch** (more details about it below).
   You can now either work on your own or work together with others on the same branch.

The development repository is virtually the same as the main repository
but everyone can manage branches in the development repository without
the possibility of breaking the main repo in any way.

#### Naming feature branches

We use feature branches with the following naming scheme for easily identifying the owner of the branch:

```bash
git checkout -b <your_nickname>/<branch_name>
```

Example: `zesterer/fix_scrolling_in_chat`

### Option #2: fork the repository

The downsides of using a fork:
* You need to configure CI to run on your fork.
* Maintainers can't easily make changes to your merge requests.

But you are free to choose this workflow instead of collaboration repo (see above).
Go to GitLab, to the main repository (not the collaboration one) and use their fork button.
Apply the troubleshooting steps in the next section to get LFS to work.

#### Troubleshooting Git LFS

When working on a fork instead of on a branch in the main repo, you'll need to do the following for the time being due to a bug in git-lfs:

1. Configure git-lfs to ignore smudging:
    ```bash
    git config filter.lfs.smudge "git-lfs smudge --skip -- %f"
    git config filter.lfs.process "git-lfs filter-process --skip"
    ```

2. Add Veloren as your upstream remote:

    ```bash
    git remote add upstream https://gitlab.com/veloren/veloren
    ```

3. Go ahead and run `git lfs pull upstream`, and continue to do so when new assets are added to the repo.

#### Commit guidelines

Regardless of which option you picked, we want our
commit history to be clean and make it easy to keep track of our past changes.
In order to ensure clean commits, we've made a list of suggested practices and tips:

* **Split your changes into reasonably sized, yet logical chunks of work.**

    If you feel a feature can be split into smaller pieces of work, you can reflect that with your commits.
    It can be hard to find a balance between what is the right amount of commits, just try making commits that make sense to you.

* **Use descriptive commit names.**

    Take a moment to shortly describe what your commit changes, or even why it changes something.
    For example, `fixes` is a poor name for a commit as it doesn't tell you anything about meaningful about the commit itself.
    If there's an issue on GitLab that relates to the commit, you may use the issue number and title, e.g. `Fixes #123 - UDP buffer overflow when too many players are on the server`.

* **Use `git commit --amend` to change the last commit.**

    For example, you pushed your change and now CI is reporting that the format check failed,
    now instead of creating a separate commit fixing the commit before it,
    run `cargo fmt` locally, run `git add` and then run `git commit --amend` and `git push -f` to fix the incomplete commit instead of creating a new one.
    The same applies to smaller fixes like spelling errors introduced by yourself, fix the commit where the mistake was made instead creating a new one.
    Do note, sometimes `cargo fmt` formatting rules have changed, in which case formatting may change parts of the codebase you haven't touched.
    In this case, feel free to make a separate commit that formats the entire codebase.

    **Tip**: As you may have noticed, if you already pushed to remote, you will have to force push your amended commit (both `git push --force-with-lease` or `git push -f` will work for this.)

* **Rebasing is a good way to change your commits later on.**

    In case you feel you made a bit of a mess with your commits at some point, you can squash commits and change the commit names.
    1. Count how many commits your branch contains, e.g. in `git status`.
    2. Run `git rebase -i HEAD~N`, where `N` is the number of commits you counted in step 1.
    3. Follow the instructions in the editor. You can change a commit name by modifying the text in a line.
    For example, to squash commit #2 and #3 into a single commit, write `squash` in front of commit #3, no need to change commit #2.
    4. Run `fmt` on every commit in your branch (in bash)
        `git filter-branch -f --tree-filter "cargo fmt" $(git merge-base origin/master HEAD)..HEAD`

### Catching up on changes to the master branch

Often when working on a feature for longer than a day or two, you might notice your branch is falling behind the master branch.
Fortunately, you can catch up on any changes your branch has missed by [rebasing on top of master](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) therefore you should **never** merge master in your feature branch!

#### How to rebase on top of master

1. First, make sure you have no uncommitted work, e.g. by creating a new commit.
2. Run `git fetch --all` to get all the latest changes.
3. Run `git rebase origin/master` to start rebasing.
    You may or may not encounter merge conflicts during, if you don't, proceed to the next step.
    If you do, you will have to resolve the conflicts. These usually arise from recent changes on
    master conflicting with changes of your own and git needs to be told which to prefer. Feel free to
    ask for help on our Discord with that.
3. Run `git push -f` to push your rebased feature branch. It must be a force push as you've changed the existing commit history.

**Tip**: Run `git status` to see the current state of your branch.

## Getting your contribution into the game

You've made a feature branch, made your commits, what now?
Now the branch must be reviewed by other members; to do this you must create a Merge Request on GitLab.

### Creating a Merge Request (MR) on GitLab

1. Once your feature is ready for review, create an [MR in GitLab](https://gitlab.com/groups/veloren/dev/-/merge_requests) from your branch `your-nickname/your-branch-name` to `veloren/veloren/master`.
2. Make sure to tick the box to *delete source branch* in the MR. There's rarely a reason to keep the branch around after merging it.
    Feel free to add additional information to the description.
    Unless the commit history of your branch comprises of clean commits with descriptive titles,
    your MR will be squashed — you may preemptively check the *squash commits* checkbox if you want this to happen.
3. Send a message on our Discord (if you have access in `#programmers` or in a working group channel otherwise in `#general`)
    and mention `@Code Reviewer` with a link to the MR, someone will look over it and will work with you together to get it merged.

## Contributing Assets

If you never worked before with git and just want to contribute assets,
post them in `#veloren-art` on our Discord and ask for feedback. Make sure you own the rights to the assets and agree it being publicly available under [GPLv3](https://choosealicense.com/licenses/gpl-3.0/) license.
**Tip**: Check out the [Artists section](artists) for further information.

## After your first contribution

Congratulations on your first contribution and thank you for helping out!
After your first contribution you should get the `Contributor` role on Discord which gives you access to important channels.

For future contributions develop on a feature branch, _in the Veloren repository_, such as our CI tests can run through and assure you that your work is following the basic rules.
