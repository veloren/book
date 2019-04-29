# CI Runner

If you are willing to donate your computer compute time to run tests on Veloren, setting up a Gitlab Runner for Veloren would help us out a lot.

## What is CI?

Continuous Integration (CI) is a set of automated tests and tasks that run on the Gitlab repo every time code is added. This means that Merge Requests have a lower chance of breaking the codebase, and we can automatically get builds of the contributed code, among other benifits.

We need your computer to help us with the testing. It's not free to run CI, so we use our own computers to do it.

## Requirements

- Preferably no internet data caps, as it will consume internet in the background
- ~20gb of free space on your computer. The Docker image is around 2gb, and many of the files can get much larger over time.

## How to set up the runner

First, you will need to contact a maintainer to get a Gitlab runner token. For this, either message @xMAC94x, or @AngelOnFira. We will probably make sure you've been with the project for a bit, as we don't want to give the token to just anyone.

You will need to have Docker installed, as all of the builds use it. You can follow instructions here,

[Linux](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

[Windows](https://docs.docker.com/docker-for-windows/install/)

[MacOS](https://docs.docker.com/docker-for-mac/install/)

Next, clone the [Veloren CI repo](https://gitlab.com/veloren/veloren-docker-ci). In the folder, navigate to runner, then run `./launch-runner`. You will have to input the token, as well as a name for the runner/. The convention for the name is `<discord-username>-<descriptor>`. So for example, @angelonfira's might be `angelonfira-desktop`.

Currently, there is no script for windows, however that will change soon. If you are able to read through the script and adapt it to windows, there aren't many ways it could go wrong though.

After the script finishes, the runner will be running in the background on your computer. It will only take processing power when there are tasks to be done, and nothing should take longer than 10 mins.

Thanks for helping :)