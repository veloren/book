# Provide a CI runner

We need to host our own CI runners, if you have a spare pc or server and have some spare compute time for Veloren, it would help us a lot.

## What is CI?

Continuous Integration (CI) is a set of automated tests and tasks that run on the Gitlab repo every time code is added.
This means that Merge Requests have a lower chance of breaking the codebase, and we can automatically get builds of the contributed code, among other benifits.

We need your computer to help us with the testing. It's not free to run CI, so we use our own computers to do it.

## Technology

We use gitlab runners in combination with docker.

## Requirements

- >= 2 cpu cores. we don't cause constant 100% load, but when a compilation even comes it, more cores help to quickly process them.
- 50gb of free hdd space. The docker image contains a cache and is about 20gb additional caches can take up some more space.
- >= 1 Mbit/s internet. you don't need fast internet, but the runner will connect to the internet from time to time. a flat rate is ideal.

## Install a runner

First, you will need to contact a maintainer to get a Gitlab runner token. For this, either message @xMAC94x, or @AngelOnFira. We will probably make sure you've been with the project for a bit, as we don't want to give the token to just anyone.

You will need to have Docker installed, as all of the builds use it. You can follow instructions here,

- [Linux](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
- [Windows](https://docs.docker.com/docker-for-windows/install/)
- [MacOS](https://docs.docker.com/docker-for-mac/install/)

Clone our [Veloren CI repo](https://gitlab.com/veloren/veloren-docker-ci) and start the helper script from the `runner` directory
```bash
git clone https://gitlab.com/veloren/veloren-docker-ci
cd veloren-docker-ci/runner
./launch-runner.sh
# provide the token from above
# provide a name in the style: `<discord-username>-<descriptor>`. So for example, @angelonfira's might be `angelonfira-server-1`.
```
The script will take about 10 minutes and when it's done a docker container is started in the background.
It will only take processing power when there are [Pipelines](https://gitlab.com/veloren/veloren/-/pipelines) to be done.

Currently, the script is Linux only, if you run Windows your best bet is to create a Linux VM (e.g. using Virtualbox and Ubuntu Server 20.04)

## Update a runner

In order to use caches effectively, we need at least `gitlab-runner v13.8.0`.
If your runner is older, please recreate the runner, you can use the `update-runner.sh` script.
Note, it is interactive and requieres your input

```bash
# 1. update repo veloren-docker-ci repo
git pull
# 2. go in runner folder
cd runner
# 3. execute update script
./update-runner.sh
# provide if you want to prune old images, choose yes except if you have certain images you want to keep or run other docker containers
# provide the CONTAINER ID that reflects the old image
# see the Install section above for re-setting up the runner
```
