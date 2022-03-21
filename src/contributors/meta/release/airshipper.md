# Release a new Version

1. Copy over CHANGELOG, update only crates.
   [example MR](https://gitlab.com/veloren/airshipper/-/merge_requests/45)
2. create release branch from master `git checkout -b "r0.7"`
3. create release tag `git tag -a "v0.7.0" -m "release 0.7.0"`
4. push release tag `git push --tag "v0.7.0"`
5. verify a release tag pipeline runs: https://gitlab.com/veloren/airshipper/-/pipelines
6. verify release container is build: https://gitlab.com/veloren/airshipper/container_registry
7. verify [github/airshipper](https://github.com/veloren/Airshipper) actions to build a release binary
8. create a release on github
9. ping `@LunarEclipse#3307` for AUR package update & ping `@Frinksy#1694` for Flathub version.