# Troubleshooting

Incase you've hit an issue this section might help you resolve it.

## Git LFS

If LFS is not installed and setup properly the lfs pointers will not be replaced with actual assets. This produces an error when running Voxygen where it complains about the validity of whatever filetype it is trying to load.

### Check status

To check if Git LFS works correctly:

```bash
git lfs status
```

### When LFS was not setup before cloning the repo

To setup LFS and download the asset files on **Linux** or **Windows**

```bash
git lfs install
git lfs fetch
git lfs checkout
```

**MacOs**

```bash
git-lfs install
git-lfs fetch
git-lfs checkout
```

### Git pull/rebase failed due to a smudging error/404

This is a known bug with git-lfs itself and has a nice workaround. Refer to [this section here](before-you-contribute.html#forking).

### When using Mingw64 (Windows)

Git LFS fails download the files properly. The main issue seems to be that the askpass program is not spawned when using a normal CMD prompt, preventing Git LFS from authenticating via SSH to retrieve the temporary access token. Setting the SSH_ASKPASS, GIT_ASKPASS and DISPLAY variables seems to solve this issue:

```bash
SET "SSH_ASKPASS=C:\Program Files\Git\mingw64\libexec\git-core\git-gui--askpass"
SET "GIT_ASKPASS=%SSH_ASKPASS%"
SET "DISPLAY=required"
```

### Migrating from submodules

If you used the previous submodules system, you can deactivate it with:

```bash
git submodule deinit --force --all
```

## Autoformat with git commit hook

You can setup a git commit hook to automatically format your code before commiting if your IDE doesn't support it by default.
Just create a file `.git/hooks/pre-commit` with the following content.
```bash
#!/bin/sh
#
# An example hook script to verify what is about to be committed.
# Called by "git commit" with no arguments.  The hook should
# exit with non-zero status after issuing an appropriate message if
# it wants to stop the commit.
#
# To enable this hook, rename this file to "pre-commit".

# run rustfmt to auto check changed files
changefmt=$(git config --bool hooks.changefmt)

rustup component add rustfmt-preview
if [ "$changefmt" != "true" ]
then
  exec cargo fmt --all -- --check
else
  echo "change files via fmt"
  cargo fmt --all --
  echo "adding all files via git add ."
  exec git add .
fi

# enable change to make fmt change files instead of just warn
# git config hooks.changefmt true
```

## Dependencies

Make sure you have all [runtime dependencies](../introduction/download.md#runtime-dependencies) installed.
