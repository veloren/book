# Before you contribute

Incase you want to contribute code (or added the assets yourself to the game) continue reading.
If you do not want to add your assets yourself skip to [Contributing Assets](#contributing-assets).

## Git Workflow

### Forking

Incase it is your **first contribution** your first step will be to **create a fork of Veloren in GitLab and clone it**.

Incase you've access to the Veloren repository you develop directly on the repository.

When working off a fork instead of on a branch in the main repo, you'll need to do the following for the time being due to a bug in git-lfs:

1. Configure git-lfs to ignore smudging:

        `git config filter.lfs.smudge "git-lfs smudge --skip -- %f"`
        `git config filter.lfs.process "git-lfs filter-process --skip"`

2. Add Veloren as your upstream remote:

        `git remote add upstream https://gitlab.com/Veloren/veloren`

3. Go ahead and run `git lfs pull upstream`, and continue to do so when new assets are added to the repo.

### Feature Branches

We develop in feature branches, so before you start contributing, create your own branch:

```bash
git checkout -b <your_nickname/some_branch_name>
```

In your own branch you can then create commits and push them to your branch how you like it. (see Rule For Commits)

### Rules For Commits

We want our code basis to be clean and make it easy to keep track of our past, this also benefits our future productivity. So there are a few rules regarding code style everyone needs to follow to get accepted.

1. Split your code in reasonable sized logical chunks of work.

   > Often a feature can be split up in smaller sizes of work, try to make use of it and structure your feature using commits. Don't just make a big commit that contains all the changes, don't make 100 commits that change one line.

2. Name each commit.

   > Find a good caption for each commit and name it. `fix things` is to unspecific, if a issue exists link it and it's title, e.g. `fixing #123 - UDP buffer overflow when too many players are on the server`.<br/>
   > If no issue exists, evaluate creating one.
   > Otherwise, describe shortly but precisely what a commit is about, e.g. `fixup several issues in physics related to collisions`.<br/>
   > Tip: If you struggle finding one title that covers you whole commit, it might be better to split in 2 parts next time.

3. Use `git commit --amend` in case you forgot to include something in your commit.

   > For example you pushed your change and now format check is failing, then instead of creating a separate commit fixing this commit, run `cargo fmt` locally, run `git add` and then run `git commit --amend` and `git push -f` to fix up the incomplete commit instead of creating a new one.<br/>
   > The same applies to smaller fixes like spelling errors introduced by yourself, fix the commit where the mistake was made instead creating a new one on top.<br/> **Exception**: Sometimes fmt changes their rules and untouched code becomes invalid, in case the formatting failure is related to fmt and not us, it's okay to use `apply fmt on whole codebase`. Please don't include other changes in such a commit.

4. Fixup your commits afterwards.

   > In case you didn't create clean commits in the first place, you can squash and change the names now.
   > First, count how many commits your branch contains, e.g. in `git status`.
   > Use the number in `git rebase -i HEAD~4`, e.g. for 4 commits on top of master.
   > Read the instructions in the editor. You can change a commit name by modifying the text in a line.
   > To Squash Commit 2 and 3 into a single commit, write `squash` in front of the 3rd commit, don't change the second one
   > 
   > Run fmt on every commit in your branch
   > `git filter-branch -f --tree-filter "cargo fmt" $(git merge-base origin/master HEAD)..HEAD`

5. Keeping your feature up to date

   > If some time has passed since you started your feature branch, rebase it on top of master from time to time to avoid merge conflicts. See below for more information.

### Rebase Strategy

The codebase uses the [rebase strategy](https://www.atlassian.com/git/tutorials/merging-vs-rebasing) therefore _do not_ merge master in your feature branch!

First, make sure you have no uncommitted work, e.g. by creating a new commit.<br/>
Run `git fetch --all` and `git rebase origin/master`.<br/>
If it returns with no error you are fine, if it returns some, fix the errors and follow the instructions.
**Tip**: Incase of an error use `git status` to show next instructions.

## Getting your contribution into the game

### Create a Merge Request

1. Once your feature is ready for review create a MR in GitLab out of your branch from `your-nickname/your-branch-name` to `master`.<br/>
2. Make sure to select `Delete source branch` for the MR.
   Feel free to add additional information to the description.<br/>
   **Note**: _If you didn't bother following Rules For Commits above, please cleanup your branch now or consider setting the `squash commits` option for your MR._<br/>
3. Then create a post in the discord (if you have access in `#programmers` or in a working group channel otherwise in `#general`) and mention `@Code Reviewer`, someone will look over the MR and will work with you together to get it merged.

### Contributing Assets

If you never worked before with git and just want to contribute assets, post them in `#veloren-art` on discord and ask if this can be added to the game. Make sure you own the rights to the assets and agree it being publicly available under GPLv3 license.<br/>
**Tip**: Checkout the [Artists](artists) section.

## After your first contribution

First off, congratulations on your first contribution and thank you for helping out!<br/>
After your first contribution you should get the `Contributor` role on discord which gives you access
to important channels and access to the repository.

For future contributions develop on a feature branch, _in the Veloren repository_, such as our CI tests can run through and assure you that your work is following the basic rules.
