<h1 align="center">
  <br>
 <img src="https://github.com/Vamshi2198/Where-am-I/blob/main/src/images/Project_Title.png">
  <br>
</h1>
  
<h2 align="center"> Find the location of a mobile robot using AMCL Agorithm</h2>
  
<p align="center">
  <a href="https://www.udacity.com/robotics">
     <img src="https://s3-us-west-1.amazonaws.com/udacity-robotics/Extra+Images/RoboND_flag.png">
  </a>
  <a href="https://husarion.com/manuals/rosbot/">
     <img src="https://github.com/Vamshi2198/Where-am-I/blob/main/src/images/husarion.jpg" width = "100" height = "50" >
  </a>
  <a href="https://aws.amazon.com/robomaker/">
     <img src="https://github.com/Vamshi2198/Where-am-I/blob/main/src/images/aws.png" width = "100" height = "50">
  </a>
</p>

<p align="center">
  <a href="#overview">Overview</a> •
  <a href="#prerequisites">Prerequisites</a> •
  <a href="#directory-structure">Directory Structure</a> •
  <a href="#how-to-launch">How To Launch</a> •
  <a href="#testing">Testing</a>
</p>


![](https://github.com/Vamshi2198/Where-am-I/blob/main/Where-am-I-GIF.gif)

## Overview  
This project is a part of Udacity's Robotics Software Engineer Nanodegree Program. In this project, I used [ROSbot](https://github.com/husarion/rosbot_description) as a mobile robot and [aws-robomaker-small-house-world](https://github.com/aws-robotics/aws-robomaker-small-house-world) as a gazebo world to replicate realistic simulation. ROSbot is localized using ROS AMCL (Adaptive Monte Carlo Localization) package inside a map in the simulation environment. The map is generated using [gazebo_ros_2Dmap_plugin](https://github.com/marinaKollmitz/gazebo_ros_2Dmap_plugin). 
There are two options to control the robot and see how it localizes in the simulation environment: 

1. `2D Navigation Goal`:  
* The first option would be sending a 2D Nav Goal from RViz. The move_base will try to navigate your robot based on the new observation and the odometry to perform the localization, you could also give the robot an initial position estimate on the map using 2D Pose Estimate.

2. `teleop_node`:  
* You can use teleop_twist_keyboard node to control ROSbot using the keyboard keys. 

## Prerequisites
* Gazebo >= 7.0  
* ROS Kinetic  
* ROS navigation package  
```
sudo apt-get install ros-${ROS_DISTRO}-navigation
```
* ROS map_server package  
```
sudo apt-get install ros-${ROS_DISTRO}-map-server
```
* ROS move_base package  
```
sudo apt-get install ros-${ROS_DISTRO}-move-base
```
* ROS amcl package  
```
sudo apt-get install ros-${ROS_DISTRO}-amcl
```
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Directory Structure  
```
.Where-am-I                                    # Where am I Project
├── catkin_ws                                  # Catkin workspace
│   ├── src
│   │   ├── aws-robomaker-small-house-world    # package that contains small house world
│   │   ├── gazebo_ros_2Dmap_plugin            # package that contains plugin to generate map of simulated world
│   │   ├── images 
│   │   ├── my_robot                           # my_robot package 
│   │   │   ├── config                         # config folder for configuration files   
│   │   │   │   ├── base_local_planner_params.yaml
│   │   │   │   ├── costmap_common_params.yaml
│   │   │   │   ├── global_costmap_params.yaml
│   │   │   │   ├── local_costmap_params.yaml
│   │   │   ├── launch                         # launch folder for launch files  
│   │   │   │   ├── amcl.launch                # Launches AMCL node 
│   │   │   │   ├── robot_description.launch
│   │   │   │   ├── world.launch               # Launches bookstore world
│   │   │   │   ├── teleop.launch              # To drive the rosbot
│   │   │   ├── maps                           # folder that contains maps
│   │   │   │   ├── map_generated.pgm
│   │   │   │   ├── map_generated.yaml
│   │   │   ├── meshes                         # meshes folder for sensors
│   │   │   │   ├── astra.stl
│   │   │   │   ├── box.stl
│   │   │   │   ├── rplidar.stl
│   │   │   │   ├── upper.stl
│   │   │   │   ├── wheel.stl
│   │   │   ├── realsense2_camera              # folder that contains launch files for realsense camera
│   │   │   ├── realsense2_description         # folder that contains description files for realsense camera
│   │   │   ├── urdf                           # urdf folder for xarco files
│   │   │   │   ├── materials.xacro            #contains material properties used in rosbot
│   │   │   │   ├── my_robot.xacro             
│   │   │   │   ├── rosbot.gazebo              #contains plugins to interact with rosbot
│   │   │   ├── worlds                         # world folder for world files
│   │   │   │   ├── empty.world
│   │   │   ├── CMakeLists.txt                 # compiler instructions
│   │   │   ├── Where-am-I.rviz                # rviz configuration
│   │   │   ├── package.xml                    # package info
│   │   ├── teleop_twist_keyboard              # package that contains teleop_node to control ROSbot with keyboard
```
## How To Launch

#### Clone the project in catkin_ws/src/ and source the environment
```sh
$ cd /home/workspace/catkin_ws/src/
$ git clone https://github.com/Vamshi2198/Where-am-I
$ source /opt/ros/${ROS_DISTRO}/setup.bash
```
#### Note : The world file proivided is empy because it only contains the url of remote repository, for this purpose you need to clone the aws-bookstore-world and place it inside your src folder. Also, delete the folder named aws-robomaker-bookstore-world manually before cloning.
```sh
$ cd /home/workspace/catkin_ws/src/Where-am-I/src/
$ git clone https://github.com/aws-robotics/aws-robomaker-small-house-world
```
#### Also, repeat the same with gazebo_ros_2Dmap_plugin and teleop_twist_keyboard packages. i.e, remove the empty file folder and clone the packages
```sh
$ cd /home/workspace/catkin_ws/src/Where-am-I/src/
$ git clone https://github.com/marinaKollmitz/gazebo_ros_2Dmap_plugin
$ git clone https://github.com/ros-teleop/teleop_twist_keyboard
```
#### Build the `Where-am-I` project
```sh
$ cd /home/workspace/catkin_ws/ 
$ catkin_make
```
#### After building the package, source your workspace
```sh
$ cd /home/workspace/catkin_ws/
$ source devel/setup.bash
```
#### Launch my_robot in Gazebo
```sh
$ roslaunch my_robot world.launch
```
#### Launch amcl node 
```sh
$ rosrun my_robot amcl.launch
```

## Testing
Click the `2D Nav Goal` button in the toolbar, then click and drag on the map to send the goal to the robot. It will start moving and localize itself in the process. if you want to use teleop_node then run :
```sh
$ roslaunch teleop_twist_keyboard teleop_twist_keyboard.py
```
The code was tested on the following specifications:
- **Processor:** `Intel Core i7-10875H`
- **Graphics:** `Nvidia GeForce GTX 1650 Ti 4GB GDDR6`
- **OS:** ` Ubuntu 20.04.3 LTS`
- **Kernal:** `5.10.60.1-microsoft-standard-WSL2`
- **ROS:** `noetic`

