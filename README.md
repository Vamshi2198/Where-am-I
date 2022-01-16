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

## Overview  
This project is a part of Udacity's Robotics Software Engineer Nanodegree Program. In this project, I used [ROSbot](https://github.com/husarion/rosbot_description) as a mobile robot and [aws-robomaker-small-house-world](https://github.com/aws-robotics/aws-robomaker-small-house-world) as a gazebo world to replicate realistic simulation. ROSbot is localized using ROS AMCL (Adaptive Monte Carlo Localization) package inside a map in the simulation environment. The map is generated using [gazebo_ros_2Dmap_plugin](https://github.com/marinaKollmitz/gazebo_ros_2Dmap_plugin/tree/0820610f46235cd7ce1458ea030ef83b1616da37). 
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
sudo apt-get install ros-(distro)-navigation
```
* ROS map_server package  
```
sudo apt-get install ros-(distro)-map-server
```
* ROS move_base package  
```
sudo apt-get install ros-(distro)-move-base
```
* ROS amcl package  
```
sudo apt-get install ros-(distro)-amcl
```
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
