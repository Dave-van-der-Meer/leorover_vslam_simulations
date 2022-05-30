# leorover_spacer_simulations
Simulations of the LeoRover for ROS

## Required packages

This repository is a slight modification of the Leo Rover package. It contains the modification to the Leo Rover simulation to add an RGB-D camera similar to a Realsense D455 camera. It adds the visual elements
to the URDF and the RGB-D camera Gazeo plug-ins.

This package requires the original packages for the Leo ROver simulation which can be installed with:

```bash
$ sudo apt install ros-noetic-leo-simulator
```

# Installation


- Create a ROS1 workspace (if you don't have one)
```bash
$ mkdir catkin_ws
$ cd catkin_ws
$ mkdir src
```

- Clone the repository
```bash
$ cd src
$ git clone https://github.com/Dave-van-der-Meer/leorover_vslam_simulations.git
$ cd ..
```

- Source the ROS distribution & build packages

If you don't have catkin installed
`$ sudo apt-get install python3-catkin-tools`

In `catkin_ws/`:
```bash
$ source /opt/ros/noetic/setup.bash
$ catkin build
```
*Warnings are fine, errors are not.*

- Launch the simulation

This will launch the simulation using Gazebo and simulate a "fake" leo rover who publish and suscribe to topics.
```bash
$ source devel/setup.bash
$ roslaunch leo_gazebo leo_marsyard2021_world.launch
```

# RTAB-Map
To get rtabmap working, check the ros-wiki page of rtabmap-ros and follow the handheld mapping rgbd tutorial. This will tell you the basic of rtabmap with rgbd. [Rtabmap_ros](https://github.com/introlab/rtabmap_ros/tree/noetic-devel)

- Clone the repo inside your workspace:

`$ git clone https://github.com/introlab/rtabmap_ros.git`

Now you need to tell wich topics are used in your simulation, to do that modify the rtabmap.launch file.

At the ` <!-- RGB-D related topics -->` part, you need to change the topic names of the rgbd camera to the ones of the simulation.

You also need to change one link from `camera_link` to `base_footprint`. This can be found inside the ` <!-- Corresponding config files -->` part at the beginning of the file.


When your changes are done, compile the rtabmap package and source your workspace:
```bash
$ catkin build
$ source devel/setup.bash
```

To launch rtabmap you can start the launch file using:
`$ roslaunch rtabmap_ros rtabmap.launch`

*Follow the rgbd tutorial for more parameters*


# Teleop
If you want to control the rover please first download the right package.

Download:
`$ sudo apt install ros-noetic-teleop-twist-keyboard`

Use the teleopt inside a terminal (**sourced**):
`$ rosrun teleop_twist_keyboard teleop_twist_keyboard.py`

Topic used for the teleop:
`/cmd_vel`
