# Autopilot system for _Tesla_ cars

Mentors: [Yeeshukant Singh](https://github.com/Yeeshukant), [Kshitij Bhat](https://github.com/KshitijBhat)

Members : 
- [Aditya Suwalka]( https://github.com/git-suwalkaaditya)

- [Tarun Kumar Patel]( https://github.com/git-tarunkp)

- [Soham Mondal]( https://github.com/Aryasmiiti14)
- [Anurag Srivastava]( https://github.com/Sigmanurag)


 **Description**:
-  While on the highway, the monotonous speed
control is a bit tiresome for drivers (especially for long
distances and longer durations). Lane Assist and Adaptive
Cruise Control (ACC) features can help the drivers in these
situations. Depending on the actions of other
objects/vehicles in the car's immediate vicinity, these
systems can slow down and stop the vehicle when required.

**Specifications**:
- Computer Vision Pipeline for Lane detection should be
efficient in detecting the free path on the road.
- Motion planning and control systems are needed to steer
the vehicle to have the least cross-track error and
automatic lane centering.
- Bonus points for an active obstacle avoidance system to
change lanes and avoid other cars in the lane.



<div id="top"></div>

<br>
<div align="center">
 <img src="https://github.com/gmeidk/DelyBot/blob/d6c620261c2f81553f9dc13830cff278a25ad252/MEDIA/robot.png?raw=true" alt="DelyBot" height="180" width="200"> 
</div>
<h3 align="center">DelyBot</h3>
<p align="center">Ready to serve you anytime, anywhere.</p>
<br>

<!-- ABOUT THE PROJECT -->
## About The Project

### Built With

* [ROS Noetic](https://www.ros.org/)
* [ROS Navigation Stack](http://wiki.ros.org/navigation)
* [ROS robot_localization](https://github.com/cra-ros-pkg/robot_localization)
* [Gazebo](https://gazebosim.org/)
* [Python](https://www.python.org/)

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- GETTING STARTED -->
## Getting Started

### Prerequisites

At first it is necessary to install external packages:

* navigation
  ```sh
  sudo apt install ros-noetic-navigation
  ```

* slam-gmapping
  ```sh
  sudo apt install ros-noetic-slam-gmapping
  ```

* map-server
  ```sh
  sudo apt install ros-noetic-map-server
  ```
  
* robot_localization
  ```sh
  sudo apt-get install ros-noetic-robot-localization
  ```

<br>

### HOW IT WORKS

<div id="top"></div>

<br>
<div align="center">
 <img src="https://github.com/git-suwalkaaditya/IITISoC-22-Auto4-Autopilot-System-Cars/blob/main/navigation%20.png" height="500" width="1500"> 
</div>

<br>
Robot navigation is implemented in the delybot_navigation package.

In the amcl.launch file, Adaptive Monte Carlo Localization (AMCL) is implemented, which 
is a method for localizing the robot and tracking its pose in a map.
The optimal path planning from the robot pose to the target pose with prior knowledge of the 
environment and static obstacles is done by the basic Global Planner.
On the other hand, the Local Planner computes in real-time the new path to avoid dynamic 
obstacles. It is possible to choose between two implemented Local Planners: DWA and
Trajectory Rollout, both of which work efficiently.

### Installation
1. First make a catkin workspace 
   ```sh
   mkdir -p catkin_ws/src
   
2. Clone the repo inside the catkin workspace
   ```sh
   cd ~/catkin_ws/src
   git clone https://github.com/git-suwalkaaditya/DelyBot.git
   ```
3. Build packages
   ```sh
   cd ~/catkin_ws
   catkin_make
   ```
4. Before running any roslaunch and rosrun command, run the following command
   ```sh
   source devel/setup.bash
    ```
   
<p align="right">(<a href="#top">back to top</a>)</p>


<!-- USAGE EXAMPLES -->
## Usage
The possible  **_optional parameter_** values are listed in the table. <br>

| Optional Parameter | Values | Default |
| --- | :---: | :---: |
| `open_rviz` | true, false | true |
| `world` | empty, delybot_test_map, delybot_test, district_map, district | district |
| `dwa_local_planner` | true, false | true |

<br>

The **world** parameter can be used to load a specific world map (the *.world* file must be located in the *delybot_description/world/* folder). <br>
To test the different world files in Gazebo it is possible to run the following command:
  ```sh
  # Usage example to open district.world in Gazebo
  roslaunch gazebo_ros empty_world world_name:=/home/your_username/catkin_ws/src/DelyBot/delybot_description/world/district.world
  ```

<br>
<br>

### delybot_description

  ```sh
  roslaunch delybot_description display.launch
  ```
Open a pre-configured Rviz session to display the robot.
  ```sh
  roslaunch delybot_description gazebo.launch open_rviz:=true
  ```
Spawn the robot into the gazebo simulation environment.
If the **open_rviz** optional parameter is *true* a pre-configured Rviz session is also opened.

<br>

### delybot_control

  ```sh
  roslaunch delybot_control ddr_control.launch world:=district
  ```
Spawn the robot with a differential drive control and a teleoperation node in gazebo. <br>

<br>

### delybot_slam

  ```sh
  roslaunch delybot_slam delybot_slam.launch world:=district_map
  ```
This command can be useful to create a 2d map of a specific world using a gmapping algorithm. <br>

<br>

### delybot_navigation

  ```sh
  roslaunch delybot_navigation delybot_navigation.launch world:=district dwa_local_planner:=true
  ```
This command is used for the robot navigation, it's possible to give through Rviz a desired goal pose. <br>
If the **dwa_local_planner** parameter is *true* the *DWA* local planner is used, else if it is *false* the *Trajectory Rollout* local planner is used. 

<br>


#### waypoint_spawner node

  ```sh
  rosrun delybot_navigation waypoint_spawner.py
  ```
This command run the waypoint_spawner node, used to send a specific goal pose selected from a predefined list to the robot. <br>
The list is imported from the **waypoint.json** file inside the *delybot_navigation/scripts/* folder. <br>

  ```sh
  # Output example
  user@user:~$ rosrun delybot_navigation waypoint_spawner.py 

  GOAL LIST:
  0) Origin
  1) Thrift Shop
  2) Salon
  3) Home
  4) Post Office
  5) Police
  6) School
  7) Fast Food

  Insert goal index: 
  ```

<!-- ROADMAP -->
## Roadmap

- [x] 3D robot modeling
- [x] Add differential drive control
- [X] Add laser and imu sensors using Kalman filter (pkg: robot_localization) 
- [X] Add world 3D model with static and moving obstacle 
- [X] Add delybot slam using gmapping to create 2D world map
- [X] Add delybot navigation
- [X] Add waypoint spawner node
- [X] Update README


<p align="right">(<a href="#top">back to top</a>)</p>

## Gazebo Simulation
https://github.com/git-suwalkaaditya/IITISoC-22-Auto4-Autopilot-System-Cars/blob/main/simulation%20video.webm

<p align="right">(<a href="#top">back to top</a>)</p>

<!-- CONTACT -->
## Reference

For further information check the report - [DelyBot Report.pdf](https://bit.ly/3GNdJTN)

https://roscon.ros.org/2017/presentations/ROSCon%202017%20Vehicle%20and%20City%20Simulation.pdf

https://github.com/theAIGuysCode/YOLOv4-Cloud-Tutorial

https://github.com/osrf/car_demo

https://github.com/gmeidk/DelyBot

http://kth.diva-portal.org/smash/get/diva2:1057261/FULLTEXT01.pdf

https://medium.com/intro-to-artificial-intelligence/model-predictive-control-udacitys-self-driving-car-nanodegree-ad7cf64fd0e4

[1] navigation package: http://wiki.ros.org/navigation

[2] slam-gmapping package: http://wiki.ros.org/gmapping

[3] map-server package: http://wiki.ros.org/map_server

[4] robot-localization package: http://wiki.ros.org/robot_localization

[5] actor: http://gazebosim.org/tutorials?tut=actor&cat=build_robo

<p align="right">(<a href="#top">back to top</a>)</p>
 
## Contacts
**Aditya Suwalka:**
[![](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/aditya-suwalka-8975b4243)
[![](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/git-suwalkaaditya)
[![](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:me210003008@iiti.ac.in)

**Tarun Kumar Patel**
[![](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/tarun-kumar-patel-5245b6243)
[![](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/git-tarunkp)
[![](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:me210003075@iiti.ac.in)

**Soham Mondal:**
[![](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/soham-mondal-4795b6243)
[![](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Aryasmiiti14)
[![](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:me210003071@iiti.ac.in)
[![](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://www.instagram.com/soham_iit_i)
[![](https://img.shields.io/badge/Twitter-0077B5?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/SohamMo46006060?t=4BcVPjN5oIqFWPKNh6HvUQ&s=08)


**Anurag Srivastava:**
[![](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/anurag-srivastava-86b409231)
[![](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Sigmanurag)
[![](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:me210003013@gmail.com)



## TAKE A LOOK AT BRANCH 3 ALSO
