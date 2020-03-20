# Local repository setup and maintenance

This section describes the initial setup and maintenance of your local repository.<br>
**Note**: To understand the following we highly recommend reading about git!

## Download source code

Clone the repository

```
git clone https://gitlab.com/veloren/veloren.git
```

See [Troubleshooting][1] if you cloned the repo before Git LFS was setup

Change your working directory to the cloned repository

```
cd veloren
```

**All commands** in this chapter from now on should be executed from there.

# Basic repo navigation

## Changing branches

In order to try out new unmerged or unfinished features, you may want to switch to a different branch.

To switch to a developement branch

```
git checkout <branch_name>
```

To switch back to master

```
git checkout master
```

## Updating

To download the latest changes and update your current branch

```
git pull
```

To download the latest changes without merging them into your local branch

```
git fetch
```

## The help command

Git also offers a help command with detailed information about other commands

```
git help <optional subcommand name>
```

## Modifying the source code

If you want to modify the source code, refer to the [developer][2] section.

To discard changes you've made to the source code

```
git reset --hard
```

Keep in mind that this deletes all the changes **without a way to recover them**.

To discard your changes with ability to restore them later

```
git stash
```

To restore stashed changes

```
git stash pop
```

## Cleaning old build files

Over time as dependencies get updated, the old compiled versions start to take up a lot of space. To delete them type

```
cargo clean
```

**NOTE**: Keep in mind that cargo will need to recompile all dependencies which can take a long time.

## Updating the toolchain

To update the rust toolchain run:

```
rustup update
```
