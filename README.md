# EdgeDeviceDocker
This is a docker and tutorial for edge device.
- ubuntu 20.04 PC
- Nvidia Jetson AGX Xavier

## Steps
1. run `build.sh` to build docker image.
2. run `$ xhost +` in local to allow host connection.
3. run `run.sh` to create and start container.

## Caution
- Make sure `$DISPLAY` is the same in local and docker. Run `$ echo $DISPLAY` to check. If not, set docker's variable to right. Run `$ export DISPAY={what's in local}`.
- The package version list can't be the same in PC and Xavier, I'm still trying to figure out the problem.
- `Dockerfile_xavier is also compatible with PC`

## Todo
- Jetson Nano
