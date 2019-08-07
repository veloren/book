# Troubleshooting
This section contains common issues and solutions.

## Git LFS
If LFS is not installed and setup properly the lfs pointers will not be replaced with actual assets. This produces an error when running Voxygen where it complains about the validity of whatever filetype it is trying to load.

### Check status
To check if Git LFS works correctly:
```
git lfs status
```

### When LFS was not setup before cloning the repo
To setup LFS and download the asset files on **Linux** or **Windows**
```
git lfs install
git lfs fetch
git lfs checkout
```
**MacOs**
```
git-lfs install
git-lfs fetch
git-lfs checkout
```

### When using Mingw64 (Windows)
Git LFS fails download the files properly. The main issue seems to be that the askpass program is not spawned when using a normal CMD prompt, preventing Git LFS from authenticating via SSH to retrieve the temporary access token. Setting the SSH_ASKPASS, GIT_ASKPASS and DISPLAY variables seems to solve this issue:

```bat
SET "SSH_ASKPASS=C:\Program Files\Git\mingw64\libexec\git-core\git-gui--askpass"
SET "GIT_ASKPASS=%SSH_ASKPASS%"
SET "DISPLAY=required"
```

### Migrating from submodules
If you used the previous submodules system, you can deactivate it with:
```
git submodule deinit --force --all
```

### Additional Required Libraries
On Debian systems additional libraries may need to be downloaded, below is a non-exhaustive list:

- libglib2.0-dev
- libcairo2-dev
- libasound2-dev
- libpango1.0-dev
- libatk1.0-dev
- libgdk-pixbuf2.0-dev
- libgtk-3-dev

And a one liner to download and install them all:
`sudo apt install libglib2.0-dev libasound2-dev libcairo2-dev libpangol1.0-dev libatk1.0-dev libgtk3.0-dev`