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

This is a known bug with git-lfs itself and has a nice workaround. Refer to [this section here](https://book.veloren.net/contributors/before-you-contribute.html#forking).

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

### Dependencies

Make sure you have all [runtime dependencies](../introduction/download.md#runtime-dependencies) installed.
