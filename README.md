# Autoware in CARLA

The carla autoware bridge is now hosted and maintained [here](https://github.com/Autoware-AI/simulation/tree/master/carla_simulator_bridge).

This repository contains a demonstrator of an autoware agent ready to be executed with CARLA **0.9.12**. You can download it from [here](https://github.com/carla-simulator/carla/releases/tag/0.9.12)**. It should also work for the latest version of carla but not be tested.

## CARLA autoware agent
The autoware agent is provided as a ROS package. All the configuration can be found inside the `carla-autoware-agent` folder.

![carla-autoware](docs/images/carla_autoware.png)

The easiest way to run the agent is by building and running the provided docker image.

### Requirements

- Docker (19.03+)
- Nvidia docker (https://github.com/NVIDIA/nvidia-docker)

### Setup

1. Firstly clone the carla autoware repository, where additional [autoware contents](https://bitbucket.org/carla-simulator/autoware-contents.git) are included as a submodule:

```sh
git clone --recurse-submodules git@github.com:yao-deng/carla-autoware.git
```
2. Copy the folder `PythonAPI` from your carla path to this project.

3. Afterwards, build the image with the following command:

```sh
cd carla-autoware && ./build.sh
```
Note: in `Dockerfile`, change `carla-0.9.12-py2.7-linux-x86_64.egg` in Line 62 to the your carla version.

This will generate a `carla-autoware:latest` docker image.

### Run the agent

1. Run a CARLA server.

```
./CarlaUE4.sh
```

2. Run the `carla-autoware` image: 

```sh
./run.sh
```

This will start an interactive shell inside the container. To start the agent run the following command:

```sh
roslaunch carla_ad_demo carla_ad_demo.launch
```

## CARLA Autoware contents
The [autoware-contents](https://bitbucket.org/carla-simulator/autoware-contents.git) repository contains additional data required to run Autoware with CARLA, including the point cloud maps, vector maps and configuration files.

## TODO
The command `roslaunch carla_autoware_agent carla_autoware_agent.launch town:=Town01` doesn't work. Need to fix