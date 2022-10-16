# Local repository setup and maintenance

This section describes the initial setup and maintenance of your local repository.<br>

_**Note:** To understand the following we highly recommend reading about git!_

## Download source code

**Note:** Veloren needs [git LFS installed](development-tools.md#git-lfs) before cloning to be able to download the assets. If you already cloned the repository before setting up git LFS use [these steps](troubleshooting.md#when-lfs-was-not-setup-before-cloning-the-repo) to get the assets downloaded.

Clone the repository

```
git clone https://gitlab.com/veloren/dev/veloren.git
```

Change your working directory to the cloned repository

```
cd veloren
```

**Note:** _All commands in this chapter from now on should be executed from there._

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

If you want to modify the source code, refer to the [developer](developers) section.

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

**NOTE:** Keep in mind that cargo will need to recompile all dependencies which can take a long time.

## Updating the Rust toolchain

We use a [`rust-toolchain`](https://github.com/rust-lang/rustup#the-toolchain-file) file in the repository which will automatically update
your rust toolchain to whichever version we use. There shouldn't be any additional effort needed on your side.
