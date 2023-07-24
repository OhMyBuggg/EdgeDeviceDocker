und# EdgeDeviceDocker
This is a docker and tutorial for edge device.
- ubuntu 20.04 PC
    - Docker version 24.0.1
- Nvidia Jetson AGX Xavier: Ubuntu 20.04
- Jetson Nano 2GB
    - Too low to use cpu.
    - Use `LXDE-based desktop` to get more RAM.
    - It doesn't have enough RAM to build my docker.

## Steps
1. run `build.sh` to build docker image.
2. run `$ xhost +` in local to allow host connection.
3. run `run.sh` to create and start container.

## Caution
- Make sure `$DISPLAY` is the same in local and docker. Run `$ echo $DISPLAY` to check. If not, set docker's variable to right. Run `$ export DISPAY={what's in local}`.
- The package version list can't be the same in PC and Xavier, I'm still trying to figure out the problem.
- `Dockerfile_xavier is also compatible with PC`
- Jetson Nano has just one device, maybe it's due to the ubuntu version.
    - https://unix.stackexchange.com/questions/512759/multiple-dev-video-for-one-physical-device

## Todo
- Jetson Nano: 192.168.100.2: Ubuntu 18.04.6 LTS
    - Docker version 20.10.7
    - 1.9G MEM will exploded, so as 100% CPU usage.
    - test_cam.py gives 632M MEM, and 40~50% CPU usage.
    - Dockerfile_cuda can't compatible with nano.
- TX2: Ubuntu 16.04.2 LTS
- Build nvidia/cuda:11.4.3-cudnn8-devel-ubuntu20.04 docker with opencv used CUDA
    - Big failed !!!!!!!!!!!!!!!! -> solved. I am idiot.
    - Docker can run, but GPU can't work with opencv. -> solved

## Update
- There is a built docker.
    - plugin-motion-detector
        - everything goes well, just run it.
            - Xavier need to use --runtime=nvidia
        - Can not show display.
    - plugin-objectcounter
        - default use waggle, need to change to local device. 
        - at least 8GB remain space -> `waggle/plugin-base:1.1.1-ml-torch1.9` this image's file structure isn't same as `waggle/plugin-base:1.1.1-base`, COPY local in it now.(TBD)
        - nano will crash.
        - CUDA different between PC and edge device (11 vs 10.2) -> update docker didn't work
    - sound-event-detection
        - 

## Note
- `$ docker builder prune` to delete docker build cache.


## Result table
| porject | platform | status | comments |
| ------- | -------- | ------ | -------- |
| motion detector | amd64 | ok |         |
|                 | arm64 | ok | 1. use --runtime=nvidia instead of --gpus all 2. can't show display |
| object counter  | amd64 | ok | CUDA 11.4 |
|                 | arm64 | failed | CUDA version 10.2 failed to run code |
| sound detector  | amd64 | ok | No cuda |
|                 | arm64 | ok | No cuda |
