---
title: Drive iRobot Create3 using a sensorleap camera
sort: 1
---

**Assumptions:** You either bought a sensorleap camera where a ros2 docker is preinstalled and running or you installed and setup our ros2 docker container yourself: [Setup ROS2 docker](/sensorleap_manual/ros2)

There are different approaches to driving around the robot:

1. ssh into camera approach
2. send drive instructions from desktop or laptop approach

## ssh into camera approach
Begin by ssh'ing into sensorleap camera.

### Start ros2 docker
Docker container should be running. To make sure run:
```bash
sudo docker ps
```

If docker container is running, you will get output looking something like:
```
CONTAINER ID   IMAGE        COMMAND                  CREATED             STATUS             PORTS     NAMES
a10d849da8cc   ros_mayfly   "/ros_entrypoint.sh …"   About an hour ago   Up About an hour             nice_archimedes
```

If ros2 docker is not running, you can run:
```bash
sudo docker run -it --net host ros_mayfly
```

To attach to the docker container from above and get an interactive bash shell, run:
```bash
sudo docker exec -it a10d849da8cc /bin/bash
```

If attaching to an already running docker container, remember to source ros2 stuff:
```bash
source /opt/ros/humble/setup.bash
```

### Install and run teleop_twist_keyboard package
Create ros2 workspace folder:
```bash
mkdir -p ~/ros2_ws/src
```

Clone `teleop_twist_keyboard` repository into `src` folder:
```bash
git clone https://github.com/ros2/teleop_twist_keyboard
```

From `ros2_ws` folder, install dependencies (there probably are none):
```bash
rosdep install -i --from-path src --rosdistro humble -y
```

Build the package:
```bash
colcon build --packages-select teleop_twist_keyboard
```

It produces a warning about setup.py install being deprecated. This can be ignored.

Source the ros2 workspace
```bash
source install/setup.bash
```

Remember to undock the robot before continuing
```bash
ros2 action send_goal /undock irobot_create_msgs/action/Undock {}
```

Run the teleop_twist_keyboard package
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

Now you can move around the robot with `ijkl` keys.

## send drive instructions from desktop approach
NOT DONE

