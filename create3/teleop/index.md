---
title: Drive iRobot Create3
sort: 2
---

**Assumptions:** You installed and setup our ros2 docker container: [Setup ROS2 docker](/manual/ros2)

Begin by ssh'ing into camera.

### Start ros2 docker
If ros2 docker is not running, you can run:
```bash
sudo docker run -it --net host ros_mayfly
```

### Attach to already running ros2 docker
See if docker container is up by running:
```bash
sudo docker ps
```

If docker container is running, you will get output looking something like:
```
CONTAINER ID   IMAGE        COMMAND                  CREATED             STATUS             PORTS     NAMES
a10d849da8cc   ros_mayfly   "/ros_entrypoint.sh …"   About an hour ago   Up About an hour             nice_archimedes
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
Inside ros2 docker, create ros2 workspace folder:
```bash
mkdir -p ~/ros2_ws/src
```

Clone `teleop_twist_keyboard` repository into `src` folder:
```bash
cd ~/ros2_ws/src
git clone https://github.com/ros2/teleop_twist_keyboard
```

From `ros2_ws` folder, install dependencies (there probably are none):
```bash
cd ..
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

