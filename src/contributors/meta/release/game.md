# Release a new Version

1. Copy over CHANGELOG, update only `server`, `client`, `server-cli`, `voxygen` crates - the others are on a independent [semver](https://semver.org/).
[example MR](https://gitlab.com/veloren/veloren/-/merge_requests/3219)
2. create release branch from master `git checkout -b "r0.12"`
3. create release tag `git tag -a "v0.12.0" -m "release 0.12.0"`
4. push release tag `git push --tag "v0.12.0"`
5. verify a release tag pipeline runs: https://gitlab.com/veloren/veloren/-/pipelines
6. verify release container is build: https://gitlab.com/veloren/veloren/container_registry
7. add link to https://veloren.net/download-other/
8. create a release on gitlab
9. verify a release binary is copied to wasabi