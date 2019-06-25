# Git workflow

This chapter describes how we use git in order to contribute to Veloren.
So assuming you have a great idea, might be to change a few lines of code, or add some images, modify some models, contribute to the music or fix a translation.
We keep the source of our game in Git, hosted by [gitlab](https://gitlab.com/veloren/veloren.git).

Please now get familiar with git (google) and compile the game once: [Download](/download/index.md)
Then start your `bash` shell

# Forking

You are free to create a fork of Veloren in GitLab and clone it. This is especially recommended if you have no developer rights in GitLab yet (you will get rights after some time).
However you can also get access to the main repository and work in it.
It has the advantage of included CI builds for all commits.

# Feature Branches

We develop in feature branches, so before you start contributing, create your own branch:
```bash
git checkout -b <some_branch_name>
```
In your own branch you can then create commits and push them to your branch how you like it. (see Rule For Commits)

# Rules For Commits

We want our code basis to be clean and make it easy to keep track of our past, this also benefits our future productivity. So there are a few rules regarding code style everyone needs to follow to get accepted.

1. Split your code in reasonable sized logical chunks of work.
Often a feature can be split up in smaller sizes of work, try to make use of it and structure your feature using commits. Don't just make a big commit that contains all the changes, don't make 100 commits that change one line.

2. Name each commit.
Find a good caption for each commit and name it. `fix things` is to unspecific, if a issue exists link it and it's title, e.g. `fixing #123 - UDP buffer overflow when to much player on server`.
If no issue exists, evaluate creating one.
Otherwise, describe shortly but precisely what a commit is about, e.g. `fixup several issues in physics related to collisions`.
Tip: If you struggle finding one title that covers you whole commit, it might be better to split in in 2 parts next time.

3. Use `git commit --amend` in case you forgot to include something in your commit.
E.g. you pushed your change and now fml is failing, than instead of creating a separate commit fixing this commit, run fml locally, run git add and then run `git commit --amend` and `git push -f` to fixup the incomplete commit instead of creating a new one.
The same applies to smaller fixes like spelling errors introduced by yourself, fix the commit where the mistake was made instead creating a new one on top.
Exception: Sometimes fmt changes their rules and untouched code becomes invalid, in case the fml failure is related to fml and not us, it's okay to use `apply fml on whole codebase`. Please don't include other changes in such a commit.

4. Rebase on master
If some time has passed since you started your feature branch, rebase it on top of master from time to time to avoid merge conflicts.
First, make sure you have no uncommitted work, e.g. by creating a new commit.
Run `git fetch --all` and `git rebase origin/master`.
If it returns with no error you are fine, if it returns some, fix the errors and follow the instructions.
Tip: Use `git status` to show next instructions.

5. Fixup your commits afterwards.
In case you didn't created clean commits in the first place, you can squash and change the names now.
First, count how many commits your branch contains, e.g. in `git status`.
Use the number in `git rebase -i HEAD~4`, e.g. for 4 commits on top of master.
Read the instructions in the editor. You can change a commit name by modifying the text in a line.
To Squash Commit 2 and 3 into a single commit, write `squash` in front of the 3rd commit, don't change the second one

# Create a Merge Request

Once your feature is ready for review create MR in GitLab out of your branch from `your-branch-name` to `master`.
Feel free to add additional information to the description (optional).
If you didn't not bother of Rules For Commits above, please cleanup your branch now or consider setting the "squash commits"
Then create a post in the discord and mention @Code Reviewer, someone will eventually look over the MR and will work with you together to get it merged
